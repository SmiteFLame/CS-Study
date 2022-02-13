# Reactive Programming

데이터가 통지될 때 마다 관련 프로그램이 반응(Reactive)해 데이터를 처리하는 프로그래밍 방식

- 데이터스트림: 데이터를 한 번에 보내지 않고 각각의 데이터가 생성될 때 마다 순서대로 보낸다

- 데이터 스트림으로 데이터를 전달받은 프로그램이 그 때 마다 적절히 처리할 수 있게 구성
- 즉, 프로그램이 필요한 데이터를 직접 가져와 처리하는 것이 아니라 보내온 데이터를 받은 시점에 반응해 이를 처리하는 프로그램을 만드는 것
  - 데이터가 변경이 될때 마다 바로 반영이 되는 것
- 리액티브 프로그래밍에서 데이터를 생산하는 측은 데이터를 전달하는 것 까지 책임을 진다.

  - 데이터를 소비하는 측의 처리를 기다릴 필요가 없다.
  - 데이터를 통지한 후 데이터를 소비하는 측에서 데디터를 처리하는 도중이라도 데이터를 생산하는 측은 바로 다음 데이터 처리 가능

  - 리액티브 시스템은 리액티브 프로그래밍과 전혀 다름
    - 리액티브 시스템: 메시지를 보내 데이터를 처리하고 상황에 따라 Scale out, Scale in 을 자동으로 수행하는 시스템

## RxJava

자바에서 리액티브 프로그래밍을 구현하는 라이브러리

1. Observer 패턴을 잘 확장했다.

- Observer 패턴: 감시 대상 객체의 상태가 변하면 이를 관찰하는 객체에 알려주는 구조
- 데이터 생성하는 측과 데이터를 소비하는 측으로 나눌 수 있어서 데이터 스트림을 처리할 수 있다.
- RxJava는 옵저버 패턴에 완료와 에러 통지를 할 수 있어서 모든 데이터 통지가 끝나거나 에러가 발생하는 시점에 별도로 대응 가능

2. 쉬운 비동기 처리

- Reactive 규칙의 근간이 되는 Observable 규약이라는 RxJava 개발 가이드 라인을 따른 구현이라면 직접 스레드를 관리하는 번거로움에서 해방된다.
- 동기 처리나 비동기 처리나 구현 방법에 큰 차이가 없다.

3. 함수형 프로그램밍의 영향을 받았다.

- 함수형 인터페이스를 인자로 전달받는 매서드를 사용해 대부분의 처리를 구현한다.
- 입력과 결과만 정해져 있다면 구체적인 처리는 개발자에게 맡길 수 있으므로 자유로운 구현이 간으하다.

## Reactive Stream

라이브러리나 프레임 워크에 상관 없이 데이터 스트림을 비동기로 다룰 수 있는 공통 매커니즘

### Reactive Stream의 구성

- Publisher(생산자): 데이터를 만들어 통지
- Subscriber(소비자): 데이터를 받아 처리하는 소비자

Subscriber가 Publisher를 구독(Subscribe)하면 Publisher가 통지한 데이터를 Subscriber가 받을 수 있다.

1. Publisher는 통지 준비가 끝나면 Subscriber에 통지(onSubscribe)한다.
2. 해당 통지를 받은 Subscriber는 받고자 하는 데이터 개수를 요청, 요청하지 않으면 Publisher는 계속 기다리게 된다.
3. Publisher는 데이터를 만들어 Subscriber에 통지(onNext) 한다.
4. 데이터를 받은 Subscriber는 받은 데이터를 사용해 처리 작업을 수행한다.
5. Publisher는 요청 받은 만큼의 데이터를 통지한 뒤 subscriber로 부터 다음 요청이 올때 까지 데이터 통지를 중단한다.
6. 이후 Subscriber가 처리 작업을 완료하면 다음 받은ㄹ 데이터 개수를 요청한다.
7. Publisher는 Subscriber에 모든 데이터를 통지하고 마지막으로 데이터 전송이 완료되었다고 통지(onCompelete)한다.
8. 완료 통지를 하고 나면 Publisher는 이 구독 건에 대해 어떤 통지도 하지 않는다.

- 데이터 개수를 요청하는 이유: Publisher가 통지하는 데이터 개수를 제어하기 위해
- Publisher와 Subscriber의 처리가 각각 다른 스레드에서 진행되는데 Publisher의 통지 속도가 빠르면 Subscriber가 소화할 수 없으므로

### 프로토콜

1. onSubscribe: 데이터 통지가 준비 됐음을 통지
2. onNext: 데이터 통지
3. onError: 에러(이상 종료) 통지
4. onComplete: 완료(정상 종료) 통지

### 인터페이스

