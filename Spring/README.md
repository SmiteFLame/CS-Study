# Spring

JAVA의 웹 프레임 워크로 JAVA 언어를 기반으로 사용한다.
JAVA로 다양한 애플리케이션을 만들기 위한 프레임 워크<br>

자바 플랫폼을 위한 오픈 소스 프레임 워크로써 경량 컨테이너로 자바 객체를 담고 관리하는 프레임 워크<br>
IOC(제어의 역행) 기반 프레임 워크로써 객체의 생성, 의존성 객체 생성, 메서드 호출을 프로그램의 흐름을 결정을 직접 하는 것이 아니라 스프링에게 넘겨 줌으로써 제어의 역적을 도와주는 프레임 워크

### 프레임 워크

- 자주 쓰일만한 기능들을 한데 모아 놓은 유틸(클래스)들의 모음
- 기본적인 설계나 필요한 라이브러리는 알아서 제공해주고 개발자가 만들고 싶은 기능을 구현하는데 집중할 수 있도록 해준다.

### 프레임 워크 VS 라이브러리

프레임워크 - 프레임워크라는 큰 틀에서 개발자가 필요한 기능들을 개발<br>
라이브러리 - 개발자가 필요한 기술을 활용하기 위해 라이브러리를 호출

### MVC2

Model, View, Controller 구조로 나뉘어서 인터페이서와 비즈니스 로닉을 분리하여 개발하는 방법<br>
Model은 데이터 처리를 주로 담당 - Service, Controller의 정보 없이 오직 대기능만 수행<br>
View는 Interface를 담당하면서 Controller를 통해 모델에 대한 시각화를 담당하여 자신이 요청을 보낼 Controller의 정보만 알고 있어야 한다.<br>
Controller는 View에 받은 요청을 가공하여 Model(Service)에 전달하는 역할과 반대 역할

<hr>

## 컨테이너

Servlet을 실행하고 관리하는 역할을 한다

- 코드의 처리과정을 위임 받은 독립적인 객체
- 적절한 설정만 되어 있으면 누구의 도움 없이도 프로그래머가 작성한 코드를 스스로 참조한 뒤 알아서 객체의 생성과 소멸을 컨트롤 해준다

### 동작 원리

1. Requetst와 Response 객체를 생성한다.
2. Servlet의 스레드를 생성하여 두 객체를 넘겨준다.
3. 스레드의 Service 메서드를 호출한다.
4. DoGet인지 DoPost중에 선택을 한다.
5. 완료된 객체를 HttpResponser로 변환하여 보낸다.
6. Request와 Response를 소멸한다.

### 특징

1. 개발자가 해야하는 역할을 컨테이너가 도 맡아서 개발자의 역할을 줄여준다.
2. 컨테이너를 개발자가 웹 서버와 통신하기 위한 소켓을 생성하고, 특정 포트에 리스닝하고, 스트림을 생성하는 등의 복잡한 일들을 할 필요 없게 해준다.
3. 컨테이너는 Servlet의 생성부터 소멸까지의 일련의 과정을 관리하는 역할을 한다.
4. 컨테이너는 요청이 들어올 때 마다 새로운 자바 스레드를 만들고 운영하여 개발자의 부담을 줄여준다.

<hr>

## Spring의 특징

### IOC

Java 코딩시 New 연산자, 인터페이스 호출, 데이터 클래스 호출하는 것을 개발자가 아닌 스프링이 대신 관리한다.<br>
즉, 객체의 생명 주기 관리를 개발자가 아닌 스피링이 한다.

- 객체의 생성 ~ 생명 주기를 컨테이너가 도 맞아서 하는 것이다
- 제어권이 컨테이너로 넘어감으로써 DI와 AOP등이 가능한 것이다
- 라이브러리: 내 코드가 라이브러리를 이용한다.
- 프레임워크: 프레임워크가 내 코드를 실행한다.

### DI

객체가 서로 의존하는 관계가 될 수 있도록 의존성을 주입하는 것<Br>
각 클래스 사이에 필요로 하는 의존 관계를 빈 설정 정보를 바탕으로 컨테이너가 연결해주는 것<br>

