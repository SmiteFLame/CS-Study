# JAVA

객체지향 언어, 이식성 높은 언어, 인터프린터 언어

- 객체: 소프트웨어 세계에 구현할 대상
- 클래스: 객체를 만들어내기 위한 설계도 혹은 툴
  - 연관되어 있는 변수와 메서드의 집합
- 인스탄스: 설계도를 바탕으로 소프트웨어 세계에 구현된 구체적인 실체 -객체를 소프트웨어에 실체화 하면 '인스턴스'이다

### JAVA의 특징

1. 자바는 객체 지향 언어이다.
2. JVM위에서 실행되기 때문에, 플랫폼에 의존하지 않고 실행 가능
3. 고성능, 바이트 코드로 변환 가능
4. 멀티 스레딩 가능

## 자바 구성 요소

### 자바 컴파일러

- 자바를 가지고 작성한 자바소스 코드를 자바 가상 머신이 이해할 수 있는 자바 바이크 코드로 변환한다.
- 자바 컴파일러는 자바를 설치하면 javac.exe라는 실행 파일형태로 설치된다.

### 자바 바이트 코드

- 자바 가상머신이 이해할 수 있는 언어로 변환된 자바 소스코드를 의미한다.
- 자바 컴파일러에 의해 변환되는 코드의 명령어 크기가 1바이트이다.
- 자바 바이트 코드는 자바 가상머신만 설치 되어 있으면, 어느 OS에서도 사용 가능하다.
-

### JVM

자바 가상머신으로 자바 애플리케이션을 클래스 로더를 통해 읽고 자바 API를 실행<br>
JAVA와 OS 사이의 중개자 역할을 하면서 JAVA는 OS에 구애받지 않고 재사용을 가능하게 해준다.

1. Interpreter

- 자바 컴파일러에 의해 변환된 자바 바이트 코드를 읽고 해석하는 역할

2. Class Loader

- 동적으로 클래스를 읽어오므로, 프로그램이 실행중인 런타임에서야 모든 코드 자바 가상 머신과 연결
- 동적으로 클래스를 로딩해주는 역할

3. Just-In-Time Compiler

- 프로그램이 실행 중인 런타임에 실제 기계어로 변환해주는 컴파일러를 의미한다.
- 즉, 자바 컴파일러가 생성한 자바 바이트 코드를 런타임에 바로 기계어로 변환하는데 사용한다.
  (기계어 - CPU가 직접 해독하고 실행할 수 있는 비트 단위로 쓰인 컴퓨터 언어, 프로그램을 나타내는 가장 낮은 단게의 개념)

4. Garbarge Collector

- 더 이상 사용하지 않는 메모리를 자동으로 회수해서 제거하는 역할

### JAVA의 메모리 영역

1. Class Area = Method Area = Static Area<br>

- JVM에 가장 먼저 처음 메모리 공간, 클래스와 Static을 올린다(클래스 로딩)

2. Stack Area <br>

- 지역변수와 매개변수가 저장된다. <br>
- 메소드 호출이 끝나면 모든 변수가 스택에서 제거

3. Heap Area <br>

- new 명령을 통해 생성된 인스턴스 변수가 놓인다. <br>
- 더 이상 호출하는 것이 없어질 때까지 존재한다 <br>

- 참조 변수에 저장되는 메모리 주소는 Stack에 저장
- 그 주소가 가르키는 메모리는 모드 Heap에 저장

4. PC Register

- Thread가 생성될 떄 마다 생성되는 Pragram Counter<br>
- 현재 스레드가 실행되는 부분의 주소와 명령을 저장하고 잇는 영역

5. Native Method Stack

- 자바 외 언어로 작성된 네이티브 코드를 위한 메모리 영역

- 스레드 생성시 Method, Heap영역은 모든 스레드가 공유한다.

<br>
메모리 관리, GC을 수행하나는 스택 기반의 가상 머신이다.

