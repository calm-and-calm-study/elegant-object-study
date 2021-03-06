# 내용 정리

- 프로퍼티가 없는 클래스는 객체지향 프로그래밍에서 악명이 높은 정적 메서드(static method)와 유사하다.
- 순수한 OOP에는 정적 메서드가 존재하지 않는다.
- 어떤 클래스의 인스턴스를 생성하고 이 인스턴스를 통해 시스템 클럭을 얻어야 한다.
- 객체가 ‘무(nothing)’이 아니면 무언가를 캡슐화해야 한다.
- 어떤 일을 수행하는 객체는 다른 객체와 공존하면서 이를 사용한다.
- 이 객체는 자기 자신을 식별할 수 있도록 다른 객체들을 캡슐화해야 한다.
- 캡슐화된 상태는 세계 안에서 객체의 위치를 지정하는 고유한 식별자이다.

# 느낀점

이 절을 읽으면서 캡슐화에 대해 생각해 보았다. 객체 내부의 객체를 가지며 그 객체가 객체를 식별하기 위한 상태 혹은 식별자가 되는 것이다. 따라서 이 객체를 식별할 수 있는 상태를 만들어줘야 하는데, 이는 생성자를 통해서 만들어주는 것이다. 이유는 객체는 객체와 서로 협응을 하는 것이 OOP의 목적이기도 하는데, 서로 어떤 객체인지 식별할 수 있어야한다는 의미라고 생각한다.

또한 이 절에서 정적 메서드를 엄격하게 배제하려고 한다. 정적 메서드는 객체의 생성(인스턴스 생성)이 없이 사용하는 기능이기 때문에 이전에 언급했던 연결장치에 가까운 객체가 될 것 같아서 배제하는 느낌이 든다.
