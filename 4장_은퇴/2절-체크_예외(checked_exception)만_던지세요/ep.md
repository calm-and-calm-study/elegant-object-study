# 내용 정리

- 체크 예외(checked exception)와 언체크 예외(unchecked exception)
- 대부분의 객체지향 언어들은 언체크 예외만을 제공하지만 Java는 두 종류의 예외를 제공한다.
- 언체크 예외를 사용하는 것은 실수이며 모든 예외는 체크 예외여야 한다.
- 자바의 throws 처럼 메서드에 발생할 수 있는 예외를 시그니처에 throws CheckedException을 선언함으로써 문제를 처리할 책임을 호출하는 쪽으로 넘긴다. 이렇게 책임을 클라이언트로 전파하면서(excalating) 객체가 제 자신이 ‘안전하지 않다'고 선언할 수 있다.
- 체크(checked) 예외를 잡기 위해 체크 예외는 항상 가시적인(visible) 이유가 있다. 만일 예외가 없다면 우리는 해롭고 안전하지 않은 메서드를 다루고 있는 것이다.
- 대조적으로 언체크(unchecked) 예외는 무시할 수 있으며 예외를 잡지 않아도 무방하다. 언어가 예외처리를 강조하지 않는다. 체크 예외는 항상 가시적이지만 언체크 예외는 공개적이지 않다.

## 꼭 필요한 경우가 아니면 예외를 잡지 마세요

- 메서드를 설계할 때 모든 예외를 잡아서 메서드를 ‘안전하게' 만들지 아니면 상위로 문제를 전파할지는 명확하게 선택해야 한다.
- 모든 catch 문에는 납득할 수 있는 이유가 있어야 한다. 반드시 예외를 잡아야 하는 이유가 있거나 다른 선택의 여지가 없는 경우가 아니라면 예외를 잡아서는 않는다.
- 이상적인 설계에서는 각 애플리케이션의 각 진입점 별로 하나의 catch 문만 존재해야 한다.
    - 불행하게도 Java 등의 다른 프레임워크는 이러한 아이디어가 기반이 아니기 때문에 이 방식이 가능한 경우는 거의 없다.
- 문제가 발생한 장소에서 문제를 해결해서 소프트웨어를 견고하게 만드는 철학은 코드 전체를 유지보수하기 어렵고 불안정하게 만든다.
- 메서드가 checked 예외를 이유없이 처리해버리면 그 메서드는 클라이언트를 무시해버린채 정해진 정보를 은폐하고 에러상황을 무시해버린다. 그러면 어떤 에러가 발생했는지 우리는 알아채리지 못한채 디버깅에 시간을 쏟을 것이다. 이런 접근 방법은 ‘흐름 제어를 위한 예외 사용(using exceptions for flow control)’이라고 부른다.
- 예외는 분기를 처리할 목적으로 설계되지 않았다. 오퍼레이션의 정상적인 흐름을 종료시키고 추가적인 조치를 필요로 하는 심각하고 복구 불가능한 상황을 나타내기 위해 설계되었다. 예외처리로 -1를 반환하는 경우가 있는데 이러한 경우에는 반환값을 매번 확인할 수 밖에 없다. 즉, 객체가 원하는 반환값을 주지 않은 ‘배신 행위'나 다름없다. 그리고 문제가 발생했을 때 원인을 파악하기가 매우 어려워진다.
- 요즘은 예외를 잡아 상황을 ‘구조'하는 일은 정당한 이유가 있을 경우에만 용인되는 중요한 행동이다.
- 잡아서 로깅하기(catching and logging)은 끔찍한 안티패턴이다.

## 항상 예외를 체이닝하세요

- ‘예외 되던지기(rethrowing)’은 예외를 잡은 동시에 새로운 예외를 던진다. 이와 같은 ‘예외 체이닝(exception chaining)’은 훌륭한 방법이다.
- 문제를 발생시켰던 낮은 수준의 근본 원인(root cause)을 소프트웨어의 더 높은 수준으로 이동시켰다는 점이다.
- 항상 예외를 체이닝하고 절대로 원래 예외를 무시하면 안된다. 모든 예외를 잡아 체이닝하고 다시 던져야 한다.