클래스 로더 - 클래스를 처음으로 참조할 때 해당 클래스를 로드하고 링크한다.

<hr>

## JAVA의 종류

### JAVA JDK(Java Development Kit)

JAVA로 된 언어를 컴파일 하고 개발 할 수 있도록 해주는 개발 환경의 세트 <br>
개발자만을 위한 컴파일러, 디버깅 툴들을 제공 <br>
JAVA SE, JAVA EE, JRE, JVM을 통합 <br>

### JAVA SE

- 스탠다드 에디션으로 가장 많이 사용되는 기본 JAVA로써 표준 문법을 의미한다.

### JAVA EE

- SE 기반으로 서버측을 개발하기 위해서 EJB, JSP, Servlet을 지원해준다

### JAVA ME

- 제한된 자원을 휴대폰, 셋텁박스등 임베디드 시스템에서 자바로 프로그램 개발할 때 이용한다.

## Generices

- 제네릭은 클래스 내부에서 사용할 데이터 타입을 외부에서 지정하는 기법
- 따로 형 변환이 필요 없고 발생하지 않기 때문에 유용하게 사용 가능

```java
public class Box<T>{
    private T t;
    public T getT(){
        return t;
    }
}

public Util{
    public static <T> Box<T> boxing(T t){
        Box<T> box = new Box<T>();
        box.setT(t);
        return box;
    }
}

// 구체적 타입을 명시하는 호출 방법
Box<Integer> box1 = new Util.<Integer>boxing(100);
// 암묵적 호출 방법
Box<Integer> box2 = new Util.boxing("암묵적호출");
```

## 자바 배열 크기 변경

1. Arrays.CopyOf(기존 배열, 새로운 배열 크기)
2. 배열을 List

## Boxing vs Unboxing

1. 기본 타입(Primitive Type) - char, int, float, double....
2. 참조 타입(Reference Type) - class, interface <br>
   Wrapper Class - 기본 타입을 객체로 다루기 위해서 사용하는 것 <br>
   EX) Byte(byte), Integer(int)....

Boxing - 기본타입을 Wrapper Class로 변경
Unboxing - Wrapper Class를 기본 타입으로 변경

### 자바 클래스 멤버 변수 초기화 순서

1. Static 변수 선언부 - 클래스가 로드 될 때 변수가 가장 먼저 초기화
2. 필드 변수 선언부 - 객체가 생성될 때 heap 메모리에 올라가고 생성자 block보다 앞서 초기화
3. 생성자 block - 객체가 생성될 때 heap 메모리에 올라간다.
4. 필드 변수 초기화 - JVM에서 내부적으로 로킹

### Serializable

자바 시스템 내부에서 상속되는 Object또는 JVM의 메모리에 상주 되어 있는 Data를 외부 자바 시스템에서도 사용할 수 있도록 Byte형태로 데이터를 변환하는 기술 <br>
이 값들을 주소값을 가지고 있지 않고 실제 값 형식으로 바꿔주면서 데이터 간 정보 통신 가능

<hr>

## 상속

```java
(A는 최상위)
A - a(int i){};
B - b(){};
C - a(){}, b(int i){} - a,b는 오버로딩(파라미터가 다르다)
D - a(int i){}, b() - a,b는 오버라이딩(a는 A, b는 B를 오버라이딩)
E - a(){}, b(){} - a,b는 오버라이딩(a는 C, b는 D를 오버라이딩)

A(호출범위) a = new ? -> a(int i)만 호출 할 수 있다.
B b = -> a(int i)와 b()만 호출 할 수 있다.

A x = new C(); -> 객체는 생성 가능
x.a(); -> 오류 발생(A의 범위에서는 a()를 호출 할 수 없다)

C x = new E();
x.b(3); ->  C에 있는 b(int i)가 실행

D x = new B(); -> 생성에서 오류가 발생
x.b();

B x = new D();
x.a(3);
1. A에서 a(int i)가 있으니 호출이 가능
2. D에서 재정의 되어 있으므로 D(int i)가 호출이 된다.
```