1. 생성자를 통해 주입하는 방식
2. Setter를 통해 주입하는 방식
3. Method를 통해 주입하는 방식

### IOC VS DI

IOC - 객체의 흐림, 생명주기 관리를 독립적인 제 3자에게 역할과 책임을 위임하는 방식<br>
DI - 인터페이스를 통해 다이나믹 하게 객체를 주입하여 유연한 프로그래밍을 가능하게 하는 패턴

### POJO

평범한 자바 프로젝트라는 의미<br>
Getter, Setter등 단순한 자바 오브젝트를 사용함으로써 의존성이 없고 유지보수가 편리하도록 제작된 오브젝트<br>
객체 지향적인 다양한 설계가 가능해지도록 하여 Spring에서도 pojo를 기반으로 프레임 워크 제작

### AOP

관점 지향 프로그래밍<br>
객체지향은 유사한 데이터들을 모아 분리하고 낮은 결합도와 캡슐화라는 장점이 있지만 중복된 코드가 많아진다.<br>
AOP는 핵심 기능과 공통 기능을 분리시킴으로서 무분별하게 중복되는 코드를 줄이게 된다.

- 로직을 기준으로 핵심과 부가적인 기능을 나눈다.
- 각각의 클래스에서 유사한 기능들을 모아서 사용하는 것들을 말한다.

- 핵심적인 관점: 핵심 비즈니스 로직
- 부가적인 관점: 앞에서 이야기한 공통으로 처리되어야 하는 코드

- 객체 지향과 달리 부가적인 관점이 핵심 비즈니스 로직의 바깥에 포함이 되어 있다.
- 로그, 보안, 트랜잭션, 예외 처리와 같은 부가적인 기능들을 일일이 추가하지 않아도 된다.

- 관점(Aspect): 공통으로 적용될 기능
- 어드바이스(Advice): 실제로 부가적인 기능을 구현한 객체
- 조인 포인트(Join Point): Advice를 적용할 위치
  - Service에서 CRUD를 처리하는 메서드 중에서 원하는 메서드를 골라서 Advice를 적용할 수 있다.
  - 이 때, Service의 모든 메서드는 Join Point가 된다.
- 포인트 컷(Point Cut): Advice를 적용할 Join Point를 선별하는 과정이나, 그 기능을 정의한 모듈을 의미
- 타겟(Target): 실제로 비즈니스 로직을 수행하는 객체
  - 즉, Advice를 적용할 대상
- 프록시(Proxy): Advice가 적용되었을 때 생성되는 객체
- 인트록덕션(Introduction): 타겟이 없는 새로운 메서드나 인스턴스 변수를 추가하는 기능
- 위빙(Weaving): Point Cut에 의해서 결정된 Target의 Join Point에 Advice를 적용하는 것

### Maven

프로젝트 관리 도구로 프로젝트의 모든 단계에서 사용하는 개발 도구이지만, 프로젝트에서 필요한 라이브러리를 자동으로 관리해주는 빌드 도구

- 자바 기반의 프로젝트의 라이프 사이클 관리를 위한 빌드 도구로 컴파일과 빌드를 동시에 수행한다

### Spring boot

스프링부트는 단독으로 실행되는 상용화 가능한 수준의 스프링 기반 애플리케이션을 쉽게 만든다.

- 자동설정, 쉬운 의존성 관리, 내장 서블릿 컨테이너
- Starter 종속성을 제공하여 애플리케이션의 간편하고 자동화된 빌드 및 설정 제공
- embedded서버를 제공하면서 복잡한 설정들을 간편하게 제공

<hr>

## 구성 요소

### 기본 환경 설정 파일

- root-context.xml - 공통 빈을 설정하는 곳, View 제외 빈 설정
- servlet-context.xml - servlet 요청과 관련된 객체 정의파일, view 페이지 경로 및 파일 지정, bean 설정
- web.xml - 환경 설정 부분, 베포 서술자. 서블릿 이름 설정, 패턴 설정, filter를 활용하여 encoding, 에러 코드별 error페이지, 웹 애플리케이션 요청시 시작 파일 설정
- pom.xml - Maven 설정 파일 / 필요한 라이브러리 다운 받는 경우 사용

