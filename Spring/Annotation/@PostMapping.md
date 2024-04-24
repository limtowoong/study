### @PostMapping

```java
@PostMapping("/")
public String Example(Model model) {
}
```

* 클라이언트가 요청한 데이터를 서버에 전달할 때 사용된다.

<br>

@RequestMapping
```java
@RequestMapping(value = "/hello", method = RequestMethod.POST)
```

@PostMapping
```java
@PostMapping("/hello")
```

<br>

* @RequestMapping 방식보다 더 간결하게 코드를 작성할 수 있다.
