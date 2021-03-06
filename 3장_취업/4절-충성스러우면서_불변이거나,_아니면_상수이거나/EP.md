# 내용 정리

- 객체란 실제 엔티티(real-life entity)의 대표자(representative)입니다. 실제라는 말은 객체의 가시성 범위(scope of visibility) 밖에 존재하는 모든 것이다.
- 모든 객체는 식별자(identity), 상태(state), 행동(behavior)을 포함한다.
- 불변 객체와 가변 객체의 중요한 차이는 불변 객체에는 식별자가 존재하지 않으며 절대로 상태를 변경할 수 없다는 점이다. 불변 객체의 식별자는 객체의 상태와 완전히 동일하다.
- Java를 포함한 대부분의 OOP 언어에서는 상태가 동일하더라도 서로 다른 객체라고 판단한다. 각 객체는 재정의할 수 있는 유일한 식별자를 가지기 때문이다.
- 가변 객체는 완전히 다른 방식으로 동작한다. 가변 객체의 상태는 변경이 가능하기 때문에 상태에 독립적인 식별자를 별도로 포함해야 한다.
- 불변 객체는 실제 객체가 어디에 존재하고 어떤 방식으로 사용해야 하는지 알고 있다.
- 불변 객체는 자신이 대표하는 실세계의 엔티티에게 충성(loyal)한다. 어떤 경우에도 항상 동일한 엔티티를 대표한다.
- 불변 객체만을 이용해서 컬렉션을 구현할 수 있을까. 상수 리스트(constant list)로 구현하는 방법, 불변 리스트(immutable list)로 구현하는 방법이 있다.
    - ‘불변’ 대신 ‘상수(constant)’라는 용어를 사용하길 권장한다.
- 비즈니스 도메인과 기술 도메인에 무관하게 어떤 종류의 시스템이라도 불변 객체를 이용해서 설계될 수 있고 설계되어야 한다.

# 느낀점

- 가변 객체와 불변객체의 개념을 유연하게 사용해야 할 것 같다. 변경이 가능한 범위를 최소한으로 줄이고 변경이 되어야 하지 않는 상황에서는 불변객체를 오가면서 만들어야 한다.
- 코틀린에서는 불변객체, 가변객체의 구분을 명확하게 하고 있다. 따라서 최소한의 범위를 지정하고 그 변경 가능한 context를 완전하게 이해할 수 있게 만들어야 한다.