## Spring MVC

Spring 프레임워크에서 제공하는 웹 모듈

MVC는 Model-View-Controller으로 구성이 되어 있다

- Web Server에 특화되어 만들어진 모듈이라, 개발자가 해야할 영역을 더 적게 만들어 준다
- 즉, 기존에 Spring보다 더 깔끔하고 간편하게 개발 가능

- Model: '데이터' 디자인을 담당한다
  - 데이터들의 정의 로써, DTO, DAO와 같은 아이들이다
  - 최대한 구체적이고 작은 Entity를 유지하면서 Model을 설계하는 것이 중요하다
- View: 실제로 랜더링되어 보이는 페이지
  - Client가 보이는 화면으로 HTML같은 파일들이다
  - 도메인 모델의 상태를 변환하거나 받아서 렌더링 역할을 한다
  - 오직 객체를 전달받아서 출력하는 역할을 한다
- Controller: 사용자의 요청을 받고, 응답을 주는 로직을 담당한다

  - Model과 View를 연결해주면서 동작 순서나 방식을 제어한다
  - 웹 프로그래밍에서는 Controller에서 Service Layer를 분리하여 Domain 로직이 수행되는 곳과 view 요청을 매핑하는 곳을 독립적으로 관리

- 장점
  - 도메인을 작은 역할 단위로 분리하여 설계하는 작업으로 분리 된다
  - 각자의 역할에 집중할 수 있도록 개발할 수 있다
  - 유지 보수성, 애플리케이션 확장성, 유연성, 중복코딩 문젬 제거
- 단점
  - 설계 시간이 오래 걸리고 model과 view의 완벽한 분리가 힘들다
  - 한 Model은 다수의 View를 가질 수 있고 Controller를 통해서 한 View에 연결되는 Model이 여러개가 될 수 있다
  - Controller는 View와 라이프 사이클이 강하게 연결되어 있어 분리하기 어렵다

### Spring MVC 구성 요소

1. DispatcherServlet - (View와 Controller의 중간 단계)
   - Spring Container(Controller의 Life Cycle을 관리)를 생성한다
   - 클라이언트의 요청을 처음 받아서 Handler에게 전송한다
   - 컨트롤러의 요청을 중앙에서 처리하는 MVC의 핵심 구성 요소
   - Web.xml에 한개 이상의 DispatcherServlet 설정
2. HandlerMapping
   - 클라이언트의 요청 URL이 어떤 컨트롤러가 처리할 지 결정
3. Controller
   - 클라이언트의 요청을 처리한 뒤 결과를 DispatcherSerlvet에게 알려준다.
4. View Resolver
   - Logical View Name - prefix, suffix -> pysical view object

### 동작 순서

1. Client는 URL을 통해 Request한다
2. DispatchServlet는 HandlerMapping을 통해 Request가 어느 Controller에게 온 요청인지 찾느다.
3. DispatchServlet는 HandlerAdapter를 통해 Request를 전달을 맡긴다.
4. HandlerAdpater는 해당 Controller에게 Request을 전달한다.
5. Controller는 로직을 처리한후 반환할 View의 이름을 반환한다.
6. DispatcherServlet는 ViewResolover를 통해 반환할 View를 찾는다.
7. DispatcherServlet는 Controller에서 View에 전달할 데이터를 추가한다.
8. 데이터가 추가된 View를 반환한다.

<hr>

## 데이터베이스 연동

### MyBatis

자바의 관계형 데이터 베이스를 좀 더 쉽게 사용할 수 있도록 하는 개발 프레임 워크<br>
JDBC를 통해 데이터 베이스에 엑세스 하는 작업을 캡슐화 하고 일반 쿼리, 저장 <br>프로시저등을 지원하여 매개 변수 및 중복 작업을 제거해준다.

특징

1. SQL Mapper 라이브러리로, 스프링과 함께 사용하는 경우 반복 처리 코드 없이 간결하다
2. Spring과 Mybatis를 연계하는 라이브러리를 이용시 직접 SQL문 호출 없이 자동화 처리 가능
3. @Annotation방식과 XML으로 SQL문을 처리가능하여 번거로운 작업 줄일 수 있다.

