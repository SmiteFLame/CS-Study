# Scala

함수형 객체 지향 프로그래밍 언어, 자바의 복잡한 단점을 해결하기 위해 만들어졌다.

- 자바의 클래스를 사용할 수 있고, 자바에서도 스칼라 코드를 호출할 수 있다.

## 함수형 프로그래밍

- 함수는 입력 값을 파리미터를 통해 입력 받고, 출력 값을 리넡하는 구조를 가지고 있다.
- 때론 파라미터를 통하지 않고 입력을 받을 수 잇다.

```java
int readData(){
    int data = Reading.getValue(System.currentTimeMills());
    return data;
}
```

- 위 처럼 입력 파라미터가 없음에도 getValue 안에서 현개 시각을 받아서 처리한다. -> 순수하지 않다
- 함수형 프로그래밍은 이렇게 숨겨진 값을 없애고 순수한 함수를 만들도록 지향하는 프로그래밍이다.

## 특징

### 데이터 타입

- 모든 데이터 타입은 객체: 자바처럼 Primitive 타입을 지원하는 것이 아닌 모든 것이 객체로 이루어져 있고 자바의 Object와 같은 클래스는 Any 타입이다.

### 싱글톤 객체

- Static을 활용하여 싱글턴 객체를 생성
- Object 키워를 이용하여 아주 쉽게 싱글턴 객체를 사용할 수 있다.

### 변수 선언

- val, var 두 가지 키워드를 사용한다. var는 일반적으로 알고 있는 변수와 동일 val는 변하지 않는다

### 자바와의 관계

- JVM에서 사용이 되므로 빌드할 때 스칼라 라이브러리만 추가해주면 같이 실행이 가능하다

## Object, Case Class, Trait

### Object

하나 이상의 인스턴스를 가질 수 없는 형태의 클래스

- new 키워드로 인스턴스를 생성하는 대신 직접 이름으로 해당 객체에 접근한다.
- 객체는 실행중인 JVM에서 최초로 접근할 때 자동으로 인스턴스화 된다.
- 객체에 처음 접근 하기 전까지는 인스턴스화 되지 않는다.

### Case Class

자동으로 생성된 메서드 몇 가지를 포함하는 인스턴스 생성이 가능한 클래스

- 자동으로 생성되는 객체를 포함하는데, 이 동반 객체도 자신 만의 자동으로 생성된 메소드를 가지고 있다.

- 케이스 클래스는 생성된 데이터 기반 메서드가 주어졌을 때 데이터를 저장하는데 사용되는 클래스인 데이터 전송 객체를 잘 지원한다.
- 데이터 저장소 용도로써 케이스 클래스가 더 적합하며, 대부분의 함수를 작성할 때는 클래스 보다 객체가 더 적합하다고 볼 수 있다.

### Trait

다중 상속이 가능하게 하는 클래스 유형 중 하나

- 다른 유형과 달리 트레이트는 인스턴스화 될 수 없다

- 타입 매개변수를 취할 수 있어서 재사용성이 뛰어나다
- 이론적으로는 다중 상속을 지원하더라도, 실제 컴파일러는 클래스와 트레이트의 긴 한 줄 짜리 계층 구조를 만들기 위해 각 트레이트의 사본을 만든다.
- 상속되 클래스와 트레이트의 수평적인 리스트를 받아서 한 클래스가 다른 클래스의 확장하는 수직적 체인으로 재구성하는 절차를 선형화라고 한다

### sealed

sealed라는 modifier를 붙인 class는 선언된 파일 안에서만 상속 받을 수 있다.

- 다른 파일에서는 사용할 수는 있지만 상속 받으려고 한다면 컴파일 에러가 발생한다.

## Future

동시성을 위해서 사용된다.

## Monad

모나드는 다른 타입의 인자를 받는 것이다

```Scala
case class Boxed[T] (value: T)
```

일반적인 함수 조합은

- A => B => C 이므로 A 데이터로 부터 C라는 결과를 얻는다

이때 Option 등으로 감싸고 같은 행동읗 한다.

- A => T[B]
- B => T[C]
- 이 과정은 묶일수 없다.
- 이 묶인 것을 풀어주기 위한 연산이 필요하다 -> flatMap

Monad는 어떤 값을 감싸는 Wrapper인데, 그 중에서도 위 3개의 Laws를 만족해야만 Monad가 된다.

1. Associativity: m flatMap f flatMap g == m flatMap (x => f(x) flatMap g)
2. Left Unit: unit(x) flatMap f == f(x)
3. Right Unit : m flatMap unit == m

### implicit

암시적 변환이라는 뜻이다

- 암시적으로 적용되는 변환을 목적으로 자동적으로 사용됩니다

1. 표시규칙: implicit 로 표시한 정의만 검토 대상이 된다.
2. 스코프 규칙 : 삽입할 implict 변환은 스코프 내에 단일 식별자로만 존재하거나, 변환의 결과나 원래 타입과 연관이 있어야 한다
3. 한번에 하나만 규칙 : 오직 하나의 암시적 선언만 사용한다.
4. 명시성 우선 규칙: 코드가 그 상태 그대로 타입 검사를 통과 한다면  암시를 통한 변환을 시도치 않음

유사하다고 생각되는 변수를 찾아서 직접 사용을 한다.

## Slick

Scala Language-Intergrated Connection Kit(Reactive Functional Relational Mapping for Scala)

- Scala는 Java와 호환 되므로 JDBC 라이브러리를 이용해서 DB 접속, 쿼리 수행 가능
- 함수형 언어에서 함수 값으로 데이터를 다뤄야 할 일이 많기 때문에 코딩이 편해진다.
