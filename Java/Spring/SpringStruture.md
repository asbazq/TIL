# Spring

기본 동작순서

![스프링구조](https://t1.daumcdn.net/cfile/tistory/996CA6455B90B6CC4E)

Request -> DispatcherServlet -> HandlerMapping -> Controller -> Service -> DAO -> DB -> DAO -> Service -> Controller -> DispatcherServlet -> ViewResolver -> View -> Response



## Entity(엔티티)

데이터베이스(Database, DB) 에 쓰일 필드와 여러 엔티티간 연관관계를 정의한다. 즉, 실제 DB Table과 연결될 클래스이다.

데이터베이스는 엑셀처럼 2차원 테이블이라고 생각하면 되는데, 이 테이블에 서비스에서 필요한 정보를 다 저장하고 활용하게 된다.

아래 그림과 같이 세로의 열 부분이 Column 이고, 가로의 행 부분이 엔티티 객체가 된다. 이 테이블 전체가 엔티티 이고, 각 1개의 행들이 엔티티 객체가 되는 것이라고 생각하면 된다.

![엔티티](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb26BcK%2Fbtq0AqdUhJD%2FM3ke7l3LtH5BFDIbAtPztk%2Fimg.png)

필드라는 것은 엔티티의 각 Column을 의미한다. "private Long bno"라고 적은 것처럼 bno라는 필드를 정의하면 하나의 Column을 정의할 수 있는 것이다.

## @ 어노테이션

- @Entity : 클래스 위에 선언하여 이 클래스가 엔티티임을 알려준다. 이렇게 되면 JPA에서 정의된 필드들을 바탕으로 데이터베이스에 테이블을 만들어준다.

- @Builder : 해당 클래스에 해당하는 엔티티 객체를 만들 때 빌더 패턴을 이용해서 만들 수 있도록 지정해주는 어노테이션이다. 이렇게 선언해놓으면 나중에 다른 곳에서 Board.builder(). {여러가지 필드의 초기값 선언 }. build() 형태로 객체를 만들 수 있다.

- @AllArgsConstructor : 선언된 모든 필드를 파라미터로 갖는 생성자를 자동으로 만들어준다.

- @NoArgsConstructor : 파라미터가 아예없는 기본생성자를 자동으로 만들어준다.

- @Getter, Setter : 각 필드값을 조회,수정할 수 있는 Getter, Setter를 자동으로 생성해준다. 

ex)

     public class ReadRequestDto {
                  private String username; 
                  private String title;
                  
                  public String getusername() {
                    return username;
                  }
                  public Stirng gettilte() {
                    return title;
                    }
                }

위와 같이 생성자를 생성해야되는데 Setter, Getter를 사용하면

          public class ReadRequestDto {
              private String username; 
              private String title;
              }

이처럼 간편한게 사용할 수 있다.

- @ToString : 해당 클래스에 선언된 필드들을 모두 출력할 수 있는 toString 메서드를 자동으로 생성할 수 있도록 해준다.

- @Id, @GeneratedValue : 해당 엔티티의 주요 키(Primary Key, PK)가 될 값을 지정해주는 것이 @Id 이다. 
 
- @GeneratedValue는 이 PK가 자동으로 1씩 증가하는 형태로 생성될지 등을 결정해주는 어노테이션이다.

- @ManyToOne : 해당 엔티티와 다른 엔티티를 관계짓고 싶을 때 쓰는 어노테이션이다. ManyToOne이라고 부르는 이유는 Writer 입장에서 Board는 여러 개가 될 수 있기 때문에 Writer : Board = 1 : N 관계가 되기 때문이다.

## Repository

Entity에 의해 생성된 DB에 접근하는 메서드(ex) findAll()) 들을 사용하기 위한 인터페이스이다.

위에서 엔티티를 선언함으로써 데이터베이스 구조를 만들었다면, 여기에 어떤 값을 넣거나, 넣어진 값을 조회하는 등의 CRUD(Create, Read, Update, Delete)를 실행하게 만드는 인터페이스.

JpaRepository를 상속받도록 함으로써 기본적인 동작이 모두 가능해지는데, JpaRepository는 어떤 엔티티를 메서드의 대상으로 할지를 다음 키워드로 지정한다. 

JpaRepository<대상으로 지정할 엔티티, 해당 엔티티의 PK의 타입>.

## Controller

사용자의 요청을 처리한 후 지정된 뷰에 모델 객체를 넘겨주는 역할을 한다. 

뷰를 연결하여 웹상에 띄우고, 뷰에서 가져오는 데이터들을 어떻게 처리하는지 사용자가 지정해놓으면 그 역할에 맞춰서 사용자의 요청을 처리하는 것이다. 