장점

1. SQL에 대한 모든 컨트롤을 하고자 할 떄 적합하다
2. SQL 쿼리들이 매우 잘 최적화 되어 있을 떄 유용하다

단점

1. 애플리케이션과 데이터베이스 간의 설계에 대한 모든 조작을 하고자 할 때 적합하지 않다.

### JPA

자바 애플리케이션에 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스(라이브러리 x)<br>
JPA는 단순히 명세이기 떄문에 구현이 없다. 대부분 Interface, Enum, Exception, Annotation으로 이루어져 있다.

- 직접적인 SQL문을 사용하지 않고 자바 코드를 사용해서 DB에 접근하고 조작할 수 있는 기술이다

장점

1. 객체 지향적으로 데이터를 관리할 수 있기 떄문에 비즈니스 로직에 집중 할 수 있다.
2. 데이터 생성, 변경, 관리가 쉽다.
3. 로직을 쿼리에 집중하기 보다는 객체 자체에 집중할 수 있다.
4. 빠른 개발이 가능하다.

단점

1. 잘 이해하고 사용하지 않으면 데이터 손실이 일어날 수 있다.
2. 성능상 문제가 있을 수도 있다

- @EnableJpaRepositories: JpaRepository에 대한 설정 정보를 자동적으로 로딩하고 Repository 빈을 등록하는 역할을 한다

- Entity: JPA가 관리하는 클래스로, 해당 클래스를 Entity라고 부른다
  - 테이블에 대응하는 하나의 클래스
  - JPA를 사용하여 테이블과 매핑해야할 클래스는 반드시 @Entity를 선언해야 한다
- 특징
  - public, protected이여야 한다
  - JPA 스팩으로 규정되어 있다

### 동작원리

- JPA에서 알아서 쿼리문으로 변환해 JDBC로 전달한 다음, JDBC는 해당 쿼리문을 DB에 전송해 결과값을 가지고 온다

- DataSource를 통해서 연결한다
  - DB Server와 기본적인 연결을 한다
  - DB Connection Pooling 기능을 사용한다
  - 트랜잭션 처리를 한다
- DB Server에 관한 정보를 설정
- property file 위치 저장
- 반드시 필요한 parameter 속성으로 설정
- 해당 datasource를 bean으로 등록

## 영속성 컨텍스트

엔티티를 영구 저장하는 환경

- EntityManager를 통해서 영속성 컨텍스트에 접근할 수 있다

- 영속화 된 상태가 바로 DB에 저장되는 것이 아니다

  - commit을 하게 된다면 영속성 컨텍스트에 있는 정보들이 DB에 쿼리로 날라간다

- JPA가 엔티티 객체들을 모아두는 공간

  - 엔티티 매니저는 관리하는 엔티티 객체들을 연속 컨텍스트에 넣어두고 객체들의 생사를 관리한다

- 비영속: 영속성 컨택스트와 관계가 없는 새로운 상태
- 영속: 엔티티 매니저를 통해 엔티티가 영속성 컨텍스트에 저장되어 관리되고 있는 상태
- 준영속: 영속성 컨택스트에서 관리되다가 분리된 상태
- 삭제: 영속성 컨텍스트에서 삭제된 상태

장점

- 1차 캐시
  - 엔티티를 영속 상태로 만든 후 다시 조회하는 경우 DB 접근이 아닌 영속성 컨텍스트에서 캐시된 내용을 조회 가능
- 동일성 보장
  - 동일한 영속성 컨텍스트내에서 동일한 키로 조회한 엔티티의 경우 같은 객체
- 쓰기 지연
  - JPA가 `entityManager.persist()`를 통해서 계속 쌓고 있는 상태
    - 쓰기 지연 SQL 저장소에 쌓는다
  - `transaction.commit()`을 통해서 쓰기 지연 SQL 저장소에 있는 Query들을 DB로 날린다
    - `flush()`를 하게 된다면 1차 캐시는 지우지 않는다
    - `flush()`후에 실제 DB Transaction에 commit된다