## Garbage Collection

- 프로그램에서 유효하지 않는 메모리를 JVM에서 알아서 정리해주는 것
- 메모리 관리 기법으로 동적으로 할당 했던 영역중에서 필요 없는 부분 해제
- 동적 할당된 메모리 영역 가운데 어떤 변수도 가리키지 않는 메모리 영역 탐지하여 해제

### GC가 일어나는 타이밍

각 영역의 할당된 크기의 메모리가 허용치를 넘을 떄 수행한다, 개발자가 컨트롤할 영역이 아니다

### GC 영역

JAVA의 Heap 영역

1. 대부분의 객체는 금방 접근 불가능한 상태가 된다.
2. 오래된 객체에서 새로운 객체로의 참조는 아주 적게 존재한다.

- 객체는 대부분 일회성이며, 메모리에 오래 동안 남아 있는 경우는 드물다

생존기간에 따라서 물리적인 Heap 영역을 나눈다.

1. Young 영역

- 새롭게 생성된 객체가 핼당되는 영역
- 대부분의 객체가 금방 Unreachable 상태가 되기 때문에, 많은 객체가 Young 영역에 생성되었다가 사라진다.
- Young 영역에 대한 Garbage Collection은 Minor GC라고 부른다

2. Old 영역

- Young 영역에서 Reachable 상태를 유지하여 살아남은 객체가 복사되는 영역
- 복사되는 과정에서 대부분 Young 영역보다 크게 할당되며, 크기가 큰 만큼 가비지는 적게 발생한다.
- Old 영역에 대한 Garbage Collection은 Major GC 또는 Full GC라고 부른다

### 동작 원리

공통 동작 원리

1. Stop The World

- JVM이 애플리케이션의 실행을 멈추는 작업이다.
- GC를 실행하는 쓰레드를 제외하고 모든 쓰레드들의 작업이 중단된다.

2. Mark and Sweep

- Mark: 사용되는 메모리와 사용되지 않는 메모리를 식별하는 작업
- Sweep: Mark 단계에서 사용되지 않음으로 식별된 메모리를 해제하는 작업

Minor GC

- Young 영역은 1개의 Eden 영역과 2개의 Survivor 영역으로 나눠진다.
  - Eden: 새로 생성된 객체가 할당되는 영역
  - Survivor: 최소 1번의 GC 이상 살아남은 객체가 존재하는 영역
- Eden 영역이 꽉차게 된다면 Minor GC가 발생
- 사용중인 객체는 Survivor 영역으로 옮겨 지게 된다
- 이때 한개의 Survivor에만 데이터가 존재하고 나머지는 빈 상태가 된다.
- 이러한 과정을 반복해서 계속 살아남은 객체는 Old 영역으로 이동한다.

- bunp the Pointer: Eden 영역에 마지막으로 할당된 객체으 주소를 캐싱해두는 것
- TLAVs: 각각의 쓰레드마 Edne 영역에 객체를 할당하기 위한 주소를 부여함으로써 동기화 작업 없이 빠르게 메모리를 할당하는 기술

Major GC

- 객체들이 계속 Promotion되어 Old 영역의 메모리가 부족해지면 발생한다.

### 장점

1. 프로그래머가 동적으로 할당한 메모리 영역 전체를 관리 안해도 된다.
2. 버그가 감소한다.
   1. 유효하지 않는 포인터 접근 - 이미 동적 할당된 메모리를 해제한 영역에 접근하게 되는 버그
   2. 이중 해제 - 이미 해제된 메모리를 또 다시 해제하는 오류 감소
   3. 메모리 누수 - 더이상 사용하지 않는 메모리를 해제하지 않고 남겨진 것이 쌓으면 메모리 누수 발생 가능

### 단점

