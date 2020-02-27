# DependancyInjection_trans
위키백과의 Dependency injection 번역


소프트웨어공학에서, 의존주입(dependency injection)은 한 객체가 다른 객체에 의존할 때 쓰이는 기술이다. "의존"은 [서비스](http:// "소프트웨어설계 관점에서, 서비스에 기반한 설계. 서비스란 서로다른 목적을 가진 클라이언트들이 사용할 수 있는 기능 또는 그 기능의 모음이다, 사용량은 제한가능 해야함.")의 예로 사용될 수 있다. 클라이언트가 어떤 서비스를 사용할지 정하는 대신에, 클라이언트에게 무슨 서비스를 사용할지 묻는다. "의존"은 그 의존성(서비스)을 사용할 객체([클라이언트](http:// "클라이언트는 서버에서 제공하는 서비스에 접근하는 컴퓨터 하드웨어 또는 소프트웨어이다. 서버는 클라이언트가 네트워크를 통해 서비스에 접근할 경우 또다른 하나의 컴퓨터일 수 있다."))에게 넘기는 것을 말한다. 서비스는 클라이언트의 [상태](http:// "information technology and computer science 에서 시스템은 상태값이 있는 것으로 묘사된다. 만약 유저 상호작용 또는 선진행된 이벤트를 기억하도록 설계했다면, 기억한 정보를 시스템상태값이라 부른다")의 한 부분이다. 클라이언트가 [서비스를 찾고](http:// "service locator pattern 은 하나의 디자인 패턴이고, 소프트웨어개발에서는 안티패턴이다. 서비스를 가져오는 과정을 추상화 레이어에 캡슐화하기 때문이다. 이 패턴은 요청이 있을 때 작업에 필요한 정보를 받는,  service locator 라고 알려져있다. 서비스를 찾는 것에 대한 가장 큰 비판은 의존관계를 감춘다는 것이다.") 빌드하는 대신 사용할 서비스들을 클라이언트에게 제공하는 것이 이 패턴의 기본개념이다.  

의존주입의 의도는 객체를 사용하거나 생성할 때 Separation of Concerns[^5]
[^5]: 컴퓨터이론에서, Soc(separation of concertns)는 프로그램을 섹션별로 나누는 방식에 대한 설계입니다. 그 대상은 프로그램 코드에 대한 것이고, 정확히는 시작할 클래스의 이름 입니다. Soc를 잘 구현한 프로그램을 모듈화된 프로그램이라 부릅니다. 모듈화 즉 클래스 분리는 잘 정의된 인터페이스 내에 캡슐화함으로써 이루어집니다. 캡슐화는 정보를 숨기는 것을 의미합니다. 계층화된 설계는 시스템정보에서 클래스 분리의 한 예이기도 합니다.
를 이루는 것이다.












