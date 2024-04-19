# 예외 처리
프로그램을 만들다 보면 수많은 예외 상황이 발생한다. 이러한 예외 상황은 자바에서 오작동이 일어나지 않게 하기 위한 배려이다. 하지만 예외 상황을 원하지 않아 무시하거나 처리하고 싶은 경우가 있을 것이다. 이러한 상황을 위해 try ~ catch, throws 구문을 이용해 예외 상황을 처리할 수 있다.

<br>

## 예외 발생 원인

예외 처리를 알아보기 전에 먼저 어떤 상황에서 예외가 발생하는 이유를 살펴보자.

<br>

### 지정된 파일을 찾을 수 없음 ( FileNotFoundException )
```java
import java.io.*;

public class Test {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new FileReader("파일"));
        br.readLine();
        br.close();
    }
}
```

* 위 코드는 '파일'이라는 이름에 파일을 찾는 코드이다.

```java
Exception in thread "main" java.io.FileNotFoundException: 파일 (지정된 파일을 찾을 수 없습니다)
	at java.base/java.io.FileInputStream.open0(Native Method)
	at java.base/java.io.FileInputStream.open(FileInputStream.java:216)
	at java.base/java.io.FileInputStream.<init>(FileInputStream.java:157)
	at java.base/java.io.FileInputStream.<init>(FileInputStream.java:111)
	at java.base/java.io.FileReader.<init>(FileReader.java:60)
	at Test/pack.Test.main(Test.java:7)
```

* 실행하면 `FileNotFoundException` 예외가 발생하게 된다.

<br>

### 배열 인덱스를 벗어나는 상황 ( ArrayIndexOutOfBoundsException )

```java
public class Test {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3};
        System.out.println(arr[3]);
    }
}
```

* 이 예외는 우리가 배열을 출력할 때 많이 발생하는 예외 중 하나이다.

```java
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 3 out of bounds for length 3
	at Test/pack.Test.main(Test.java:6)
```

* 배열은 0번부터 시작하기 때문에 arr[3]는 a배열 4번째를 뜻한다. 그래서 3번째까지 밖에 없는 배열을 4번째까지 출력할려고 하였기 때문에 `ArrayIndexOutOfBoundsExcept` 예외가 발생하게 된다.

<br>

### 나누기 연산에서 0으로 나누는 경우 ( ArithmeticException )

```java
public class Main {
    public static void main(String[] args) {
        int x = 10;
        int y = 0;
        System.out.println(x / y);
    }
}
```

* 10에서 0은 나눠지지 않는다 그렇기에 다음과 같은 오류가 발생한다.

```java
Exception in thread "main" java.lang.ArithmeticException: / by zero
	at Test/pack.Test.main(Test.java:7)
```

* 이 처럼 `ArithmeticException` 예외가 발생한다.

<br>

### 잘못된 형변환 ( ClassCastException )

```java
public class Test {
    public static void main(String[] args) {
        Object obj = "오브젝트";
        Integer num = (Integer) obj;
    }
}
```

* 다음과 같이 Object에는 '오브젝트'라는 문자열이 들어가 있다. 하지만 Integer(숫자) 형식으로 형변환을 하였기 때문에 다음과 같은 오류가 발생한다.

```java
Exception in thread "main" java.lang.ClassCastException: class java.lang.String cannot be cast to class java.lang.Integer (java.lang.String and java.lang.Integer are in module java.base of loader 'bootstrap')
	at Test/pack.Test.main(Test.java:6)
```
* 형변환에 실패하여 `ClassCastException` 예외가 발생한다.

<br>

### Null 포인터 참조 ( NullPointerException )

```java
public class Test {
    public static void main(String[] args) {
        String str = null;
        System.out.println(str.length());
    }
}
```

* str에 문자열을 넣지 않았기 때문에 length()를 사용할 수 없다.

```java
Exception in thread "main" java.lang.NullPointerException: Cannot invoke "String.length()" because "str" is null
	at Test/pack.Test.main(Test.java:6)
```

* `NullPointerException` 예외가 발생한다.

<br>

## try ~ catch문

이제 예외들을 처리하기 위해 try ~ catch문을 사용해 보자.

```java
try {
	//실행 코드
} catch (예외 1) {
	//예외 처리 문장
} catch (예외 2) {
	//예외 처리 문장
}
```

* try문 안의 수행할 문장 중에서 예외가 발생하지 않는다면 catch문에 속한 문장들은 수행되지 않는다. 하지만 try문 안의 문장을 수행하는 도중에 예외가 발생하면 예외에 해당되는 catch문이 수행된다.