말 그대로 컨트롤러 답게 MVC 에서 웹상으로 들어오는 여러 요청들을 처리하는 역할이라고 보면된다. 

단순히 말하자면, 스프링 프레임워크(Spring Framework)의 컨트롤러(Controller)의 역할은 Model과 View를 이어주는 다리 역할이라고 보면 된다.

## Service

Service 는 Model이 데이터베이스에서 받아온 데이터를 전달받아 가공하는 역할을 한다.

## DTO

DTO(Data Transfer Object)란 계층간 데이터 교환을 위해 Data를 변형해서 사용하는 객체(Java Beans)이다.

Spring boot는 기본적으로 아래와 같은 계층 간의 데이터 교환이 이루어집니다.

![데이터 교환](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlRsK2%2FbtqJWrHlHvO%2FA1dmCicOWPlVtwPKpopQck%2Fimg.png)

|Layer|	객체|
|---|---|
|Presentation Layer	|Controller|
|Business Layer|	Service|
|Persistence Layer|	JDBC, ORM 등|
|Database|	MySQL, MariaDB 등|

**특징**

로직을 가지고 있지 않으며, 순수하게 getter/setter로만 이루어져있는 객체이다.

**사용 예시**

모든 회원 정보를 불러와야 한다고 가정하자.

User Table에는 회원의 이름, 성별, 나이, 핸드폰번호, 아이디, 비밀번호 등 많은 정보들이 존재한다.

하지만, 나는 이름, 성별, 나이만 필요하다.

User Table에 모든 데이터가 필요하지 않은 지금, Entity로 만들어 둔 class를 사용하기에는 보안상의 문제, 필요없는 값을 가지고 있다는 점에서 좋지 않다.

이런 경우, 이름, 성별, 나이만 담는 DTO를 만들어 사용하자.

## MVC

MVC 패턴(Model-View-Controller Pattern)은 애플리케이션 개발 시 그 구성요소를 Model과 View, Controller 세 가지 역할로 구분하는 디자인 패턴이다.

비즈니스 처리 로직(Model)과 UI 영역(View)의 중간에서 Controller가 연결해주는 역할을 한다.

Controller는 View로부터 들어온 사용자 요청을 해석해 Model을 업데이트하거나 Model로부터 데이터를 받아 View로 전달하는 작업 등을 수행한다.

MVC 패턴의 장점은 Model과 View를 분리함으로써 서로의 의존성을 낮추고 독립적인 개발을 가능하게 한다.

Controller는 View와 도메인 Model의 데이터를 주고 받을 때 별도의 DTO를 주로 사용한다. 

도메인 객체를 View에 직접 전달할 수 있지만, 도메인의 비즈니스 기능이 노출될 수 있으며 Model과 View 사이에 의존성이 생기기 때문이다.

## Model이란?

HashMap 형태를 갖고 있으며, key, value값을 가지고 있습니다. 

또한 addAttribute()와 같은 기능을 통해 모델에 원하는 속성과 그것에 대한 값을 주어 전달할 뷰에 데이터를 전달할 수 있습니다.

Spring에서 Controller의 메서드를 작성할 때는 특별하게 Model이라는 타입을 파라미터로 지정할 수 있습니다. 

Model 객체는 JSP에 컨트롤러에서 생성된 데이터를 담아서 전달하는 역할을 하는 존재입니다. 

이를 이용해서 JSP와 같은 뷰(View)로 전달해야 하는 데이터를 담아서 보낼 수 있습니다. 

메서드의 파라미터에 Model 타입이 지정된 경우에는 스프링은 특별하게 Model 타입의 객체를 만들어서 메서드에 주입하게 됩니다.

## DAO

Data Access Object의 약자로 풀어 해석하면 Data에 직접 Access하는 객체를 의미한다.

DAO는 데이터베이스를 조회, 조작하는 것을 전담하는 객체다. 

VO(=DTO 다만 VO는 Read-Only로 Getter 기능만 포함)를 통해 데이터베이스의 데이터와 매칭되는 객체를 생성한 후 데이터베이스의 데이터를 조회하거나 삽입, 삭제, 갱신할 수 있다.

다시 말하면, 실제 DB에 접근하여 CRUD하는 객체를 말한다.

ex) repository package에 해당한다.

JPA의 경우 JPARepository를 사용하는 경우가 DAO의 예시라고 생각하면 된다.


[스프링 구조 참조](https://coder-in-war.tistory.com/entry/Spring-12-DAO-DTO-Entity%EC%99%80-%EC%8A%A4%ED%94%84%EB%A7%81-%ED%8C%A8%ED%82%A4%EC%A7%80%EC%9D%98-%EC%A0%84%EC%B2%B4-%EA%B5%AC%EC%A1%B0)

참고 : https://gh402.tistory.com/53