1. 어떤 메모리를 해제해야할 지 결정하는데 사용되는 알고리즘에 의해 비용 증가
2. 객체가 필요 없는 시점을 알고 있는 경우에도 GC 알고리즘이 메모리 해제 비용 추적해야됨
3. 실시간 서비스에는 적합하지 않다(GC행동 타이밍, 점유시간 예측 불가능)

### GC 알고리즘

1. Default GC

- Minor GC는 Copy & Scavenge, Full GC는 Mark & Compact 알고리즘 사용
- 위에서 설명했던 방식

2. Parallel GC

- 스레드 수를 지정하고여러 스레드들 동시에 이용해 GC를 수행하는 방법

1. Low - pause: GC 속도보다 순간적으로 애플리케이션 동작이 중단되는 형상을 최소화
2. Throughput: Minor GC의 신속한 수행에 초점을 맞춘 방식
3. Concurrent GC: Low-pause와 비슷한 방식으로 애플리케이션이 돌아가는 단게에서 GC 수행
4. Incremental GC(Train GC): Minor GC 일어날 때마다 Old GC 영역의 GC를 조금씩 수행해 Full GC의 발생 횟수를 감소

<hr>

## 추상클래스 VS 인터페이스

### 추상클래스

1. Default 생성자를 가진다(서브 클래스가 인스턴스화될 때 호출함)
2. 추상 메소드, 비 추상 메소드를 포함 할 수 있다.
3. 상속한 클래스는 모든 메소드를 구현할 필요가 없다.
4. 객체 생성이 불가하므로 extend로 구현

### 인터페이스

1. 생성자를 가지지 않는다.
2. 추상 메소드만 선언할 수 있다.
3. 인터페이스를 구현하는 클래스는 모든 메서드를 구현해야 한다.
4. 객체 생성이 불가하므로 implement로 구현

### 인터페이스를 사용하는 이유

유연성: 완전한 요구사항이 도출되지 않은 상태에서 빠르게 개발하면서 지속적으로 새로운 요구사항과 변경사항을 적용하는 방식

- 상속을 받은 하위 클래스에서는 부모 클래스의 메서드를 오버라이딩시켜서 다형성을 가능하게 한다

<hr>

## JDBC

- 자바에서 데이터베이스를 접속할 수 있도록 하는 자바 API
- 데이터 베이스에 자료를 쿼리문을 작성하거나 업데이트 하는 방법을 제공하고 있다
- JDBC가 없으면 데이터베이스 종류마다 각각의 SQL문을 사용해야 했다

- JAVA 코드로 DB 서버에 접속
- SQL문을 구성하고 DB서버에서 실행
- DB서버에서 처리한 결과를 가져오기
- DB의 정보를 가져오기

- 간단한 코드도 중복으로 사용되는 경우가 많다
- Connection와 같은 리소스를 제대로 릴리즈 하지 않으면 시스템의 오류가 나는 경우가 있다

### JDBC 동작 순서

1. DriverManager를 통해서 Connection 인스턴스를 얻는다

- Connection: 데이터베이스와 연결하는 객체

2. Connection을 통해서 Statement를 얻는다

- Statemennt: SQL 구문을 실행하는 역할
- 스스로 SQL 구문을 이해하지 않지만 SQL 관리를 한다

3. Statement를 이용해 ResultSet을 얻는다

- ResultSet: 결과값을 저장할 수 있다
  - 저장된 값을 한 행 단위로 타입을 지정해서 가져올 수 있다

### Web Server VS WAS Server

Web - HTML, CSS, JS등 정적인 데이터를 처리하는 웹 서버
WAS - JSP, ASP, PHP등 사용자의 ㅇ비력을 받아 서버에서 처리하는 동적인 서버

사용자 처리 -> WEB 서버 -> WAS 동적 처리 -> WEB 서버 -> 사용자 응답 메시지

<hr>

## 에러 VS 예외

에러 - 시스템에 비정상적인 상황이 생겼을 때 발생

