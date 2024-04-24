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
