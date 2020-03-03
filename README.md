# DependancyInjection_trans
위키백과의 Dependency injection 번역


소프트웨어공학에서, 의존주입(dependency injection)은 한 객체가 다른 객체에 의존할 때 쓰이는 기술이다. "의존"은 [서비스](http:// "소프트웨어설계 관점에서, 서비스에 기반한 설계. 서비스란 서로다른 목적을 가진 클라이언트들이 사용할 수 있는 기능 또는 그 기능의 모음이다, 사용량은 제한가능 해야함.")의 예로 사용될 수 있다. 클라이언트가 어떤 서비스를 사용할지 정하는 대신에, 클라이언트에게 무슨 서비스를 사용할지 묻는다. "의존"은 그 의존성(서비스)을 사용할 객체([클라이언트](http:// "클라이언트는 서버에서 제공하는 서비스에 접근하는 컴퓨터 하드웨어 또는 소프트웨어이다. 서버는 클라이언트가 네트워크를 통해 서비스에 접근할 경우 또다른 하나의 컴퓨터일 수 있다."))에게 넘기는 것을 말한다. 서비스는 클라이언트의 [상태](http:// "information technology and computer science 에서 시스템은 상태값이 있는 것으로 묘사된다. 만약 유저 상호작용 또는 선진행된 이벤트를 기억하도록 설계했다면, 기억한 정보를 시스템상태값이라 부른다")의 한 부분이다. 클라이언트가 [서비스를 찾고](http:// "service locator pattern 은 하나의 디자인 패턴이고, 소프트웨어개발에서는 안티패턴이다. 서비스를 가져오는 과정을 추상화 레이어에 캡슐화하기 때문이다. 이 패턴은 요청이 있을 때 작업에 필요한 정보를 받는,  service locator 라고 알려져있다. 서비스를 찾는 것에 대한 가장 큰 비판은 의존관계를 감춘다는 것이다.") 빌드하는 대신 사용할 서비스들을 클라이언트에게 제공하는 것이 이 패턴의 기본개념이다.  

의존주입의 의도는 객체를 사용하거나 생성할 때 [Separation of Concerns](http:// "컴퓨터이론에서, Soc(separation of concertns)는 프로그램을 섹션별로 나누는 방식에 대한 설계입니다. 그 대상은 프로그램 코드에 대한 것이고, 정확히는 시작할 클래스의 이름 입니다. Soc를 잘 구현한 프로그램을 모듈화된 프로그램이라 부릅니다. 모듈화 즉 클래스 분리는 잘 정의된 인터페이스 내에 캡슐화함으로써 이루어집니다. 캡슐화는 정보를 숨기는 것을 의미합니다. 계층화된 설계는 시스템정보에서 클래스 분리의 한 예이기도 합니다.")
를 이루는 것이다. 이것은 가독성과 코드 재사용성을 높일 수 있다.

의존주입은 inversion of control 기술의 한 형태이다. 서비스들을 호출하는 클라이언트는 어떻게 그 서비스들이 생성되는지 알지 못합니다. 대신에, delegate 에 서비스를 제공할 코드 또는 injector를 제공합니다. 클라이언트는 injector 를 호출하지 못합니다; 서비스를 생성하는 injector를. injector는 이미 있거나 injector에 의해 생성된 서비스를 클라이언트에게 주입합니다. 그런 후에야 클라이언트는 서비스들을 이용합니다. 클라이언트는 injector 에 대해, 어떻게 서비스를 생성하는지 실제로 어떤 서비스가 사용되는지 따위를 알 필요가 없습니다. 클라이언트는 오직 서비스 인터페이스에 대해서만 알면 됩니다. 인터페이스에 클라이언트가 서비스를 어떻게 사용할지 정의되어 있기 때문입니다. 이것은 , 객체 "생성"의 책임으로 부터 "사용"의 책임을 분리합니다.

## Intent
의존주입은 다음과 같은 문제를 해결합니다.
* 어떻게 어플리케이션이나 클래스가 그것들의 객체 생성으로 부터 자유로울 수 있는가?
* 어떻게 서로다른 환경내에서 객체 생성 방법을 지정할 수 있는가?
* 어떻게 어플리케이션이 서로다른 환경을 지원할 수 있는가?

클래스 내에서 직접 객체들을 생성하는 것은 융통성이 없습니다. 왜냐하면 나중에 클래스와 떨어져서 생성할 수 없기 때문입니다. 다른 객체가 필요할 때 클래스를 재사용할 수 없고 테스트하기도 어렵게 만듭니다. 실제 데이터를 mock 객체로 대체할 수 없기 때문입니다. 

클래스는 더이상 객체가 필요할 때 그것을 생성할 책임을 가지지 않고, Abstract Factory 디자인 패턴과 같이 팩토리객체에 생성을 위임할 필요도 없습니다.

## Overview
의존주입은 클라이언트의 의존성 생성을 행위로 부터 분리합니다. 이것은 프로그램이 loosely coupled 될 수 있고, dependency inversion 과 single responsibility principles 를 따를 수 있게 됩니다. service locator pattern 과는 완전히 반대로 클라이언트가 시스템이 어떤 의존성을 찾는지 알게 됩니다.

기초적인 단위의 주입은 새로운 것이거나 특정한 메카니즘이 아닙니다. parameter passing 방식으로 모두 똑같이 작동합니다. 주입에서 paramter passing 은 클라이언트가 세부단계까지 관여할 필요가 없음을 말합니다.

주입은 또한 제어를 넘기는 것에 관한 것이고, 어떻게 독립적으로 이전할 것인지에 관한 것입니다, 참조 위치든 값이든 말이죠.

의존주입은 다음의 네가지 원칙을 따릅니다.
* service 객체 필요
* service 에 의존하는 client 객체 필요
* client 가 어떻게 서비스를 사용할지 정의된 interfaces
* 주입기(injector), 서비스를 생성하고 클라이언트에게 주입할 책임이 있는.

비유하자면,
* service - 전기, 가스, 하이브리드 또는 디젤 차
* client - 엔진에 상관없이 같은 방식으로 차를 운전하는 운전자
* interface - automatic방식, 운전자가 기어나 기타 엔진상세에 대해 이해하고 있을 필요가 없는.
* injector - 차를 사주고, 어떤 종류를 살지 결정하는 부모님

어떤 객체든 service 가 될 수 있다. 다른 객체를 이용하는 어떤 객체든 client 가 될 수 있다. 무슨 이름으로 하든 상관 없고 주입에서 어떤 역할을 하는지가 중요하다.

interfaces 는 클라이언트가 의존하는 타입이다. 클라이언트가 사용가능한 것이다. interface 는 서비스에 의해 구현된 말그대로의 interface 일 수도 있지만, 추상 클래스일 수도 있고 심지어 그 자체가 서비스 일 수도 있다, 마지막은 [DIP](http:// "dependency inversion principle") 를 위반하고 테스트하기 어려워지지만. 한가지 알아야할 것은, 클라이언트가 인터페이스가 어디에 있는지 모르기 때문에 인터페이스를 구체적으로 생성하거나 확장하지 말아야 한다. 

클라이언트는 인터페이스에 대한 구체적인 구현은 알지 못한다. 오직 아는 것은 인터페이스 이름과 API 이다. 클라이언트는 인터페이스가 무엇을 바꾸는지 알지 못해도 인터페이스를 바꿀 필요가 없다. 그러나 인터페이스가 클래스에서 인터페이스나 그 외의 것으로 refactoring 될 때에는 다시 컴파일 할 필요는 있다.(https://softwareengineering.stackexchange.com/q/257976). 만약 클라이언트와 서비스가 따로 배포되면 문제가 어렵다, 의존주입이 해결할 수 없는 관계이기 때문이다.

injector 는 클라이언트에게 서비스를 소개한다. 또는 종종 클라이언트를 만들기도 한다. injector 는 객체를 클라이언트화 하거나 나중에 다른 클라이언트를 위한 서비스로 다루면서 복잡한 객체간 관계를 가지기도 합니다. injector 는 클라이언트가 아닌 단지 서로 일하는 많은 객체들 일 수 있습니다. injector 는 다음과 같이 불리기도 합니다: assembler, provider, container, factory, builder, spring, construnction code 또는 main.

의존성주입은 규칙이 될 수도 있다, 모든 객체의 생성과 행위를 분리토록 요구하는. 객체 생성을 수행하는 DI 프레임워크 따르면 new 키워드 사용을 금지하거나 또는 덜 엄격하게, 오직 [value objects](http:// "컴퓨터이론에서, value object 는 작은 객체이다, 동일여부는 같은 값을 가질 때이고, 같은 객체이어야 함을 의미하지는 않는. ") 생성만 허락할 수 있다.

### Taxonomy
Inversion of control(IoC) 는 DI 보다 일반적이다. 간단히 말해, IoC 는 당신이 코드를 호출 하는 것이 아닌, 코드가 당신을 호출하게끔 하는것이다. [template method pattern](http:// "객체지향 프로그래밍에서, template method 는 Design Patterns 책에서 나오는 행위설계패턴중 하나 입니다. template method 는 추상화된 superclass 에 있는 메소드입니다. template method 로써 같은 파일내에 추가적인 helper mothod들을 구현합니다. ") 이  DI 뺀 IoC 이다. polymorphism 은 상속을 통해 이루어진다. 

[composition](http:// "컴퓨터이론에서 object composition 은 객체나 데이터타입을 더 복잡한 하나로 조합하는 방식을 말한다. 조합(Compositions)은 데이터구조와 다음의 공통적인 것들과 관련이 있습니다: union, set, sequence 그리고 다양한 graph구조. 객체지향에서 사용하는 객체들과 마찬가지로." ) 을 통해 IoC를 구현하는 의존성주입은 [strategy pattern](http:// "컴퓨터프로그래밍에서, strategy pattern 은 행위에 관한 소프트웨어설계패턴 입니다, 런타임중에 알고리즘을 선택가능한. 하나의 알고리즘만을 사용하는 것이 아닌, 여러개의 알고리즘 중에 런타임중 사용할 알고리즘을 지시받아서 사용합니다.") 과 동일할 수 있지만 strategy pattern 은 객체의 생명주기를 통한 객체간 서로 주고받을 수 있는 의존성을 목표로합니다, 의존성주입은 의존성에 대해 오직 하나의 인스턴스만 갖습니다. delegation 과 composition 을 통해서지만 여전히 polymorphism 입니다.

### Dependency injection frameworks
CDI 와 같은 Application frameworks 그리고 그것의 구현들: Weld, Spring, Guice, Play framework, Salta, Glassfish HJ2, Dagger, 그리고 Managed Extensibility Framework(MEF) 는 의존성주입은 지원하지만 필수요소는 아닙니다.

### Advantages
* 의존성주입은 클라이언트가 설정가능한 여지를 줍니다. 오직 클라이언트의 행위만 고정입니다. 클라이언트가 원하는 인터페이스를 통해 어떠한 행위도 가능합니다
* 의존성주입은 설정파일에 시스템설정을 넣어 다시 컴파일하는 일 없이 다시설정한 시스템설정이 반영되도록 할 수 있습니다. 분리된 설정은 다른 컴포넌트를 사용하는 상황에서도 쓰일 수 있습니다. 테스트도 포함해서요.
* 의존성주입은 코드에 어떤 변화도 필수는 아니기 때문에 레가시코드에도 리펙토링을 통해 적용할 수 있습니다. 클라이언트는 좀 더 독립적으로 subs 이나 mock objects 를 사용하는 분리된 곳에서 unit test 할 수 있습니다. 테스트 용이함은 의존성주입을 사용할 때 느끼는 장점 중 하나입니다.
* 의존성주입은 클라이언트가 사용하는 것에 대한 구체적인 지식이 없어도 됩니다. 클라이언트를 설계의 변경이나 결점에 대한 직접적인 영향으로 부터 분리합니다. 이것은 재사용성, 테스트용이성 그리고 유지관리측면에 도움이 됩니다.
* 어플리케이션 객체들에 있는 boilerplate code 가 줄어듭니다, 의존성을 설정하거나 모든작업을 초기화하는 것은 provider component 에서 처리하기 때문입니다.
* 의존성주입은 동시적인 또는 독립적인 개발 다 가능합니다. 두 개발자는 독립적으로 서로의 클래스들을 개발할 수 있습니다, 오직 서로 통신할 인터페이스만 알면 됩니다. Plugins 는 때로는 서드파티기업에서 개발되고 심지어 누가 플러그인을 사용하는 제품을 만들었는지도 얘기해주지 않습니다.
* 의존성주입은 클래스와 의존성들 사이의 coupling 을 감소시킵니다.

### Disadvantages

* 의존성주입은 클라이언트가 객체생성시 설정에 대한 세부사항을 넣어야 합니다. 기본값 사용이 가능할 때에는 번거로울 수 있습니다.
* 의존성주입은 코드를 추적(읽기)하기가 어렵습니다, 왜냐하면 생성자와 기능이 떨어져있기 때문입니다. 개발자는 시스템이 어떻게 작동하는지에 대해 추가적인 파일을 살펴봐야 합니다. 
* 의존성주입 프레임워크들은 동적 프로그래밍으로 구현됩니다. 이것은 IDE 의 자동화, 예를들면, "참조 찾기", "호출 계층구조 보이기" 그리고 안전한 리펙토링 같은 사용을 방해할 수 있습니다.
* 의존성주입은 보통 더많은 선행개발노력이 필요합니다. 개발자는 어떤 것을 구현을 필요로 할 때 반드시 먼저 의존하는것이 주입이 되었는지 확인해야하기 때문입니다.
* 의존성주입은 클래스로부터 복잡한 코드를 밖으로 옮깁니다, 의도치않거나 쉽게 관리하기 어려운 클래스들 사이 로요.
* 의존성주입은 의존성주입프레임워크에 대해 의존적이 될 수도 있습니다.

## Structure
### UML class and sequence diagram
![](https://github.com/khjoon0204/outerpark/blob/master/W3sDesign_Dependency_Injection_Design_Pattern_UML.jpg?raw=true)
의존성주입 설계패턴 샘플 UML 클래스와 시퀀스 다이어그램

위의 UML class diagram 에서, Client 클래스는 ServiceA 와 ServiceB 객체들을 필요로한다, ServiceA1, ServiceB1 클래스가 아니라, Injector 클래스는 객체들을 생성하고 Client에 주입한다. Client 를 객체생성으로 부터 분리한다.
UML sequence diagram 은 실시한 상호작용들을 보여준다: Injector 객체는 ServiceA1 과 ServiceB1 객체들을 생성하고, 그 후에 Client 객체를 생성한다, 그리고 ServiceA1, ServiceB1 객체들을 주입한다.

## Examples
### Without dependency injection
다음의 Java 예는, 클라이언트 클래스가 constructor 에 의해 초기화된 member variable 을 포함합니다. 클라이언트는 어떤 서비스를 사용하고 생성을 할지 제어합니다, 클라이언트는 서비스예시에서 하드코딩된 의존성을 가지고 있다고 말할 수 있습니다.
~~~
// 의존성주입 없는 예시
public class Client {
    // 클라이언트가 사용할 서비스에 대한 내부참조
    private ExampleService service;

    // 생성자
    Client() {
        // 의존성주입을 사용하는 대신 생성자에서 구현
        service = new ExampleService();
    }

    // 서비스를 사용하는 클라이언트안에 메소드
    public String greet() {
        return "Hello " + service.getName();
    }
}
~~~
의존성주입은 멤버변수를 초기화하는 대안적 기술이다, 위에서 처럼 명백하게 서비스를 생성하는 것이 아닌. 우리는 이 예시를 다양한 기술을 이용하면서 아래에 설명할 것이다.

### Types of dependency injection
클라이언트 객체가 외부모듈에 대한 참조를 할 수 있는 방법은 적어도 세가지가 있다.
constructor injection
    클라이언트 생성자 클래스를 통해 의존성을 제공받는 방법
setter injection
    injector 가 의존성을 주입하는데에 사용하는 setter method 를 만드는 방법
interface injection
    인터페이스는 의존성을 어떤 클라이언트에게든 주입할 주입메소드를 제공합니다. 클라이언트들은 의존성에 접근하는 setter method 를 드러내는 인터페이스를 구현해야합니다.
Other types
DI 프레임워크는 위에 제시된 것들 외에 다른 주입 타입을 가질 수 있습니다.
프레임웍스를 테스트할 때에는 다른 타입을 사용하기도 합니다. 현대의 테스트가능한 프레임웍스들은 클라이언트가 의존주입을 꼭 하지 않아도 됩니다, 그래서 레가시 코드도 테스트가능하게끔 만듭니다, 특히 자바언어에서는 리플렉션을 이용하여 테스트할 때나 할당으로 주입을 허용할 때 private 속성을 public 하게 만들 수 있습니다.
역전주입에서는 의존성에 대한 완전한 삭제를 제공하지않습니다, 대신에 단순히 다른 의존의 형태로 교체합니다. 경험상, 만약 프로그래머가 클라이언트 코드만 볼 수 있고 무슨 프레임워크가 사용되고 있는지 말할 수 있다면, 클라이언트는 프레임워크의 하드코딩된 의존성을 가집니다.

Constructor injection
이 메소드는 클라이언트가 constructor 에 파라메터를 제공합니다
~~~
// Constructor
Client(Service service) {
    // 클라이언트 안에 들어온 서비스에 대한 참조를 저장한다
    this.service = service;
}
~~~

Setter injection 
이 메소드는 클라이언트가 setter method 를 제공합니다
~~~
// Setter method
public void setService(Service service) {
    // 클라이언트 안에 들어온 서비스에 대한 참조를 저장한다
    this.service = service;
}
~~~

Interface injection 
클라이언트는 단순히 클라이언트 종속성에 대한 setter메소드와의 인터페이스를 공개합니다. 의존성 주입이 있을 때 injector 가 클라이언트와 대화하는 방식입니다
~~~
// Service setter interface.
public interface ServiceSetter {
    public void setService(Service service);
}

// Client class
public class Client implements ServiceSetter {
    // 클라이언트가 사용하는 서비스에 대한 내부참조
    private Service service;

    // 클라이언트가 사용하기 위해 service를 set
    @Override
    public void setService(Service service) {
        this.service = service;
    }
}
~~~

Constructor injection comparison
모든 종속성을 처음에 생성하는것을 선호합니다, 클라이언트객체는 언제나 유효한 상태임을 확신할 수 있기 때문입니다, 어떤 의존성참조는 null 을 가지고 있는것과는 달리. 그러나 이 방법대로면, 나중에 의존성이 바뀌는 것에 대해 대처하지 못합니다. 때문에 클라이언트를 바꿀 수 없게, 그리고 thread safe 하게 만들어야 합니다.
~~~
// Constructor
Client(Service service, Service otherService) {
    if (service == null) {
        throw new InvalidParameterException("service must not be null");
    }
    if (otherService == null) {
        throw new InvalidParameterException("otherService must not be null");
    }

    // 클라이언트 안에 서비스참조들을 저장한다
    this.service = service;
    this.otherService = otherService;
}
~~~

Setter injection comparison
클라이언트는 각각의 종속성에 대한 setter메소드를 제공해야만 합니다. 이것은 언제든 종속성참조들의 상태값을 바꿀 수 있는 자유를 줍니다. 그러나 만약 주입된 의존성이 하나 이상이면 클라이언트는 모든 종속성이 사용하기 전에 주입이 됐는지 확신하기 어렵습니다.
~~~
// 클라이언트가 사용할 service 를 set
public void setService(Service service) {
    if (service == null) {
        throw new InvalidParameterException("service must not be null");
    }
    this.service = service;
}

// 클라이언트가 사용할 다른 서비스를 set
public void setOtherService(Service otherService) {
    if (otherService == null) {
        throw new InvalidParameterException("otherService must not be null");
    }
    this.otherService = otherService;
}
~~~

이 주입들은 어디에도 의존없이 일어나기 때문에 주입이 끝났음을 클라이언트에게 알릴 방법이 없습니다. 종속성에 대한 setter 호출이 실패할 때 종속성은 그냥 null 로 남아있을 수 있습니다. 클라이언트는 종속성을 사용할 때 주입이 끝난건지 확인해야 합니다. 
~~~
// Set the service to be used by this client
public void setService(Service service) {
    this.service = service;
}

// Set the other service to be used by this client
public void setOtherService(Service otherService) {
    this.otherService = otherService;
}

// Check the service references of this client
private void validateState() {
    if (service == null) {
        throw new IllegalStateException("service must not be null");
    }
    if (otherService == null) {
        throw new IllegalStateException("otherService must not be null");
    }
}

// Method that uses the service references
public void doSomething() {
    validateState();
    service.doYourThing();
    otherService.doYourThing();
}
~~~

Interface injection comparison

인터페이스주입의 장점은 종속성은 무시할 수 있지만 여전히 새 클라이언트에 대한 참조는 가지고 있어, 그것을 이용해 자기-참조로 클라이언트에게 보냅니다. 종속성은 injector가 됩니다. 주입 메소드(단지 setter method 일 수도 있다)는 인터페이스를 이용하는것이 키포인트입니다.
클라이언트와 클라이언트의 종속성을 소개하기 위해 조립자가 여전히 필요합니다. 조립자는 클라이언트에 대한 참조를 가질 것이고, 종속성을 set 하기위해 setter인터페이스로 변환할 것입니다. 그리고 종속객체에 setter인터페이스를 넘기고 돌아서 다시 자기-참조로 클라이언트에게 넘깁니다. 
인터페이스 주입이 값을 갖기 위해서는 종속성은 자기에게 참조를 넘기는 추가작업이 있어야 합니다. 이것은 다른 의존성을 해결하기 위해 factory 나 부가적인 조립자처럼 보일 수 있습니다, 몇몇 세부구현사항들을 메인조립자로부터 추상화하면서.
~~~
// Service setter interface.
public interface ServiceSetter {
    public void setService(Service service);
}

// Client class
public class Client implements ServiceSetter {
    // Internal reference to the service used by this client.
    private Service service;

    // Set the service that this client is to use.
    @Override
    public void setService(Service service) {
        this.service = service;
    }
}

// Injector class
public class ServiceInjector {
	Set<ServiceSetter> clients;
	public void inject(ServiceSetter client) {
		clients.add(client);
		client.setService(new ServiceFoo());
	}
	public void switchToBar() {
		for (Client client : clients) {
			client.setService(new ServiceBar());
		}
	}
}

// Service classes
public class ServiceFoo implements Service {}
public class ServiceBar implements Service {}

~~~

Assembling examples
수동으로 메인에서 의존성을 조립하는 것도 의존주입의 한가지 방식입니다.
~~~
public class Injector {
    public static void main(String[] args) {
        // Build the dependencies first
        Service service = new ExampleService();

        // Inject the service, constructor style
        Client client = new Client(service);

        // Use the objects
        System.out.println(client.greet());
    }	
}
~~~
위의 예제는 객체를 수동으로 생성하고, 바로 작동을 시작합니다. 알아야할 점은 이 injector 는 순수하지않습니다. 이 injector 는 생성한 객체를 사용하고있습니다. 