- 시스템 레벨에서 발생하기 때문에 심각한 수준
- 개발자가 미리 예측하여 처리 불가능 하기 때문에 오류에 대한 처리를 신경 안써도 된다.

예외 - 개발자가 구현한 로직에서 발생

- 발생할 상황을 미리 예측하여 처리할 수 잇다.
- 개발자가 처리할 수 있는 곳에 구분하고 처리 방법을 명확히 알고 적용 해야 한다.

<hr>

## Collection

### List vs Set vs Map

List - 순서가 있는 데이터의 집합으로 데이터의 중복을 허용 <br>
Set - 순서를 유지하지 않는 데이터의 집합으로 데이터의 중복을 허용하지 않음<br>
Map - 키와 값의 상으로 이루어진 데이터의 집합, 키는 중복X, 값은 중복O<br>

### ArrayList vs LinkedList

ArrayList - 배열이 동적으로 늘어나는 것이 아니라 꽉 차게 되면 더 큰 용량의 배열을 만들어서 옮기는 작업을 한다.

- 초기 용량을 설정하는 것이 좋다.
- 읽는 시간이 빠르지만, 추가 삭제가 느리다. (단 순차적인 추가 삭제는 더 빠르다)
- 특정 용량이 능러아게 되면 1.5배 용량을 늘린 후에 새로운 배열에 기존 배열을 copy한다
  - ADD: O(1)
  - REMOVE: O(n)
  - GET: O(1)
  - Contains: O(n)
- 데이터 추가, 삭제를 위해 임시 배열을 생성해서 데이터를 복사
- 데이터의 인덱스를 가지고 있어 데이터 검색이 빠르다

LinkedList - 내부적으로 양뱡향의 연결 리스크 구성되어 있어서 참조하려는 원소에 따라 처음부터 순향향, 역뱡뱡향 순회 가능

- 크기를 변경할 수 없다
- 비 순차적인 데이터 추가 삭제가 시간이 오래 걸린다.
- 읽는 시간은 느리지만, 추가 삭제가 빠르다.
  - ADD: O(1)
  - REMOVE: O(1)
  - GET: O(n)
  - Contains: O(n)
- 데이터 검색시 처음부터 노드를 순회하기 때문에 느리다

### HashMap Null 가능?

- Value에서는 가능하다, Treemap은 정렬 순서때문에 불가능하다

### HashMap vs TreeMap vs LinkedHashMap vs HashTable

HashMap - Array의 Index를 hash함수를 통해서 계산한다<br>

- Hash값을 사용하기 때문에 순서를 보장하지 않는다.
- 해당 Array에 바로 접근하기 때문에 get()은 O(1)이다.

TreeMap - Entry가 Tree구조로 저장되어 있다.

- Tree구조로 되어 잇어 정렬이 되어 있다
- Tree 구조때문에 get()은 O(logN) 성능을 보인다.

LinkedHashMap - HashMap과 동일하지만 Entry내에 before, after가 저장되어 있다.

- 입력 메서드의 순서를 보장 받을 수 있다.

HashTable - Map 인터페이스를 구현한 클래스로 중복허용X, 동기화 처리가 되어 있다.

- HashMap과 다르게 Key값으로 null을 허용하지 않는다.

### Add vs Offer

- add: 데이터를 추가할 때 문제 상황이 발생하는 경우 예외를 던진다
- offer: 데이터를 추가할 때 문제 상황이 발생하는 경우 false를 던진다

<hr>

## Call By Value vs Call By Reference

### Call By Value

- 함수 안에서 인자 값이 변경되어도 외부의 변수 값은 변경되지 않는다.

### Call By Reference

- 함수 안에서 인자의 값을 변경되면, Argument로 전달된 객체의 값도 변경된다.

## Servlet

클라이언트 요청을 처리하고 그 결과를 반환하는 웹 프로그래밍 기술

- 자바를 사용하여 웹을 만들기 위햐수 필요한 기술
- 클라이언트가 요청을 하면 그에 맞는 결과를 전송해 주는 것

