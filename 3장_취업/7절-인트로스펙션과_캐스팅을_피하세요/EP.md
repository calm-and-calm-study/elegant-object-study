# 내용 정리

- 타입 인트로스펙션(introspection)과 캐스팅(casting)을 사용하고 싶은 유혹에 빠지더라도 절대로 사용해서는 안된다.
- 자바의 `instanceof` 연산자와 `Class.cast()` 메서드가 이 범주에 포함된다.
- 타입 인트로스펙션은 리플렉션(reflection)이라는 포괄적인 용어이다. 리플렉션을 사용하면 메서드, 명령어, 구문, 클래스, 객체, 타입 등을 변경할 수 있다.
- 이 접근 방법은 타입에 따라 객체를 차별하기 때문에 OOP의 기본 사상을 심각하게 훼손시킨다.
- 리플렉션은 객체를 차별한다.
- 런타임에 객체의 타입을 조사(introspect)하는 것은 클래스 사이에 결합도가 높아져 기술적인 관점에도 좋지 않다.
- instanceof 연산자를 사용하거나 클래스를 캐스팅하는 일은 안티패턴이다.
- 대부분의 OOP는 리플렉션과 함께 이런 기능을 제공하고 있지만 사용하지 않아야 한다.

# 느낀점

- 리플렉션, 타입 캐스팅에 대한 부정적인 견해다.
- 기본적으로 런타임시에 일어나는 상황은 우리가 예상하지 못한다. 따라서 런타임에서 에러가 날 지점들을 컴파일 에러로 가지고 오면 예상할 수 있게 되어 에러를 방지할 수 있다.
- 코틀린은 NPE를 컴파일 시점으로 최대한 가져왔다. QueryDSL은 SQL시 발생할 수 있는 에러를 컴파일 시점으로 가져왔다. 그와 반대되는 런타임 익셉션을 최대한 줄여가자.
