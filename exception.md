# 예외 처리
프로그램을 만들다 보면 수많은 예외 상황이 발생한다. 이러한 예외 상황은 자바에서 오작동이 일어나지 않게 하기 위한 배려이다. 하지만 예외 상황을 원하지 않아 무시하거나 처리하고 싶은 경우가 있을 것이다. 이러한 상황을 위해 `try ~ catch`, `throws` 구문을 이용해 예외 상황을 처리할 수 있다.

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
* 실행하면 `FileNotFoundException`라는 예외가 발생하게 된다.

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
* 배열은 0번부터 시작하기 때문에 arr[3]는 a배열 4번째를 뜻한다. 그래서 3번째까지 밖에 없는 배열을 4번째까지 출력할려고 하였기 때문에 `ArrayIndexOutOfBoundsExcept`라는 예외가 발생하게 된다.

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
* 이 처럼 `ArithmeticException`라는 예외가 발생한다.

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
* 다음과 같이 `Object`에는 "오브젝트"라는 문자열이 들어가 있다. 하지만 `Integer`(숫자) 형식으로 형변환을 하였기 때문에 다음과 같은 오류가 발생한다.
```java
Exception in thread "main" java.lang.ClassCastException: class java.lang.String cannot be cast to class java.lang.Integer (java.lang.String and java.lang.Integer are in module java.base of loader 'bootstrap')
	at Test/pack.Test.main(Test.java:6)
```
* 형변환에 실패하여 `ClassCastException`라는 예외가 발생한다.

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
* str에 문자열을 할당하지 않았기 때문에 `length()` 메서드를 호출할 수 없다.
```java
Exception in thread "main" java.lang.NullPointerException: Cannot invoke "String.length()" because "str" is null
	at Test/pack.Test.main(Test.java:6)
```
* `NullPointerException`라는 예외가 발생한다.

<br>

## try ~ catch문
이제 예외들을 처리하기 위해 `try ~ catch`문을 사용해 보자.
```java
try {
	//실행 코드
} catch (예외 1) {
	//예외 처리 문장
} catch (예외 2) {
	//예외 처리 문장
}
```
* try 문 안의 수행할 문장 중에서 예외가 발생하지 않는다면 catch문에 속한 문장들은 수행되지 않는다. 하지만 try문 안의 문장을 수행하는 도중에 예외가 발생하면 예외에 해당되는 catch문이 수행된다.

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
`ArithmeticException`이 발생하면 예외 메시지와 스택 트레이스 즉, 예외가 발생한 위치와 관련된 자세한 정보를 출력합니다.

<br>

## finally
프로그램 수행 도중 예외가 발생하면 프로그램이 중단되거나 catch문으로 넘어간다. 이때 예외가 발생해도 반드시 실행되어야 하는 부분이 있다면 'finally'를 사용하면 된다.

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
위 예제에서 try문이 실행되면 "1"이 출력되고 그다음에 예외가 발생한다. 그럼 자연스럽게 다음 코드가 실행되지 않기 때문에 "2"는 출력되지 않는다. 그럼 만약 여기서 "2"를 출력하고 싶으면 어떻게 해야할까?

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
finally 구문은 try문에 실행 여부와 상관없이 무조건 실행된다. 그래서 위 예제가 실해되면 "1" -> ( 예외 발생 ) -> "2" 순으로 출력될 것이다.