- 클라이언트의 요청에 대해 동적으로 작동하는 웹 애플리케이션 컴포넌트
- HTML을 사용하여 요청에 응답
- JAVA THREAD를 이용해서 동작
- MVC 패턴에서 Controller에서 이용된다
- HTTP 프로토콜 서비스를 지원하는 HttpServlet클래스를 상속받는다

### JSP

서블릿은 JAVA 소스코드 한에 HTML 코드가 있다, JSP는 HTML 소스 코드 속에 자바 소스 코드가 들어가는 구조

JSP는 서버 스크립트 기술로 미리 약속된 규정에 따라 간단한 키워드를 조하하여 입력하면, 실행 시점에 각각의 키워드에 매핑되어 있는 어떤 코드로 변환 후에 실행된다

### Servlet VS JSP

Servlet: 자바코드로 구현하고 컴파일 하고 베포해야 한다

- 사용자의 요청을 받아 분석하고 비즈니스 층과 통신을 처리하고 처리한 결과를 다시 사용자에게 응답하는 컨트롤러 층을 담당

JSP: HTML처럼 태그를 사용하여 자바코드도 사용이 가능하다

- 장점을 최대한 활용할 수 있도록 프리젠테이션 계층(View)를 담당한다

### 동작 방식

1. 클라이언트가 URL를 입력하면 HTTP Request가 Servlet Container로 전송한다
2. 요청을 전송받은 Servlet Continaer는 HttpServletRequest, HttpServletResponse 객체를 생성
3. web.xml을 기반으로 사용자가 요청한 URL이 어느 Servlet에 대한 요청인지 찾는다
4. 해당 Servlet에서 Service 메서드를 호출한 후 클라이언트에 GET, POST 여부에 따라 doGet, doPost를 호출
5. 해당하는 동적페이지를 생성 후 HttpServletResponse 객체에 응답을 보낸다
6. 응답이 끝나면 HttpServletRequest, HttpServletResponse 객체를 소멸

### web.xml

Web application은 반드시 하나의 web.xml파일을 가지고 잇어야 핟나

- 브라우저가 Java Servlet에 접근하기 위해서 WAS(Tomcat)에 대한 필요한 정보를 알려줘야 하는데 Servlet을 호출할 수 있으며, 이것을 정하는 것이 web.xml이다

1. ServletContext의 초기 변수
2. Servlet 및 JSP에 대한 정의 및 맵핑
3. MimeType 매핑
4. Session의 대한 유효시간
5. Welcome file list

### Servlet Continaer

서블릿을 관리해 주는 역할

- 웹 서버와 통신 지원
  - listen, accept등을 API로 제공하여 복잡한 과정을 생략한다
- 서블릿 생명주기 관리ß
  - 서블릿의 탄생과 죽음을 관리한다, 클래스를 로딩하고 인스턴스화 한다
- 멀티 쓰레드 지원 및 관리
  - 쵸엉이 올때마다 새로운 자바 스레드를 생성하고 관리한다
- 선언적인 보안 관리
  - 개발자는 보안과 관련된 내용을 하지 않아도 된다

### Servlet 생명 주기

1. init(): 클라이언트 요청이 들어오면 컨테이너는 해당 서블릿이 메모리에 있는지 확인하고 없으면 init()를 실행한다

- 처음 한 번만 실행되기 때문에, 서블릿 스레드에서 공통적으로 사용하는 것은 오버라이딩하여 구현한다

2. service(): 클라이언트 요청에 따라서 service() 메서드를 통해 요청에 대한 응답이 doGet(), doPost()로 분기된다

- 서블릿 컨테이너가 클라이언트 요청이 오면 httpServletRequest, httpServletResponse에 의해 requets, response 객체가 제공된다

3. destroy(): 컨테이너가 서블릿을 종료하면 destroy() 메서드를 호출하고 단 한 번만 실행이 된다

## Apache HTTP Server