```java
public class Test {
	public static void main(String[] args) {
		int x = 10;
		int y = 0;

		try {
			System.out.println(x / y);
		} catch (ArithmeticException e) {
			System.out.println(e.getMessage());
			e.printStackTrace();
		}
	}
}
```
ArithmeticException 예외가 발생하면 예외 메시지와 스택 트레이스 즉, 예외가 발생한 위치와 관련된 자세한 정보를 출력합니다.

<br>

## finally

프로그램 수행 도중 예외가 발생하면 프로그램이 중단되거나 catch문으로 넘어간다. 이때 예외가 발생해도 반드시 실행되어야 하는 부분이 있다면 finally를 사용하면 된다.

다음 예제를 보며 설명하겠다.
```java
public class Test {
	public static void main(String[] args) {
		int x = 10;
		int y = 0;

		try {
			System.out.println("1");
			System.out.println(x / y);    // 예외 발생
			System.out.println("2");      // 실행 X
		} catch (ArithmeticException e) {
			System.out.println(e.getMessage());
			e.printStackTrace();
		}
	}
}
```
위 예제에서 try문이 실행되면 '1'이 출력되고 그다음에 예외가 발생한다. 그럼 자연스럽게 다음 코드가 실행되지 않기 때문에 '2'는 출력되지 않는다. 그럼 만약 여기서 '2'를 출력하고 싶으면 어떻게 해야할까?

다음 예제를 보도록 하자.
```java
public class Test {
	public static void main(String[] args) {
		int x = 10;
		int y = 0;

		try {
			System.out.println("1");
			System.out.println(x / y);
		} catch (ArithmeticException e) {
			System.out.println(e.getMessage());
			e.printStackTrace();
		} finally {
			System.out.println("2");
		}
	}
}
```
finally 구문은 try문에 실행 여부와 상관없이 무조건 실행된다. 그래서 위 예제가 실해되면 '1' -> (예외 발생) -> '2' 순으로 출력될 것이다.

<br>

## 예외 활용

예외를 직접 만들어보고 어떻게 활용할 수 있는지 알아보자.

<br>

```java
public class Test {
	public void setGender(String gender) {
		if("남자".equals(gender)) {
			return;
		}
		System.out.println("당신의 성별은 "+ gender +" 입니다.");
	}

	public static void main(String[] args) {
		Test test = new Test();
		test.setGender("남자");
	}
}
```
* 위 예제는 setGender 메서드에서 '남자'라는 문자열이 입력되면 return으로 메서드를 종료해 성별을 출력하는 문장이 실행되지 않도록 한다.

<br>

## RuntimeException

이제 '남자'라는 문자열이 입력되면 예외가 발생하도록 해보겠다.

<br>

```java
class GenderException extends RuntimeException {
}

public class Test {
	public void setGender(String gender) {
		if("남자".equals(gender)) {
			throw new GenderException();
		}
		System.out.println("당신의 성별은 "+ gender +" 입니다.");
	}

	public static void main(String[] args) {
		Test test = new Test();
		test.setGender("남자");
	}
}
```
단순히 return 부분을 `throw new GenderException();`로 변경해주고 `class GenderException extends RuntimeException`을 추가하면 예외를 발생시킬 수 있다.

그럼 이번에는 Exception에 대해 배워보도록 하자.

<br>

## Exception

```java
class GenderException extends Exception {
}

public class Test {
	public void setGender(String gender) {
		if("남자".equals(gender)) {
			throw new GenderException();
		}
		System.out.println("당신의 성별은 "+ gender +" 입니다.");
	}

	public static void main(String[] args) {
		Test test = new Test();
		test.setGender("남자");
	}
}
```

일단 `class GenderException extends RuntimeException`에서 `class GenderException extends Exception`으로 변경해보자 그럼 결과는 컴파일 오류가 발생할 것이다.

Why? 그건 RuntimeException과 Exception에 차이를 알아야 한다.

RuntimeException은 예외 처리를 안 해도 되는 반면, Exception은 예외 처리를 필수적으로 해야 하는데 이건 컴파일러에서 강제적으로 요구하기 때문이다. 그리고 RuntimeException은 예측 불가능한 예외라는 뜻으로 Unchecked Exception라고 불리며, Exception은 예측 가능한 예외라는 뜻으로 Checked Exception라고 불린다.

그럼 Exception에 예외 처리를 어떻게 해야되냐?

다음 예제를 보도록 하자.

```java
class GenderException extends Exception {
}

public class Test {
	public void setGender(String gender) {
		try {
			if("남자".equals(gender)) {
				throw new GenderException();
			}
			System.out.println("당신의 성별은 "+ gender +" 입니다.");
		} catch (Exception e) {
			System.out.println("예외 발생");
		}
	}

	public static void main(String[] args) {
		Test test = new Test();
		test.setGender("남자");
	}
}
```
위 예제처럼 try ~ catch문을 통해 GenderException 예외를 처리할 수 있다.

