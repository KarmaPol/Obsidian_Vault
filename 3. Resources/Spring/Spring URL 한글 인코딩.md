https://www.google.com?q=카프카
-> Url 쿼리에 한글이 있을때, 리다이렉트 헤더에 올라가지 않는 문제 발생
```java
The Unicode character [카] at code point [52,852] cannot be encoded as it is outside the permitted range of 0 to 255
```

=> 아스키 코드로 변경해 해결
```java
URI uri = new URI(originalUrl);  
String encodedUrl = uri.toASCIIString();
```
