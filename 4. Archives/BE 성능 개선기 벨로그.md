![post-thumbnail](https://velog.velcdn.com/images/kkhkr98/post/1894e7f7-fd23-4251-9527-13c40e2339ef/image.png)

## 문제상황

![](https://velog.velcdn.com/images/kkhkr98/post/ed9b9625-c83a-4d16-8ad0-491313f605b5/image.png)

산학협력 인턴십을 통해 '야생동물 질병관리 시스템'의 환경시료 관리 페이지 개발을 담당하였다.

사용자가 환경시료를 직접 DB에 접근하지 않고 편리하게 관리할 수 있도록  
엑셀 업로드/다운로드, 시료 추가, 시료 수정, 시료 삭제 등의 기능을 구현하였다.

이 때 ibSheet를 통해 시료 데이터를 323건 이상 추가/수정하고 저장 시 일부 데이터가 누락되는 현상이 발생하였다.

## JDBC template batchUpdate

처음엔 데이터가 많아져서 지연 시간이 늘어나 일부 데이터가 누락되는 현상으로 판단하였다.

기존에 팀에서 대규모 gis 데이터를 서버에 저장하는 코드에 jdbc template batch를 도입한 적이 있으니  
시료 관리에도 도입하면 속도를 개선할 수 있을 것이라고 판단하였다.

```java
// 간략화한 코드
String insertSql =  "INSERT INTO EXAMPLETABLE "
			+ "(MAINKEY, B, C, D, E) "
			+ "VALUES (SEQ.NEXTVAL, ?, TO_DATE(?, 'YYYYMMDD'), TO_DATE(?, 'YYYYMMDD'), ?);";
            
public void batchInsert(List<ExampleSheet> list) {
		try {
			jdbcTemplate.batchUpdate(insertSql,
				new BatchPreparedStatementSetter() {
					@Override
					public void setValues(PreparedStatement ps, int i) throws IllegalArgumentException {
						SaveEnvrmtSmplSheet sess = list.get(i);
						try {
							ps.setString(1, sess.getB());
							ps.setString(2, sess.getC());
							ps.setString(3, sess.getD());
							ps.setString(4, sess.getE());
                            ...
						} catch (SQLException e) {
							logger.error("SQL ERROR : " + "batchInsert", e);
						}
					}
					
					@Override
					public int getBatchSize() {
						return list.size();
					}
			});
		}catch(ArithmeticException | IllegalArgumentException | IndexOutOfBoundsException | NoSuchElementException | NullPointerException e) {
			logger.error("ERROR : " + "ExampleSheetBatchRepository.batchInsert", e);
			throw e;
		}
}
```

이때 ExampleSheet는 JPA, lombok을 활용해 빌더 패턴으로 설계한 DTO이다.  
JDBC template의 batchUpdate 메소드를 사용하면 기존엔 100번의 통신에 update 쿼리를 요청할 걸 한꺼번에 쿼리를 모아서 보낼 수 있다.

속도가 빨라졌으니 문제가 해결됐을것이라고 생각했다.  
그러나 데이터 누락 문제는 속도가 빨라졌음에도 해결되지 않았다.

## Save 함수 직접 구현

속도를 개선하였으나 보낼 수 있는 데이터의 갯수(323건)은 그대로였다.  
즉 다른 원인이 존재한다는 뜻이다.

웹 브라우저의 용량 문제, DBMS 문제 등 여러 원인을 상정하고 디버깅을 했다.

- IBSHEET 데이터를 json화해서 찍어보니 클라이언트에서 데이터 결손은 없었다.
- Spring controller가 받는 데이터 자체에 누락이 있었다.

따라서 통신 중에 데이터 누락이 있음을 확신했고,  
IBSHEET의 DoSave 메소드는 데이터를 url 쿼리 스트링 방식으로 보내기 때문에 용량에 제한이 생긴다.

따라서 http 메시지 바디 부분에 json을 실어 보내도록 저장 함수를 새롭게 짰다.

```javascript
// 자바스크립트 코드
function ibSheetModifiedSave(url){
  	// 데이터 validation 체크
	manualValidation();
	if(isValidated) {
		isValidated = false;
		return;
	}
	// 중복 검사
	if(checkDupl()) return;
	
	var saveData = mySheet1.GetSaveJson();
	ibSheetJsonSave(saveData.data, url);
}

function ibSheetJsonSave(data, url){
	$.ajax({
		type: 'POST',
		url: url,
		data: JSON.stringify(data),
		contentType: 'application/json',
		beforeSend: function() {
        	// IBSHEET 로딩 이미지 띄우기
        	mySheet1.ShowProcessDlg("Save"); 
	    },
		success: function(response){
			let parsedXml = parseXml(response);
			mySheet1_OnSaveEnd(parsedXml.code, parsedXml.message);
	    },
	    error: function(error){
			alert("오류 발생");
          	...
	    },
		complete: function() {
        	// IBSHEET 로딩 이미지 제거
			mySheet1.HideProcessDlg("Save");
		},
  	})
}
```

기존 DoSave함수는 저장 직전 이벤트로 메소드들을 실행할 수 있는 기능이 있었으나,  
직접 구현하니 Validation 로직 등을 직접 구현해줘야 했다.

### Map<String, Object>[] -> Map<String, String[]> 변환 메소드 구현

또한 url 쿼리 대신 json으로 데이터를 받기위해 새롭게 컨트롤러를 설계하였으니 기존 서비스 코드에 parameter로 들어가는 자료구조와 일치하지 않는 문제가 발생했다.

- 기존 코드의 url 쿼리를 통해 받은 데이터 자료구조는 **Map<String, String[]>**이다.
- @RequestBody 어노테이션으로 받은 json 데이터의 자료구조는 **Map<String, Object>[]**이다.

따라서 기존코드와 호환성을 위해,  
Map<String, Object>[] => Map<String, String[]> 변환 메소드를 구현하였다.

```java
// 자바 코드
public Map<String, String[]> paramToJsonConverter(Map<String, Object>[] data){
		HashMap<String, ArrayList> convertMap = new HashMap<>();
		Map<String, String[]> sheetDataMap = new HashMap();
		
		for(int i = 0; i < data.length; i++) {
			for(String key : data[i].keySet()) {
				if(i == 0) {
					ArrayList<Object> lst = new ArrayList<>();
					convertMap.put(key, lst);
				}
				ArrayList currentList = convertMap.get(key);
				currentList.add(data[i].get(key));
			}
		}
		
		for(String key : convertMap.keySet()) {
			ArrayList<String> currentList = convertMap.get(key);
			String[] currentArray = new String[currentList.size()];
			int size = 0;
			for(Object temp : currentList) {
				currentArray[size++] = String.valueOf(temp);
			}
			sheetDataMap.put(key, currentArray);
		}
		
		return sheetDataMap;
	}
```

## 성능개선

결과적으로 데이터 누락 문제는 속도가 원인이 아니었지만  
batchUpdate 메소드를 사용함으로써 속도를 개선하였고,  
url 쿼리 방식에서 json으로 보내도록 직접 구현함으로써 누락 문제를 해결하였다.

```java
// without batchUpdate
jsonSaveEnvrmtSmplSheet execution time : 5692

// with batchUpdate
jsonSaveEnvrmtSmplSheet execution time : 4242
```

5천 건의 데이터를 기준으로 약 25퍼센트의 성능 개선을 했다.

## 총평

산학협력인턴십을 통해 실제 서비스의 성능 개선을 경험할 수 있었다.  
동일한 원인으로 인해 데이터 누락 문제가 발생하는 기존의 다른 서비스 또한  
이번 문제 해결 사례를 토대로 해결하였다.

인턴이지만 프로젝트에 직접적으로 기여할 수 있는 기회를 얻어 감사했고,  
이번 경험으로 개발자로써 더욱 성장할 수 있었다.