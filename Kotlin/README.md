# Kotlin

자바 가상 머신에서 돌아가는 JetBrains에서 만든 개발 언어<br>
코틀린을 컴파일 하면 JVM에서 돌아가는 Bytecode를 생성한다.

### Kotlin VS Java

1. 코틀린은 자바와 높은 상호 운영성을 가지고 있다.

- 안드로이드 API, JVM libs등을 그대로 사용하도 모든 Java 프레임 워크들을 사용할 수 있다.

2. 코틀린은 자바 보다 프로그램 안정성을 높일 수 있다.

- Java의 흔한 에러인 NULL Pointer Exception에서 자유롭다.

3. 코틀린은 자바보다 간결하다.
4. 코틀린은 컴파일 속도가 빠르다.

- 런타임 사이즈가 작다.

### 장점

실용성, 간결성, 안정성, 상호 운영성

1. Null 안정성

- 널값 허용 여부를 컴파일 단계에서 검사하므로 런타임에서 발생하는 오류를 줄일 수 있다.
- 세이프콜(?)을 통해서 null이 아닌 경우에만 함수에 접근할수 있다(name?.length)
- 자바에서도 @Nullable, @NotNull을 통해서 사용이 가능하다

2. 간결한 문법

- 세미콜런 없음, new 키워드가 없다, 타입 추론을 지원한다.

3. 가변/불변 지원

- var: 할당된 값을 런타임 시에 자유자재로 바꿀 수 있다.
- val: 값을 한번 할당하면 그 후에 변경할 수 없다(= Java.final)
- const: 컴파일시의 상수라는 의미, 컴파일 타임에 값을 할당해야 한다는
  - 즉, 함수나 어떤 클래스의 생성자에게도 할당 불가능, 오직 문자열이나 기본 자료형만 가능하다
- 리스트에서도 사용이 가능하다.
  - mutableListOf<Int>으로 사용하면 추가 삭제가 가능하다.
  - listO<Int>을 통해서 만들면 추가 삭제가 가능하다
  - 자바9에서 부터도 사용이 가능하다

4. 정적 타입 지정 언어

- 모든 프로그램 구성 요소의 타입을 컴파일 시점에서 알 수 있다.
- 프로그램 안에서 객체의 필드나 메소드를 사용할 때 마다 컴파일러가 타입을 검증해준다.
- VS 동적
  - 동적은 타입 관계 없이 넣을 수 있어서 메소드, 필드 접근 때 검증이 일어나서 시간이 더 빠르다
  - 반대로 이름을 잘못 입력하는 경우 실수도 컴파일시 걸러내지 못하고 실행 시점에서 오류가 발생한다.
- 장점
  - 성능: 실행 시점에 어떤 메소드를 호출할지 알아내는 과정이 필요 없어서 메소드 호출이 빠르다
  - 신뢰성: 컴파일러가 프로그램의 정확성을 검증하기 때문에 실행 시 프로그램이 오류로 중단될 가능성이 더 적어진다.
  - 유지 보수성: 코드에서 다루는 객체가 어떤 타입에 속하는지 알 수 있기 때문에 처음 보는 코드를 다룰 때도 더 쉽다.

5. 함수형 프로그래밍

- First-Class 함수: 함수를 일반값으로 다룰 수 있다.

  - 함수를 변수로 저장할 수 있고, 인자로 다른 함수에 전달할 수 있다
  - 함수에서 새로운 함수를 만들어서 반환할 수 있다.

- 불변성: 일단 만들어지고 나면 내부 상태가 절대로 바꾸지 않는다.
- 부수효과 없다: 입력이 같으면 항상 같은 출력을 내놓고 다른 객체 상태를 변경하지 않는다.
- 간결성: 더 강력한 추상화를 할 수 있고 코드 중복을 막을 수 있다.
- 다중 스레드에 대한 안정성: 불변 데이터 구조를 사용하고 순수 함수를 그 데이터 구조에 적용한다면<br>
  다중 스레드 환경에서 같은 데이터를 여러 스레드가 변경할 수 ㅇ없다

### 단점

1. 순수 자바 패키지보다 패키지 사이즈가 커진다.
2. 빌드 시간이 느리다.
3. 자바카 코틀린을 호출할 때 Optional처리 문제가 있다.

- 변수뒤에 ?이 없으면 non-null로 처리되어 exception 처리 된다.

4. 함수 파라미터는 var이 아니라 val이다?

### const val VS val

const val - 컴파일 시점에 할당이 된다 <br>
(소스코드를 작성하고 기계어 코드로 변환되어 실행 가능한 프로그램으로 편집) <br>
val - 런타임 시점에 할당이 된다.<br>
(컴파일 과정을 마친 프로그램이 사용자에 의해 실행되어 지며, 응용 프로그램이 동작되어지는 때) <br>
컴파일을 한 후에 런타임을 가진다.