- 변경 감지
  - 엔티티의 수정 시 따로 쿼리 조작 메서드가 필요 없음
  - Entity 데이터 수정시 update나 persisit를 통해서 영속성 컨텍스트에 해당 데이터를

### 캐시

- 1차 캐시: 영속성 컨텍스트 내부의 엔티티를 보관하는 장소
  - 트랜잭션이 시작하고 종료할 때 까지만 유효하다.
  - 같은 엔티니가 있으면 동일성을 보장한다.
- 2차 캐시: 애플리케이션 범위의 캐시
  - 동시성을 극대화 하기 위해 캐시 한 객체를 직접 반환하지 않고 복사본을 만들어서 반환한다.
  - 영속성 컨텍스트가 다르면 객체 동일성을 보장하지 않는다.

### Entity Mananger

특정 작업을 위해 데이터베이스에 엑세스 하는 역할

- Entity를 DB에 등록, 조회, 수정, 삭제하는 역할
- EntityManangerFactory를 트랜잭션 단위를 수행할 때 마다 생성된다
  - EntityManagerFactory는 DB당 단 하나만 생성이 되야 한다
- 고객의 요청이 올때마다 사용했다가 닫는다
- 내부에는 영속성 컨텍스트가 있으며 이를 통해서 관리한다
- 여러 엔티티 매니저가 하나의 영속성 컨텍스트르 공유한다

- 여러 스레드가 동시에 접근하면 동시성 문제가 발생하므로 스레드간 절대 공유하지 않는다

- 객체들의 Flush은 Transaction에서 관리를 하게 되고 여기서는 객체들의 생사를 관리하게 된다

### EntityTransaction

데이터를 변경하는 모든 작업은 반드시 Transaction안에서 이루어져야 한다

## Impl 분리하는 이유

OOP에서 의존 역전의 원칙과 매우 연관이 된다

- 추가적인 요청사항이 들어오면 기존 소스를 수정하는 것
- MVC Pattern에서 View는 자신이 요청할 Controller만 일고 있으면 된다
- Controller에서는 파라미터들을 이용해서 Service에게 요청을 하게 된다
- Service는 Request와 Response와 같은 매개 변수를 사용하지 않고 오직 비즈니스 로직만 구현하게 된다
- View에서 변경이 되어도 Service에서 View에 종속적인 코드가 없기 때문에 그대로 사용하게 된다
- 즉, 이 아니라, 기존 Service 인터페이스를 구현한 다른 클래스를 구현해 그 객체를 사용

## 생성자 주입 방법

의존 관계를 주입하는 방법이다

- 생성자의 호출 시점에 1회 호출되는 것을 보장한다
- 주입 받은 객체가 변하지 않거나, 반드시 객체의 주입이 필요한 경우에 강제하기 위함이다
- 생성자가 1개만 있을 경우 @Autowired를 생략해도 가능하다

### 사용하는 이유

- 의존 관계 주입이 변경이 필요한 상황은 거의 없다
- 생성자 주입을 통해 변경의 가능성을 배제하고 불변성을 보장하는 것이 좋다

- 컴파일 시점에 누락된 의존성을 확인할 수 있다
- 애플리케이션 구동 시점에 순환 참조 에러를 방지할 수 있다

## Maven VS Gradle

빌드 관리 도구

- 자바 코드와 프로젝트 내에 필요한 각종 xml, properties, jar 파일들을 JVM이나 WAS가 인식할 수 있도록 패키징 해주는 빌드 과정
- 프로젝트 생성, 테스트 빌드, 배포 등의 작업을 위한 전용 프로그램
- 필요한 라이브러리들을 설정파일을 통해 자동으로 다운로드 해주고 이를 간편히 관리해주는 도구이다

### Maven

Java용 프로젝트 관리 도구

- 빌드 중인 프로젝트, 빌드 순서, 다양한 외부 라이브러리 종속성 관계를 pom.xml 파일에 명시한다
- Maven은 외부 저장소에서 필요한 라이브러리와 플러그인들을 다운로드 한 다음, 로컬시스템의 캐시에 모두 저장한다

### Gradle

Groovy 언어(JAVA의 스크립트 언어)를 사용한 빌드 관리 도구

