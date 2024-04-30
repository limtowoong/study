### @RequiredArgsConstructor

```java
@Service
@RequiredArgsConstructor
public class PostService {

	private final PostMapper postMapper;

}
```

* @RequiredArgsConstructor는 final로 선언된 모든 멤버에 대한 생성자를 만들어준다.

```java
@Service
public class PostService {
	private final PostMapper postMapper;

	public PostService(PostMapper postMapper){
		this.postMapper = postMapper;
	}

}
```

