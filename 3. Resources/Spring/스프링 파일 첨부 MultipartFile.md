```java
@PostMapping("/upload")
public String saveFile(@RequestParam MultipartFile file) {
	if (!file.isEmpty()) {
		String fullpath = file.getOriginalFilename();
		file.transferTo(new File(fullPath)); // 실제 파일로 저장
	}
	...
}
```
### 주요 메서드
- file.getOriginalFilename() 파일 명 참조
- file.transferTo() 실제 파일로 저장
### application 설정
```properties
spring.servlet.multipart.max-file-size=1MB
spring.servlet.multipart.max-request-size=10MB
```