오픈 소스 소프트웨어 아파치 소프트웨어에서 만든 웹 서버

- 클라이언트에게 HTML 문서로 된 페이지를 웹 브라우저로 전달

- 리눅스가 서버 OS 최다 점유을을 차지하자 아파치도 자연스럽게 최다 점유을을 가지게 되었다

- 동적인 웹 서버 같은 경우는 사용자의 요구에 따라서 다양한 웹 페이지를 제공한다

특징

- 오픈 소스가 무료
- 다양한 모듈을 제공
- 확장성과 보안 수준이 높다
- 많은 기능으로 상대적으로 느리다
- 오버헤드가 많이 발생된다

### Apache Tomcat

현재 가장 일반적이고 많이 사용되는 WAS(웹 애플리케이션 서버)

- WAS: 웹 서버와 웹 컨테이너의 결합으로 다양한 기능을 컨테이너에 구현하여 다양한 역할을 수행한다
- 웹 컨테이너는 클라이언트의 요청이 있을 때 내부 프로그램을 통해 결과를 만들어내고 이것을 다시 클라이언트에 돌려주는 역할을 한다

- Apache: 정적인 데이터를 처리하는 웹 서버
  - 클라이언트가 GET, POST, DELETE 등등의 메서드를 요청을 하면 그에 대한 결과를 돌려주는 기능을 한다
  - 정적인 HTML이나 이미지를 제공하는 서버를 웹 서버
- Apache Tomcat: 동적인 데이터를 처리하는 웹 서버
  - 동적인 처리를 하기 때문에 WAS라고 한다
  - 사용자 요청(웹 브라우저) -> 웹 서버 -> WAS(동적 처리) -> 웹 서버 -> 사용자 응답 메시지(웹 브라우저)
  - 사용자가 요청한 것들 중 자체적으로 처리할 수 없는 것들을 톰캣과 같은 컨테이너에게 넘겨 처리 결과를 받아와서 클라리언트에게 넘겨주는 역할도 수행한다

### Synchronized

Multi-Thread 환경에서 동기화를 제어해야 되는 경우 Synchronized를 사용해서 동일한 자원을 동시에 접근하게 되었을 떄 동시 접근을 막는다.

1. Method에 사용하는 방법
2. 블록에 사용하는 방법

### Static

정적이라는 의미를 가지고 있다.

- Static 키워드를 통해 생성된 정적 멤버들은 Heap이 아니라 Static 영역에 할당을 하게 된다.
- Static 영역에 할당된 메모리는 모든 객체가 공유하니 어디에서든지 참조할 수 있다.
- Static 영역에 존재하기 때문에 프로그램 종료시 가지 메모리가 할당된 채로 존재하게 된다.

### Final

Final 필드는 초기값이 저장되면 최종적인 값이 되어 프로그램 실행 도중에 수행할 수 없다.

초기값을 줄 수 있는 방법

1. 필드 선언시에 주는 방법
2. 생성자를 통해서 주는 방법

- Final이 설정이 되어 있다면 상속 받더라도 오버라이딩이 불가능하다.

## Mutable VS Immutable

- Mutable: 인스턴스가 생성된 후에 값의 내용이 변할 수 있는 클래스, 주소는 바꾸지 못한다.
  - String을 제외한 참조 타입 변수
- Immutable: 인스턴스가 일단 생성된 후에는 인스턴스의 내용이 절대변하지 않는 특징을 가진 클래스

  - Int등의 기본 타입들 and String

- String 같은 경우는 컴파일 시점에서 자동으로 StringBuffer가 실행이 된다.
- StringBuilder는 Mutable하다

- String 같은 경우는 concat(추가) 할때 마다 new String을 통해서 변경이 된다.
  - new String을 할 때 마다 해시코드 값이 설정이 된다.
- StringBuilder 같은 경우는 append(추가) 할때 마다 바로 이어 붙혀주게 된다.

  - 해시코드 값은 변하지 않고 데이터가 변경되게 된다.

