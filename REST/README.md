# REST

Representational State Transfer API(표현 상태 전송 API)<br>
웹에 존재하는 모든 자원(이미지, 동영상, DB 자원)에 고유한 URI를 부여해 활용 <br>
자원을 정의하고 자원에 대한 주소를 지정하는 방법론<br>
이런 REST의 형식을 따른 시스템을 RESTful이라고 부른다.

## REST의 구성요소

1. 자원(Resource), URI

- 모든 자원은 고유한 ID를 가지고 ID는 서버에 존재하고 클라이언트는 각 자원의 상태를 조작하기 위해 요청을 보낸다.
- HTTP에서 이러한 자원을 보내는 ID는 'user/1'같은 HTTP URI이다

2. 행위(Verb), Method

- 클라이언트는 URI를 이용햐 자원을 지정하고 조작하기 위해 Method를 사용한다. (GET, POST, PUT, DELETE)

3. 표현(Representation)

- 클라이언트가 서버로 요청을 보냈을 때 서버가 응답으로 보내주는 자원의 상태를 Representatio

## REST의 특징

1. Uniform(유니폼 인터페이스)

- URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일
- 장점
  - 요청하는 Client가 Platform(Android, IOS, JSP 등)에 무관하며, 특정 언어에 종속받지 않는다
  - REST API는 HTTP를 사용하는 모든 플랫폼에서 사용 가능하며, Loosely Coupling(느슨한 결함) 형태를 갖는다
  - 서버의 기능이 변경이 되어도 클라이언트를 업데이트 할 필요가 없어진다

2. Stateless(무상태성)

- 작업을 위한 상태 정보를 따로 저장하고 관리하지 않는다
- 세션 정보나 쿠키 정보를 별도로 저장하고 관리하지 않기 때문에 API 서버는 들어오는 요청만 단순히 처리한다
- 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 구현이 단순해진다.
- Stateful - Server와 Client간 세션의 'State(상태)'에 기반하여 Client에 response를 보낸다
  - 세션 상태를 포함한 Client와 세션 정보를 Server에 저장하게 된다
  - EX) TCP (3-way handshaking 처럼 SYN과 STNACK를 주고 받으면서 서로의 상태를 확인한다)
  - 세션의 정보를 Server에 저장하고 세션 상태에 따른 응답을 한다
  - Client A가 로드밸런서를 통해 Server #1에 저장이 되면 Client A의 세션 정보가 저장이 된다
  - 로드밸런서를 연결하여 Server #2에 연결하는 경우 Client A에 대한 정보가 없으므로 세션 인증을 처음부터 다시 연결해야 한다
  - 이러한 중복 작업을 없애기 위해서는 Client A의 요청은 Server #1을 향애 유지되도록 관리를 해야한다
- 장점
  - Scaling이 자유롭다
    - Stateful 같은 경우는 Client의 세션 정보가 새로 Scale out된 서버에 저장되어 있지 않다
    - 세션 정보를 옮겨주는 부수적인 관리가 필요하다
    - Statless같은 경우 Server는 Client 세션 관리를 하지 않으므로 Scale out을 편하게 할 수 있다
    - Stateless 서비스 구조는 Client의 정보들을 외부 DB에 저장을 하게 된다

3. Cacheable(캐시 가능)

- HTTP라는 기존 웹 표준을 그대로 사용하기 떄문에, 웹에서 사용하는 기존 인프라를 그대로 활용이 가능
- HTTP 프로토콜 표준에서 사용하는 Last-Midified태그나 E-Tag를 이용하면 캐싱 구현 가능

- PUT, DELETE에는 사용이 불가능하며 주로 GET에 일반적으로 사용한다
  - POST는 일반적으로 불가능 하지만 리소스의 만료시간(Expires), 리소스가 생성된 시간부터 상대적 시간(Cache-Control)을 통해서 사용가능하다

