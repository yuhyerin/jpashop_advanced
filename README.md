# 템플릿 메서드 패턴 / 전략 패턴 정리!

## 들어가기 전에... 디자인 패턴이란?
처음 디자인 패턴을 공부할 때는, 단순히 아키텍처? 코드의 모양? 형태? 라고 생각했다. <br/>
그래서 a 패턴은 A 구조, b 패턴은 B 구조.. 이런식의 암기를 하려고 했다. <br/>
하지만 사실 겉보기엔 비슷해 보이는 구조들이 존재하고..모호하다. 실제로 왜 이런 구조가 쓰여야 하는지에 대한 이해가 부족했다.

### 디자인 패턴의 가장 큰 차이는 "의도" 이다.
- GOF 디자인 패턴에서 정의한 각 패턴들의 "의도"를 정확히 파악해야 한다.
> 템플릿 메서드 패턴 : 작업에서 알고리즘의 골격을 정의하고, 일부 단계를 하위 클래스로 연기한다. 템플릿 메서드를 사용하면 하위 클래스가 알고리즘의 구조를 변경하지 않고도 알고리즘의 특정 단계를 재정의 할 수 있다.

> 전략 패턴 : 알고리즘 제품군을 정의하고, 각각을 캡슐화 하여 상호 교환 가능하게 만들자. 전략을 사용하면 알고리즘을 사용하는 클라이언트와 독립적으로 알고리즘을 변경할 수 있다. 

## 1. 템플릿 메서드 패턴
- 의도 : 코드의 변하는 부분과 변하지 않는 부분을 분리하여 단일 책임 원칙을 높여서 변경 지점을 한곳으로 모아 변경에 쉽게 대처할 수 있는 구조를 만든다.
- 구조
  - 부모 : 추상 클래스
    - 코드의 변하지 않는 부분을 추상 클래스 내에 메서드에 정의한다. (알고리즘의 골격을 정의함. = 템플릿)
    - 코드의 변하는 부분은 추상 메서드로 정의해 놓음. (자식 클래스가 구현하도록 강제함)
  - 자식 : 부모 클래스를 상속하여 추상 메서드를 오버라이딩 한다.
    - 상속과 오버라이딩을 통한 다형성으로 알고리즘 전체 구조를 변경하지 않고 특정 부분만 재정의 할 수 있게 된다.
- 단점
  - 자식은 부모 클래스의 기능을 딱히 사용하지도 않는데, 불필요하게 자식이 부모를 의존하는 관계가 생긴다. 
  - 그로 인해 부모를 수정할 경우 자식에게 영향이 간다.
  - 상속 구조를 갖게 되면서 불필요한 강한 결합을 가지 게되는 문제를 해결하기 위한게 다음의 전략 패턴이다.

## 2. 전략 패턴
- 의도 : 템플릿 메서드 패턴과 마찬가지로 코드의 변하지 않는 부분과 변하는 부분을 분리하고자 한다.
- 구조
  - Context : 클래스 (변하지 않는 템플릿 역할)
    - 변하지 않는 부분을 클래스 내에 메서드에 정의한다. (알고리즘의 골격을 정의)
    - 생성자를 통해 Strategy 타입으로 전략을 주입받는다. or 전략을 바로 메서드의 파라미터로 전달받을 수 도 있다.
  - Stratey : 인터페이스 (변하는 알고리즘 역할)
    - Strategy 에 정의된 메서드를 구현체에서 정의한다. (변하는 부분을 구현)
  - 장점
    - Context 는 Strategy 인터페이스와만 의존관계를 갖기 때문에 Context 를 수정하더라도, Strategy 인터페이스 구현체들에는 영향이 없다. (템플릿 메소드 패턴과 다른 점)
    - 반대로 Strategy 인터페이스의 구현체들을 수정하거나, 새로운 구현체를 생성하더라도 Context 클래스에는 영향이 없다.
  
