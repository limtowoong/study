### @Configuration

```java
@Configuration
public class AppConfig {

	@Bean
	public MyService myService() {
		return new MyServiceImpl();
	}

}
```

* XML 파일 대신 Java 클래스로 빈을 정의하고 구성할 때 사용된다.