- E-Tag: 리소스를 특정 문자열로 변경한 값이다
  - 만약 리소스가 변경되면 이 값도 변경이 해제 되면서 cache 적용이 해제된다
  - Client에서는 ETag를 체크하기 위해 문자열을 헤더와 함께 보내고 캐시를 확인하여 용도의 해저 조건을 확인한다
  - etag와 동일하면 304(Not Modified), 동일하지 않으면 200과 리소스를 반환한다
- Last-Modified
  - 해당 리소스가 마지막으로 변경되었는지 확인한다
  - 헤더를 보냈을 때 Last-Modified가 If-Modified-Since보다 작다면 304, 아니면 200과 리소스를 반환한다

4. Self-descriptiveness(자체 표현 구조)

- REST API 메시지만 보고도 이를 쉽게 이해할 수 있어야 한다

5. Client - Server 구조

- 클라리언트는 사용자 인증, 컨텍스트(세션, 로그인 정보)등을 직접 관리하는 구조
- 각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로간 의존성이 줄어든다

6. 계층형 구조

- REST 서버는 다중 계층으록 구성되어 있으며, 보안, 로드 밸런싱, 암호화 계층을 추가해서 유연성 추가 가능
- PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 한다

## REST 설계

1. URI는 정보의 자원을 표현해야한다
2. 자원에 대한 행위는 HTTP METHOD(GET, POSt, PUT, DELETE)로 표현한다

### HTTP vs REST

- HTTP는 Stateless한 성격을 가진 '프로토콜'
  - HTTP를 사용해서 정해둔 스펙으로 데이터를 주고 받으며 통신하는 것
- REST는 Stateless한 성격을 가진 '설계 구조'
  - HTTP에 제약 조건이 추가가 된다
    - 자원의 식별
    - 메시지를 통한 리소스 조작
    - 자기서술적 메서지
    - 애플리케이션의 상태에 대한 엔진으로서 하이퍼미디어
- 즉, REST는 HTTP의 방법이다
  - HTML처럼 하이퍼 링크가 추가되어 어떤 API를 호출해야 하는지 해당 링크를 통해서 받을 수 있어야 한다

## REST API의 규칙

1. URI는 정보의 자원을 표현해야 한다(리소스 명은 동사보다는 명사를 사용)

- DELETE와 같은 행위는 표현이 들어가서는 안된다

2. 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE 등)로 표현

- 회원 정보를 가져오는 경우: GET
- 회원 정보를 추가하는 경우: POST
- 회원 정보를 수정하는 경우: PUT
- 회원 정보를 삭제하는 경우: DELETE

URI는 자원을 표현하는 데 집중하고 행위에 대한 정의는 HTTP METHOD를 통해 REST한 API를 설계하는 중심 규칙

```
GET - /members/show/1 - X
GET - /members/1 - O

GET - /members/delete/2 - X
DELETE - /members/2 - O
```

### URI 설계시

1. 슬래시 구분자('/')는 계층 관계를 나타내는 데 사용
2. URI 마지막 문자로 슬래시 구분자 ('/')을 포함하지 않는다
3. 하이픈('-')은 URI 가독성을 높이는데 사용한다
4. 밑줄('\_')은 URI에 사용하지 않는다
5. URI 경로는 소문자를 사용한다(대소문자에 따라 다른 리소스로 파악된다)
6. 파일 확장자(EX: JPG, PNG)는 URI에 포함하지 않는다

### 리소스 간의 관계를 표현하는 방법

```
/리소스명/리소스 ID/관계가 있는 다른 리소스명
GET /users/{userid}/devices
```

관계 명이 복잡하다면 이를 서브 리소스에 명시적으로 표현할 수 있다
```
/ 사용자가 가지고 있는 디바이스 (기본형)
GET /users/{userid}/devices
/ 사용자가 좋아하는 디바이스
GET /users/{userid}/likes/devices

```

