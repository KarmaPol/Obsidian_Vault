https://blog.junu.dev/37

### 코틀린 OPEN, NOARG
코틀린은 기본이 Final -> jpa 리플렉션 위해 open 붙여줘야함
open 키워드, 기본 생성자 생성을 플러그인으로 지원
```yml
plugins {
	id "org.jetbrains.kotlin.plugin.jpa" version "1.3.61"
}

allOpen { annotation("javax.persistence.Entity") annotation("javax.persistence.MappedSuperclass") annotation("javax.persistence.Embeddable") }
```