<br>

## 예외 던지기

앞 예제처럼 try ~ catch를 사용하여 setGender 메서드에서 예외 발생과 예외 처리를 다 처리할 수 있지만 throws 구문을 사용하여 main 메서드에서 예외를 처리할 수 도 있다.

```java
class GenderException extends Exception{
}

public class Test {
	public void setGender(String gender) throws GenderException {
		//try {
			if("남자".equals(gender)) {
				throw new GenderException();
			}
			System.out.println("당신의 성별은 "+ gender +" 입니다.");
		//} catch (Exception e) {
		//	System.out.println("예외 발생");
		//}
	}

	public static void main(String[] args) {
		Test test = new Test();
		test.setGender("남자");
	}
}
```
일단 throws 구문을 쓰고 try ~ catch 문을 주석처리 해봤다.

이러면 당연하게도 컴파일 오류가 뜬다.

```java
class GenderException extends Exception{
}

public class Test {
	public void setGender(String gender) throws GenderException {
		if("남자".equals(gender)) {
			throw new GenderException();
		}
		System.out.println("당신의 성별은 "+ gender +" 입니다.");
	}

	public static void main(String[] args) {
		Test test = new Test();
		try {
			test.setGender("남자");
		} catch (Exception e) {
			System.out.println("예외 발생");
		}
	}
}
```

위 예제는 main 메서드에 try ~ catch 문을 사용하여 예외 처리를 하였다.

결과는 '예외 발생'이 출력되었다.

그럼 여기서 의문점이 생긴다 굳이 throws를 써서 main 메서드에서 예외를 처리할 필요가 있을까?

그 이유를 지금부터 설명할 것이다.

```java
class GenderException extends Exception {
}

public class Test {
	public void setGender(String gender) {
		try {
			if("남자".equals(gender)) {
				throw new GenderException();
			}
			System.out.println("당신의 성별은 "+ gender +" 입니다.");
		} catch (Exception e) {
			System.out.println("예외 발생");
		}
	}

	public static void main(String[] args) {
		Test test = new Test();
		test.setGender("남자");
		test.setGender("여자");
	}
}
```

위 예제는 try ~ catch 문만을 사용하여 작성한 코드이다.

```java
예외 발생
당신의 성별은 여자 입니다.
```

결과를 보면 남자, 여자 문자열 모두 실행되었다.

```java
class GenderException extends Exception {
}

public class Test {
	public void setGender(String gender) throws GenderException {
		if("남자".equals(gender)) {
			throw new GenderException();
		}
		System.out.println("당신의 성별은 "+ gender +" 입니다.");
	}

	public static void main(String[] args) {
		Test test = new Test();
		try {
			test.setGender("남자");
			test.setGender("여자");
		} catch (GenderException e) {
			System.out.println("예외 발생");
		}
	}
}
```

위 예제는 throws를 사용한 코드이다.

```
예외 발생
```

결과는 남자 문자열만 실행되었다.

위 결과를 보면 예외 처리를 어느 부분에서 하느냐에 따라 결과가 달라진다. 그렇므로 throws는 상황에 알맞게 쓰는게 맞는 것 같다.

추가적으로 throw와 throws에 대해 좀 더 설명하겠다.

## throw & throws

thorw는 개발자가 의도적으로 예외를 발생시키므로써 예외가 발생할 수 있는 코드가 있다는 것을 알려준다.

throws는 지금 위치한 메서드가 아닌 다른 메서드 또는 상위 메서드에서 예외 처리를 하도록 예외를 던지는 것이다.

```java
class ExceptionClass extends Exception {
}

public class Example {
	public void methodA() {
		try {
			methodB();
		} catch (Exception e) {
			System.out.println("메서드 B에서 예외가 발생했습니다.");
		}
	}
	
	public void methodB() throws ExceptionClass{
		throw new ExceptionClass();
	}

	public static void main(String[] args) {
		Example ex = new Example();
		ex.methodA();
	}
}
```
위 예제는 다른 메서드에 예제를 던져서 처리하는 방식이다.

```java
class ExceptionClass extends Exception {
}

public class Example {
	public void methodA() throws ExceptionClass {
		throw new ExceptionClass();
	}
	
	public static void main(String[] args) {
		Example ex = new Example();
		try {
			ex.methodA();
		} catch (Exception e) {
			System.out.println("메서드 B에서 예외가 발생했습니다.");
		}
	}
}
```
위 예제는 상위 메서드에 예외를 던져서 처리하는 방식이다.