1. Publisher: 데이터를 생성하고 통지하는 인터페이스
2. Subscriber: 통지된 데이터를 전달받아 처리하는 인터페이스
3. Subscription: 데이터 개수를 요청하고 구독을 해지하는 인터페이스
4. Processor: Publisher와 Subscriber의 기능이 모두 있는 인터페이스

### Subscription

Publisher와 Subscriber가 사용하는 Subscription은 통지 받을 데이터 개수를 지정해 데이터 통지를 요청하거나 해지할 때 사용하는 인터페이스

## Reactive Streams 규칙

1. onSubscribe는 해당 구독에서 한 번만 발생한다.
2. 통지는 순차적으로 이루어 진다.
3. null을 통지하지 않는다.
4. Publisher의 처리는 완료(onComplete) 또는 에러(onError)를 통지해 종료한다.

Subscription의 규칙

1. 데이터 개수 요청에 Long.MAX_VALUE를 설정하면 데이터 개수의 의한 통지 제한은 없어진다.
2. Subscription의 메서드는 동기화 된 상태로 호출해야 한다.

## RxJava

### 기본 구조

데이터를 만들고 통지하는 생산자와 통지된 데이터를 받아 처리하는 소비자로 구성된다.

- 생산자를 소비자가 구독해 생산자가 통지한 데이터를 소비자가 받게 된다.
- Reactive Streams 지원
  - 생산자: Flowable
  - 소비자: Subscriber
  - 기본적인 매커니즘은 Reactive Streams와 같다
    - Flowable로 구독 시작, 데이터 통지, 에러 통지, 완료 통지를 하게 된다.
- Reactive Streams 미지원
  - 생산자: Observable
  - 소비자: Observer
  - RxJava 2.x 버전의 Obserable과 Observer는 Reactive Streams를 구현하지 않아서 Reactive Streams 인터페이스를 사용하지 않는다.
  - 기본적인 매커니즘은 거의 같다
  - 데이터 개수를 제어하는 배압 기능이 없기 때문에 데이터 개수를 요청하지 않는다
  - Subscription을 사용하지 않고 Disposable이라는 구독 해지 메서드가 있는 인터페이스를 사용하게 된다.
    - dispose: 구독을 해지 한다.
    - isDisposed: 구독을 해지하면 true, 해지하지 않으면 false를 반환한다.
  - 데이터를 교환할 때 데이터 개수를 요청하지 않고 바로 Observer에 통지된다.

### 연산자

RxJava에서는 생산자(Flowable/Ovservable)가 통지한 데이터가 소비자(Subscriber/Observer)에 도착하기 전에 불필요한 데이터를 삭제하거나 소비자가 사용하기 쉽게 데이터를 변환하는 등 통지하는 데이터를 변경해야 할 때가 있다.

통지하거나 데이터를 생성하거나 필터링 또는 변환하는 메서드를 연산자 라고 한다.

- 연산자를 연결해 나감으로써 최종 통지 데이터의 단순한 처리를 단계적으로 설정할 수 있다.

메서드 체인

1. 인자듸 데이터를 왼쪽부터 순서대로 통지하는 Flowable을 just 메서드로 생성한다.
2. filter 메서드는 Flowable이 통지하는 데이터를 1건 씩 받아 해당 데이터를 통지한다면 true를 반환하고, true인 데이터를 통지하는 Flowable을 생성한다.
3. map 메서드는 Flowable이 통지하는 데이터를 1건씩 받아 이를 변환해 통지하는 Flowable을 생성한다. 여기서는 data \* 100 계산식으로 전달받은 데이터의 100배를 전달한다.

```
public static void main(String[] args){
  Flowable<Integer> flowable =
    Flowable.just(1,2,3,4,5,6,7,8,9,10) // 1
      .filter(data -> data % 2 == 0)    // 2
      .map(data -> data * 100)          // 3

  // 구독해서 받은 데이터를 출력
  flowable.subscribe(data -> sout(data));
}
```

- 데이터를 메서드 체인에 통과하게 해 Flowable/Observable이 통지하는 데이터를 최종으로 어떤 데이터를 통지할 것인지를 제어할 수 있다.
- RxJava는 함수형 프로그래밍의 영향을 많이 받아 메서드 대부분이 함수형 인터페이스를 인자로 받는다.
  - 함수형 인터페이스의 구현은 함수형 프로그래밍의 원칙에 따라 같은 입력을 받으면 매번 같은 결과를 반환한다.
  - 기본으로 그 입력값과 처리는 외부 객체나 환경에 의해 변화가 일어나지 않는다.
