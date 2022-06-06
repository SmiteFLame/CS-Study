# 함수형 프로그래밍

오직 순수 함수만들 이용해서 부수 효과가 없는 함수들로만 구축 한다는 것이다.

- 부수효과: 그냥 결과를 돌려주는 것 이외의 어떤 일을 수행하는 함수를 가리켜 부수 효과가 있는 함수라고 칭한다

  - 변수를 수정
  - 자료 구조를 제자리에서 수정
  - 객체의 필드를 선정
  - 예외를 던지거나 요류를 내면서 실행을 중단
  - 콘솔에 출력하거나, 사용자의 입력을 읽음
  - 파일에 기록하거나 파일에서 읽어드린다.
  - 화면을 그린다.

- 함수형 프로글밍은 우리가 프로그래밍을 작성하는 방식에 대한 제약이지 표현 간으한 프로그램의 종류의 제약이 아니다.
- 순수 함수들로 프로그램을 작성하면 모듈성이 증가하기 때문인다

## 예제

### 부수효과 존재하는 프로그램

```Scala
class Cafe{
    def buyCoffee(cc: CreditCard): Coffee = {
        val cup = new Coffee()
        cc.charge(cup.price)    // 부수 효과: 신용카드를 실제로 청구한다.
        cup
    }
}
```

- 신용 카드 청구에는 외부 세계와의 일정한 상호작용이 관여 한다.
- 신용카드 거래에 대한 트랜잭션을 승인하고, 대금을 청구하고, 참조를 위해 거래 기록을 영구적으로 기록하는 등의 작업을 필요하다
- 하지만, 결과를 다시 돌려주는 것은 Coffee 객체이다.
- 그 외의 모든 동작들은 부수적으로 일어난다.

```Scala
class Cafe{
    def buyCoffee(cc: CreditCard, p: Payments): Coffee = {
        val cup = new Coffee()
        p.charge(cc, p.price)
        cup
    }
}
```

- 여전히 부수 효과는 발생하지만 검사성은 높아졌다.
- payment를 하나의 인터페이스를 만들고 모의 구현을 작성하면 검사를 할 수 있다.

### 부수효과 제거

청구 건을 하나의 값으로 돌려주게 하는 것이다.

```Scala
class Cafe{
    def buyCoffee(cc: CreditCard): (Coffee, Charge) = {
        val cup = new Coffee()
        (cup, Charge(cc, cup.price))
    }
}
```

- 생성 문제건이 아니라 처리 또는 연동 문제가 분리 되었다.
- buyCoffee 함수는 이제 여러 잔의 커피를 한 번의 거래로 구매하기 위해 이 함수를 재 사용하기 쉬어진다.

```Scala
cass class Charge(cc: CreditCard, amount: Double){
    def combine(other: Charge): Charge =
        if (cc == other.cc)
            Charge(cc, amount + other.amount)
        else
            throw new Exception("Cant combine charges to different cards")
}
```

```
class Cafe{
    def buyCoffee(cc: CreditCard): (Coffee, Charge) = {
        val cup = new Coffee()
        (cup, Charge(cc, cup.price))
    }

    def buyCoffees(cc: CreditCard, n: Int) : (List[Coffee], Charge) = {
        val purchases: List[(Coffee, Charge)] = List.fill(n)(buyCoffee(cc)) // x의 복사본 n개로 이루어진 List를 생성
        val (coffees, charges) = purchases.unzip                            // unzip은 쌍들의 목록을 목록들의 쌍으로 분리한다.
        (coffees, charges.reduce((c1,c2) => c1.combine(c2)))                // 한 번에 처욱건 두개를 combine을 이용하여 하나의 결합하는 과정을 반복함으로써 하나의 청구건으로 만든다.
    }
}
```

- buyCoffee를 재사용함으로써 사용할 수 있다.
- 두 함수 모두 Payments 인터페이스를 복잡한 모의 구현을 정의하지 않고도 쉽게 검사할 수 있다.

## 순수 함수

- 부수효과가 없는 함수
- 즉, 항상 같은 값만 돌려주는 함수
- 순수 함수의 이러한 개념을 참조 투명성이라고 한다.

- 참조 투명성: 모든 프로그램 p에 대해서 표현식 e의 모든 출현을 e의 평가 결과로 치환해도 p의 의미에 아무 영향이 미치지 않는다면, e는 참조에 투명하다
- 순수성: 만일 표현식 f(x)가 참조에 투명한 모든 x에 대해 참조에 투명하다면 함수 f는 순수하다.

## 참조 투명성, 순수성, 그리고 치환 모형

참주 투명성: 함수가 수행하는 모든 것이 함수가 돌려주는 값으로 대표된다는 불면 조건을 강제 한