- 프로젝트의 어느 부분이 업데이트 되었는지 알기 때문에, 빌드에 점진적으로 추가할 수 있다
- 업데이트가 반영된 빌드의 부분은 더 이상 재 실행되지 않는다

### 차이점

- Gradle: 작업 의존성 그래프
  - 어떤 Task가 업데이트 되었고 안되었는지 체크를 하기 때문에 빌드 시간이 단축이 된다
  - Concurrent에 안전한 캐시를 허용한다: 두 개 이상의 프로젝트가 동일한 캐시를 쓰게 되면 서로 overwrite되지 않도록 서로 동기화 시킨다
  - Maven에 비해서 친숙하지는 않지만 확장성이 뛰어나다
- Maven: 고정적이고 선형적인 단계의 모델

## web.xml

Spring Boot으로 넘어가게 되면서 web.xml을 다른 기능들이 수행한다

1. application.properties: context-param 설정이 들어가 있다
2. Application.java: 이 함수를 정의하고 @EnableAutoConfiguration을 통해서 대부분의 설정을 자동으로 해준다
3. @Configuration: Bean 설정을 추가하여 등록을 할 수 있다

- 서블릿 관련 설정은 내부적으로 자동으로 설정이 된다
- Session-config는 application.properties으로 설정이 가능하다

## RestController VS Controller vs

Http ResponseBody가 생성되는 방식이 다르다

### Controller

주로 View를 반환하기 위해 사용된다

- Client가 Request할 때 Dispatcher Servlet의 Handler Mapping을 통해서 위치를 파악하고 해당하는 Controller에 전송을 한다
- Controller가 작업을 완료한 후에는 ViewResolver를 통해서 해당하는 View에 데이터를 전송하게 된다
- Controller는 Data를 반환하는 경우도 있다 이때에는 @ResponseBody을 활용을 해야한다 이를 통해 Json 형태로 데이터를 변환할 수 있다
- Data를 반환하기 위해서는 HttpMessageConverter가 동작을 하게 된다
  - 여러 Converter가 등록이 되어 있고 반환해야 하는 데이터에 따라서 Converter까 달라진다

### RestController

Controller에 ResponseBody를 추가한 것이다

- RestController의 주용도는 JSON 형태로 객체 데이터를 반환하는 것이다
- Client는 URI형식으로 웹 서비스에 요청을 보낸다, Mapping되는 Handler와 그 타입을 찾는 DispatcherServlet이 요청을 인터셉트 하고 RestController는 해당 요청을 처리하고 데이터를 반환

## Component VS Controller VS Service VS Repository

전부 Component를 가능하지만 관점에 대해서 연관성을 더 부여할 수 있고 AOP를 통한 처리가 쉽게 가능하다

### Component

Spring에서 관리하는 객체임을 표시하기 위해 사용되는 기본적인 Annotation

### Controller

Web MVC 코드에서 사용되는 Annotation, @RequestMapping을 해당 Annotation밑에서만 사용이 가능하다

### Repository

@Repository은 플랫폼 별 예외를 잡아서 Spring의 통합 검사되지 않은 예외 중 하나로 다시 던지는 것이다

### Service

비즈니스 로직과 Respository Layer를 호출하는 함수에 사용된다

- 다른 Annotation과 다르게 추가된 기능은 없다

### Transaction Annotation

스프링에서 제공하는 트랜잭션 처리 중 하나, 선언적 트랜잭션이라고도 부른다.

- Transactional은 Spring AOP를 기반으로 동작한다.
- 프록시 객체를 통해 기능을 수행하고 이상이 없으면 Commit, 예외가 발생하면 Rollback을 진행한다.

- Private 메소드에서는 사용 불가능 하다, 프록시 객체를 생성하야 하기 때문에 상속받을 수 없는 private는 트랜잭션 관리가 되지 않는다.
- 내부의 메소드 호출시 트랜잭션 관리가 되지 않는다: 메소드를 호출하면 프록시 객체가 아닌 대상 객체 메소드를 호출하기 떄문에 트랜잭션 적용이 되지 않는다.

