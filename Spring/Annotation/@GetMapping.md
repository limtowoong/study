### @GetMapping

```java
@GetMapping("/")
public String Example(Model model) {
}
```

* 서버에게 데이터를 요청할 때 사용한다.

<br>

@RequestMapping
```java
@RequestMapping(value = "/hello", method = RequestMethod.GET)
```

@GetMapping
```java
@GetMapping("/hello")
```

<br>

* @RequestMapping 방식보다 더 간결하게 코드를 작성할 수 있다.
