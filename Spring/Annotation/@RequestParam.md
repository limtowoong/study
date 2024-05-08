# @RequestParam 
querystring에서 매개변수 값을 가져오는데 사용된다. 

<br>

### Controller
```java
package com.example.demo.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class NewController {
	
	@GetMapping("hello-mvn")
	public String helloMvn(@RequestParam("name") String name, Model model) {
		model.addAttribute("name", name);
		return "helloMvn";
	}

}
```

### html + thymeleaf
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<p th:text="${name}"/>
</body>
</html>
```

### 결과

![image](https://github.com/limtowoong/study/assets/104752202/536a1832-1e4f-45b0-a63d-79e3afb3b82f)