- 즉, String은 불변의 속성을 갖는다.
  - 새로운 데이터를 만들면 데이터는 새로 생성이 되고 기존 문자열은 GC에 들어간다.
  - 변하지 않는 문자열을 자주 읽어들이는 경우 String을 사용하면 좋다.
  - 문자열 추가, 수정, 삭제등의 연산이 빈번하게 발생하는 경우 Heap에 많은 Garbage가 생성이 된다
- StringBuilder, StringBuffer는 가변성을 가지기 때문에 동일 객체 내에 문자열을 변경이 가능하다

- StringBuffer는 멀티 쓰레드 환경에서 안정성을 가지고 있다
- StringBuilder는 동기화를 지원하지 않기 때문에 단일 스레드에서 성능이 좋다.

### String Pool

자바에서 String을 관리하기 위해서 String Pool을 통해서 해시코드 값들을 저장

- "=="를 통해서 String이 같이 않을 때의 원인이 된다.
- String이 선언되면 String Pool에 반드시 String literal이 생겨난다. 그리고 같은 값을 찾는 경우가 생가면 다시 반환한다.
- new 를 통해서 생성되는 경우 새로운 메모리가 Heap에 선언이 되면서 같은 문자열이라도 String Pool에 추가된다.
- 즉, new로 생성된 String은 완전히 다른 메모리에 존재를 하게 되어 String Pool에 없이 존재한다.

```JAVA
String str1 = "abc";
String str2 = new String("abc");
String str3 = new String("abc");
String str4 = "abc";
if(str1 == str2) -> false // new 연산자와 String Pool의 차이
if(str3 == str4) -> false // new 연산자와 String Pool의 차이
if(str1 == str4) -> true  // 같은 String Pool에 있음
if(str2 == str3) -> false // new 연산자와 new 연산자 이므로 주소값이 다름

```

### 정리

- String: 문자열 연산이 적고 멀티스레드 환경
- StringBuffer: 문자열 연산이 많고 멀티스레드 환경
- StringBuilder: 문자열 연산이 많고 단일스레드 혹은 동기화 고려 X인 경우

## Parameter VS Argument

```JAVA
public void cancat(str1, str2){
  return a + " " + b
}

str.concat("A", "B");
```

- Parameter: concat 입장에서 str1, str2를 의미한다.
- Argument: str입장에서 "A", "B"를 의미한다.

## Checked Exception VS Unchecked Exception

Exception: 프로그램 중에 개발자의 실수로 예끼치 않은 상황이 발생했을 때

### Checked Exception

RuntimeException의 하위 클래스가 아닌 Exception의 하위 클래스

- Checked Exception은 반드시 에러 처리 해야하는 특징이 있다.
- 컴파일 단계에서 확인한다.
- 예외 발생하면 트랜잭션을 Rollback하지 않는다.

### Unchecked Exception

RuntimeException의 하위 클래스들을 의미한다

- 말 그대로 실행중에 발생할 수 있는 예외를 의미한다.
- 실행 단계에서 확인한다.
- 예외 발생하면 트랜잭션을 Rollback 한다.

## Volatile

멀티 스레드 환경에서 동기화 해주는 키워드

- 기존 멀티 스레드 애클리케이션은 성능적인 이유로 메인 메모리에서 변수를 읽고 CPU 캐시에 복사하고 작업한다.
- CPU메모리 영역에 캐싱된 값이 아니라 항상 최신의 값을 가지도록 메인 메모리 영역에서 값을 참조한다.
- 연자적 연산에만 동기화 보장한다.
- 하지만 다른 스레드가 데이터 값을 저장하지 않았으면 최신의 값을 가져오지 못한다.
- 메인 메모리로 부터 읽거나 쓰기 떄문에 CPU 캐시보다 비용이 더 비싸다

- Syncronized: 작업 자체를 원자화한다.
- Volatile: 특정 변수에 대해서 최신 값을 제공한다.
