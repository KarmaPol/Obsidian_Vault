https://chanhuiseok.github.io/posts/algo-37/

### 맨 앞, 맨 끝 문자
- str.front()
- str.back()
### 숫자를 문자로, 문자를 숫자로
- to_string(number)
- stoi(str), stod(str), stof(str), stol(str)
### 유용한 함수들
- str.empty()
  비었는지 확인
- swap(str1, str2)
  문자열 교환
- str.clear()
  문자열 없애기
- str1.append(str2)
  문자열 더하기
- str.find(str2)
  문자열 찾고 인덱스 반환
- str.substr(3, 2)
  문자열 3번째 인덱스부터 길이 2만큼 반환
- str.substr(3)
  문자열 3번째 인덱스부터 끝까지 반환
- str.replace(idx, len, str2)
  문자열 특정 인덱스부터 일정 길이 만큼 str2로 변경
- str.replace(str.begin()+1, str.begin()+3, str2)
  1번째 인덱스부터 3번째 인덱스 직전까지 str2로 변경
