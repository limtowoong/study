# Long과 long 차이

Long은 null 사용 가능

<br>

long은 null 사용 불가능

<br>

# Integer 

Integer은 null 사용 가능

<br>

int는 null 사용 불가능

<br>

# 이유

int와 long은 기본형(Primitive Type) 변수다.

기본형 변수가 뭐지?

기본형 변수는 값을 저장하는 공간이다. 즉, 실제 값이 저장된다.

그래서 기본형 변수는 값이 없으면 0을 반환하기 때문에 null이 올 수 없다.

그럼 Integer와 Long은 왜 null이 올 수 있는거냐?

Integer와 Long은 참조형(Reference Type) 변수이기 때문이다.

참조형 변수가 뭐냐?

참조형 변수도 기본형과 똑같이 값을 저장한다. 하지만 참조형은 실제 값이 아닌 주소 값을 저장한다.

주소? 우리가 생각하는 https:// 이런걸 말하는건가? 라고 생각하겠지만 아니다.

정확히는 메모리 주소이다.

메모리 주소를 이해하기 위해서는 Stack 영역과 Heap 영역에 대해 알아야한다.

기본형 변수는 Stack 영역에서 실제 값을 그대로 저장한다.

반면, 참조형 변수는 Stack 영역에 공간을 생성하고 Heap 영역에도 공간을 생선해서 실제 값을 저장한다.

Heap 영역에 생성한 공간에서 실제 값을 저장하고 그 공간(Heap 영역)의 주소 값을 불러와서 Stack 공간에 저장한다. 
