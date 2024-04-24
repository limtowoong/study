# Annotation 이란?

* 클래스나 메서드에 추가하여 다양한 기능을 부여하는 역할을 한다.<br>
즉, 메타데이터(meta data: 데이터를 위한 데이터)라고 볼 수 있다.

<br>

* 어노테이션을 사용하면 코드량이 감소하여 유지보수와 가독성이 향상된다.

<br>

## Spring에서 주로 사용하는 Annotation

### @SpringBootApplication

```java
@SpringBootApplication
public class DemoApplication {

	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
	}
}
```

* 스프링 부트 애플리케이션을 더욱 쉽게 설정하고 구성할 수 있도록 도와준다. 즉, 개발자가 직접 세부 구성을 하지 않아도 된다.

<br>

### @Component

```java
@Component
public class MyComponent {
}
```

* 주로 스프링 컨테이너에 클래스를 빈으로 등록할 때 사용한다. 따라서 다른 클래스에서도 사용할 수 있게된다.

<br>

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

<br>

### @Bean

* 주로 메서드를 스프링 컨테이너에 빈으로 등록할 때 사용되며, @Configuration가 없으면 빈으로 등록되지 않는다.

<br>

### @Controller

```java
@Controller
public class Controller {

	@GetMapping("/")
	public String Example(Model model) {
	}

}
```

* 웹 요청을 처리할 때 사용되며, @RequestMapping 또는 @GetMapping, @PostMapping을 사용하여 url 요청을 처리한다.

<br>

### @RequestMapping

```java
@RequestMapping(value = "/", method=RequestMethod.GET)
public String Example(Model model){
}

@RequestMapping(value = "/", method=RequestMethod.POST)
public String Example(Model model){
}
```

* url 요청을 어떤 메서드에서 처리할지 결정할 때 사용한다.

<br>

### @PostMapping, @GetMapping

```java
@GetMapping("/")
public String Example(Model model) {
}

@PostMapping("/")
public String Example(Model model) {
}
```

* @RequestMapping 방식보다 더 간결하게 코드를 작성할 수 있으며, post는 보낼 때 get은 받을 때 사용한다.

<br>

### @Mapper

```java
@Mapper
public interface UserMapper {
	User getUserById(Long id);
	void insertUser(User user);
	void updateUser(User user);
	void deleteUser(Long id);
}
```

```xml
<mapper namespace="com.example.UserMapper">
	<select id="getUserById" resultType="com.example.User">
		SELECT * FROM users WHERE id = #{id}
	</select>

	<insert id="insertUser" parameterType="com.example.User">
		INSERT INTO users (username, email) VALUES (#{username}, #{email})
	</insert>

	<update id="updateUser" parameterType="com.example.User">
		UPDATE users SET username = #{username}, email = #{email} WHERE id = #{id}
	</update>

	<delete id="deleteUser" parameterType="Long">
		DELETE FROM users WHERE id = #{id}
	</delete>
</mapper>
```

* Mapper 인터페이스와 XML 파일을 연결하여 MyBatis가 SQL 쿼리를 실행하는 방법을 정의한다. 여기서 인터페이스는 SQL 쿼리를 호출하는 메서드이고, XML 파일은 이러한 메서드와 SQL 쿼리를 매핑한다.

<br>

```java
@Getter
@Setter
public class Request {

	private Long id;
	private String title;
	private String content;
	private String writer;
	
}
```

### @Getter

* 객체의 값을 읽어온다.

<br>

### @Setter

* 객체의 값을 변경한다.

<br>

### @Data

* Setter, Getter를 합친거다.

<br>

### @Service

* @Component와 같이 스프링 컨테이너에 클래스를 빈으로 등록한다. 하지만 @Component는 일반적인 클래스를 나타낸다면 @Service는 비즈니스 로직을 처리하는 클래스를 나타낸다.

<br>

```java
@Service
@RequiredArgsConstructor
public class PostService {

	private final PostMapper postMapper;

}
```

### @RequiredArgsConstructor

* 자동으로 final 필드를 생성하여 의존성 주입을 편리하게 처리한다.

<br>

@RequestParam


@RequestHeader

@RequestBody

@ResponseBody

@RestController

@Autowired

@Test

@SpringBootTest