- 부가 작용: 전달받은 데이터의 상태를 변경하거나 처리 작업의 외부에 어떤 변화를 주는 것
  - 부가 작용이 발생하는 처리작업은 객체의 상태를 변경해 외부에서도 참조 가능한 객체에 어떤변화를 주거나 파일이나 데이터베이스를 변경하는 것을 말한다
  - 외부의 상태 변경이 데이터 통지 처리에 영향을 주는 것을 피하지 않으면 책임 범위가 넓어져 단순한 처리라도 관리가 어렵다.
  - RxJava에서는 기본으로 부가 작용이 발생하는 처리는 메서드 체인 도중이 아니라 최종으로 데이터를 받아 처리하는 소비자 측에서 일우저 지는 것이 좋다.
  - 함수형 인터페이스 처리에 대해 부가 작용이 발생하지 않으면 여러 스레드에서 공유하는 객체가 없어서 스레드 안전을 보장할 수 있다.

```
// 인자로 데이터를 직접 지정하면 지정한 시점에 평가된 값을 받게 된다.
// 아래는 Flowable을 생성하면 생성된 시점의 시스템 시작을 통지한다.
Flowable<Long> flowable = Flowable.just(System.currentTimeMillis());


// 함수형 인터페이스를 메서드의 인자로 지정하면 메서드가 처리하는 시점에 정의된 실행해 값을 가져온다.
Flowable<Long> flowable = Flowable.fromCallable(() -> System.currentTimeMillis());
```

- just 메서드는 생성한 Flowable은 여러 번 구독해도 같은 값을 통지
- Callable 메서드에서 생성한 Flowable은 구독할 때 마다 다른 값을 통지한다.

### 비동기 처리

처리 범위를 분리할 수 있게 설계 되어 잇어 서로 다른 스레드에서 실행할 수 있다.

- 데이터를 통지하는 측이 무엇을 하더라도 데이터를 받는 칙에서 데이터에 의해서만 바뀌게 된다면 비동기로 쉽게 전환할 수 있다.
- RxJava에서는 개발자가 직접 스레드를 관리하지 않게 각 처리 목적에 맞춰 스데르를 관리하는 스케줄러 제공
- 스케줄러: 데이터를 생성해 통지하는 부분과 데이터를 받아 처리하는 부분을 지정할 수 있다.
  - 생산자: 생성자 메서드에서 생성한 Flowable/Observalbe이 데이터 통지를 어떤 스캐줄러에서 처리할지를 제어한다.
  - 소비자: 데이터의 필너타 변환하는 메서드와 소비자의 데이터의 수신 처리를 어느 스케줄러가 할지 제어한다.

중요한 것은 데이터 통지하는 쪽과 받는 측은 통지시에만 데이터를 주고 그 외의 요인은 서로의 행동에 영향으 주지 않아야 한다.

- 생산자와 소비자 사이에서 이루어지는 처리를 외부 변수를 참조해 바꾸면 비동기 처리에 영향을 주게된다.
- 비동기 처리할 때는 생산자에서 소비자까지의 처리가 노출되지 않게 폐쇄적으로 개발하면 어느 정도 위험을 줄일 수 있다.

### Cold 생산자, Hot 생산자

- Cold 생산자: 1개의 소비자와 구독 관계를 맺는다.
  - Cold 생산자가 통지하는 데이터의 타임라인은 구독할 때 마다 생성된다
- Hot 생산자: 여러개의 소비자와 구독 관계를 맺는다

  - Hot 생산자는 이미 생성한 데이터의 타임라인에 나중에 소비자가 참가하는 것을 허용한다

- RxJava에서 생성 메서드로 생성된 생성자는 기본으로 Cold 생산자이다.
- Hot 생산자르 생성하려면 Cold 생산자에서 Hot 생산자로 변환하는 메서드를 호출하거나 뒤에서 Processor와 Subject를 생성해야 한다.

### ConnectableFlowable, ConnectableObservable

ConnectableFlowable, ConnectableObservable은 Hot Flowable, Observable이며, 여러 Subscriber/Observer에서 동시에 구독할 수 있다.

- Cold와 달리 subscribe 메서드를 호출해도 처리를 시작하지 않고 connect 메서드를 호출해야 처리를 시작하다
- 처리를 시작하기 전에 여러 Subscriber/Observer에서 구독하게 하고 그 후에 처리해 처음 부터 동시에 여러 구독자에게 데이터를 통지할 수 있다.

- refCount: ConnectableFlowable, ConnectableObservable에서 새로운 Flowable, Observable을 생성한다

  - Flowable, Observable은 이미 다른 소비자를 구독하고 있다면 도중에 구독하더라도 같은 타임라인에서 생성되는 데이터를 통지한다.
  - refCount 메서드에서 생성한 Flowable, Observable는 더이상 ConnectableFlowable, ConnectableObservable이 아니므로 connect 메서드가 없다

- autoConnect: ConnectableFlowable, ConnectableObservable 지정한 개수의 구독이 시작된 시점에 처리하는 Flowable, Observable 생성
  - autoConnect 메서드에서 인자 없이 생성하면 처음 subscribe 메서드가 호출된 시점에 처리를 시작
  - autoConnect 메서드에서 인자를 구독 개수를 지정한다면 지정한 개수에 도달한 시점에서 처리를 시작한다