### Collection와 Document

```
/sports/soccer/players/13
```

- Collection: Sports, Players
- Document: soccer, 13
- 이 둘을 사용하고 단수 복수를 사용하여 좀 더 이해하기 쉬운 URI를 설계할 수 있다

## HTTP 응답코드

- 2XX
  - 200(OK): 클라이언트의 요청을 정상적으로 수행함
  - 201(CREATED): 클라이언트가 어떠한 리소스 생성을 요청, 해당 리소스가 성공적으로 생성됨(POST)
- 3XX
  - 300(MULTIPLE CHOICE): 요청에 대한 응답이 하나 이상 존재하여 사용자는 하나를 골라야 한다
  - 301(MOVED PERMANETLY): 클라이언트가 요청한 리소스에 대한 URI가 변경되었을 경우
- 4XX
  - 400(BAD REQUEST): 클라이언트의 요청이 부적절 할 경우 사용하는 응답코드
  - 401(UNAUTHORIZEd): 클라이언트가 인증되지 않은 상태에서 보호된 리소스를 요청했을 떄 사용하는 코드(로그인 안한유저가 로그인 후 가능한 요청을 시도)
  - 403(FORBIDDEN): 유저 인증 상태와 상관 없이 응답하고 싶지 않은 리소스를 요청했을 때
  - 404(NOT FOUND): 클라리언트가 요청한 리소스에서는 사용 불가능한 Method를 이용했을 경우
- 5XX
  - 500(INTERNAL SERVER ERROR): 서버에 문제가 있는 경우
  - 501(NOT IMPLEMENTED): 서버가 요청을 이행하는 데 필요한 기능을 지원하지 않음

## 필터링

URL 매개변수는 REST를 통해서 필터링 하는 방법은 가장 쉬운 방법이다

### LHS

연산자를 인코딩을 대괄호 ("[]")을 통해서 사용한다

- `GET/item?price[gte]=10&price[lte]=100`
- 이 방식을 통해서 10 이상 100 이하의 값을 추출할 수 있다
- LHS Brackets는 서버 측면에서 구문 분석하기가 조금 어렵지만 더 큰 기능을 제공한다
  - 사용편의성: 중첩된 JSON 개체를 대괄호로 쉽게 인코딩, 쿼리 문자열을 만들 수 있다
  - 구문 분석 간편: URL 파라미터 키에 필드 이름과 연산자가 모두 포함되어 있어서 URL을 보지 않고 GROUP BY하기 쉽다
  - 특수 문자를 벗어날 필요가 없다: 필터에 사용자가 설정할 수 있는 추가 사용자 지정 메타데이터 필드가 포함될 수록

### RHS

연산자를 (":")추가하여 구분할 수 있다.

- `GET/item?price=gte:10&price=lte:100`
- 중복 필터가 지원되지 않는 경우 서버측에서 구문 분석하기 쉽다
- 사용자 정의 바인더는 필요하지 않다
- 시퀀스 또는 맵을 통해서 동일 변수들을 받을 수 있다.

### Second Query Param

검색이 필요한 경우 검색 매개 변수를 사용하여 직접 필터와 범위에 대한 지원을 추가할 수 있다

- `GET /items?q=title:red chair AND price:[10 TO 100]`
- API 사용자를 위한 가장 유연한 쿼리
- 백앤드에 거의 구문 분석이 필요 없으며 검색 엔진 또는 데이터 베이스에 직접 전달될 수 있다

## Pagination

- ```GET /items?limit=n&offset=ㅡ```
- n개의 개수 제한으로 m번째 데이터부터 데이터를 확인할 수 있다

- 구현이 용이하며, 파리미터를 SQL 쿼리에 직접 전달하는 것 외에는 거의 코딩이 필요하지 않다
- Stateless한 서버 상태를 유지한다
- 사용자 정의 Sort_by 매개변수에 관계 없이 작동한다