1. 클래스, 메서드에 @Transactional이 선언되면 해당 클래스에 트랜잭션이 적용된 프록시 객체 생성
2. 프록시 객체는 @Transcational이 포함된 메서드가 실행될 경우, 트랜잭션을 시작하고 Commit or Rollback을 수행
3. CheckedException or 예외가 없는 경우 Commit
4. UnchechedException이 발생하면 Rollback

전파 레벨(Propagation)

- REQUIRED(DEFAULT): 부모 트랜잭션내에서 실행하며 부모 트랜잭션이 없으면 새로운 트랜잭션 생성
- REQUIRES_NEW: 부모 트랜잭션을 무시하고 새로운 트랜잭션 생성
- SUPPORT: 부모 트랜잭션에서 실행하며 없는 경우 트랜잭션 없이 실행
- MANDATORY: 부모 트랜잭션에서 실행하며 부모 트랜잭션이 없으면 예외 발생
- NOT_SUPPORT: 트랜잭션 없이 실행하며 부모 트랜잭션 내에서 실행될 경우 일시 정지
- NEVER: 트랜잭션 없이 실행하며 부모 트랜잭션이 존재하며 예외 발생
- NESTED: 부모 트랜잭션에서 진행될 경우 별개로 Commit, Rollback 가능, 부모 트랜잭션이 없으면 REQUIRED와 동일

## Spring Batch

- Batch: 일괄처리, 실행 도중 문제가 생기면 그 지점부터 재 시작할 수 있다는 점
- 같은 파라미터로 같은 함수를 실행하는 경우 실패한 부분에서 부터 다시 실행할 수 있도록 하는 것

### Batch 애플리케이션의 조건

- 대용량 데이터: 대량의 데이터를 가져오거나, 전달하거나, 계산하는 등의 처리를 할 수 있어야 한다.
- 자동화: 심각한 문제 해결을 제외하고는 사용자 개입이 없어야 한다.
- 견고성: 잘못된 데이터를 충돌/중단 없이 처리할 수 있어야 한다.
- 신뢰성: 무엇이 잘못되었는지 추적할 수 있어야 한다.
- 성능: 지정한 시간 안에 처리를 완료하거나 동시에 실행되는 다른 애플리케이션을 방해하지 않도록 수행해야 한다.

### VS Quartz

Quartz는 스케줄러의 역할이고 Batch와 같이 대용량 데이터 배치 처리에 대한 기능을 지원하지 않는다.

## 중복 코드 제거

Client -> [Filter] -> Dispatcher -> [Interceptor] -> Controller

### Filter

Dispatcher Servlet에 요청이 전달되기 전/후에 URL 패턴에 맞는 모든 요청에 대해 부가 작업을 처리할 수 잇는 기능을 제공

- Spring Container가 아닌 Tomcat과 같은 Web Container에 의해 관리가 되므로 Dispatcher Servlet 가기전에 요청을 처리하는 것이다.

- init: 필터 객체를 초기화하고 서비스에 추가하기 위한 메소드
  - 1회 init 메서드를 호출하여 필터 객체를 초기화 하면 이후 요청들은 doFilter를 통해 전/후 처리 된다.
- doFilter: url-pattern에 맞는 모든 HTTP 요청이 Dispatcher Servlet으로 전달되기 전/후에 컨테이너에 의해 실행되는 메서드
- destroy: 필터 객체를 서비스에서 제거하고 사용하는 자원을 반환하기 위한 메서드

### Interceptor

Spring에서 제공하는 기술로써 Dispatcher Servlet이 Controller를 호출하기 전과 후에 요청과 응답을 참조하거나 가공할 수 있는 기능을 제공

- preHandler: Controller가 호출되기 전에 실행된다. 컨트롤러 이전에 처리해야 하는 전처리 작업이 있을 때 사용된다.
- postHandler: Controller가 호출된 후에 실행된다. 후처리 작업때 사용된다.
- afterCompletion: 모든 뷰에서 최종 결과를 생성하는 일을 포함해 모든 작업이 완료된 후에 실해오딘다.
  - 요청 처리 중에 사용한 리소스를 반환할 때 사용하기에 적합하다.
