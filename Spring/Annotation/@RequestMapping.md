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