## 단 한번만 복구하세요

- 예외 후 복구는 ‘흐름 제어를 위한 예외 사용(using exceptions for flow control)’으로 알려진 안티패턴의 또 다른 이름이다.
    - 빠르게 실패하기 진영에 속한다면 예외 후 복구를 적용할 수 없다. 빠르게 실패하기는 복구라는 개념 자체가 존재하지 않는다.
- 모든 메서드가 예외를 던진 후 해당 예외를 잡아서는 안된다. 모든 예외는 애플리케이션의 가장 높은 곳까지 전파될 것이다. 실제로는 하나가아니라 몇 개의 지점이 있을 것이다. 여기서 지점이란 애플리케이션과 커뮤니케이션하는 진입점을 의미한다.
- 가장 높은 지점인 main에서 예외를 잡는 것이 가장 적절한 위치이다. 복구하기에 적합한 유일한 장소이다. 모든 진입점에서 동일한 작업이 수행돼야 한다. 하지만 이게 좋은 방법이 아니다. 항상 예외를 체이닝하고 다시 던지고 최상위 수준에서 한번만 복구해야한다.

## 관점-지향 프로그래밍을 사용하세요

- 가끔은 실패한 오퍼레이션을 재시도할 필요가 있다.
- 재시도를 위해서는 예외를 잡아서 복구하고 최대 횟수만큼 재시도를 해야한다.
- 메서드는 안전하지 않지만 즉시 불안정해지지 않는다.
- 관점-지향 프로그래밍(aspect-oriented programming, AOP)이라는 기법이 있다. AOP는 단순하면서도 강력한 프로그래밍 패러다임으로 OOP와도 궁합이 잘 맞는다. 전형적인 연산을 크게 단순화시키고 OOP로 작성한 코드의 장황함을 제거할 수 있는 기본적인 기법이다.
- 실패 재시도를 ‘관점(aspect)’ 이라고 부른다. 핵심 클래스로부터 덜 중요한 기술과 매커니즘을 분리해서 코드 중복을 제거할 수 있기 때문이다. 사용하는 언어와 무관한게 AOP에 관해 더 많이 이해하고 프로젝트에 사용할 것을 적극 추천한다.
- OOP의 코드를 깔끔한 상태로 유지하기 위해 AOP를 적용할 수 있는 현실적이면서도 실용적인 예이다.

## 하나의 예외 타입만으로도 충분합니다

- ‘절대 복구하지 않기'와 ‘항상 체이닝하기'에 설명한 내용을 동의한다면 예외 탕비이 중복기능(redundant feature)인 이유를 이해할 수 있다. 단 한번만 복구한다면 어떤 예외라도 담을 수 있는 예외 객체만 있으면 된다.
- 사실 단 한번만 복구한다면 어떤 예외라도 담을 수 있는 예외 객체만 있으면 된다. 올바르게 예외를 체이닝했다면 예외의 타입을 알 필요가 없다. 예외는 오직 체이닝한 후 다시 던지기 위할뿐이다.

# 느낀점

- 모든 대다수의 언어의 흐름과 정 반대의 내용이다. 대다수의 개발자들은 체크드 예외를 던지는 기능에 큰 불만을 느끼고 있으며 언체크드 예외만 처리하는 것이 옳다고 전해진다. 코틀린도 자바와 달리 체크 예외를 처리하지 않는데 그 이유는 아래 이유와도 같다.

![코틀린 공식 문서](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/97eba2aa-8e36-43a7-8bf2-ea5916216bff/Untitled.png)

코틀린 공식 문서

- 다양한 예외에 대한 처리 방법을 보여줘서 꽤나 실용적인 챕터였다. 우리는 보통 빠르게 실패하기를 통해 예외를 발생하고 그 예외를 AOP를 이용해서 핸들링한다. 빠르게 실패하기와 체이닝하기, AOP의 합작으로 최적화된 시스템이라고 생각을 한다.
