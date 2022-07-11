# Week3

이번주차는 숙련주차로 본격적으로 spring에대해 알아보고 공부하는 주였다. 

개인과제는 "회원가입, 로그인, 댓글 작성/수정/삭제 기능이 추가된 나만의 항해 블로그 백엔드 서버 만들기"였는데 아직 시작조차하지 못 했다.

하나를 하려고 하면 관련된 개념을 모르기 때문에 공부를 해가면서 해야했고, 공부하는 도중에도 MVC가 많이 헷갈려서 찾아보고 공부하는데 오랜시간을 잡아먹었다. 

그럼에도 아직 MVC의 대해 잘 모르는 것 같다. 기본적인 MVC에 대해 공부하는데도 이렇게 오래 걸리는데 차후 공부하게 될 개념이나, 프로그래밍을 내가 할 수 있을지 걱정된다.

또한 알고리즘도 같이 병행하고 있는데, 사용공식들을 알아가며 좀 쉬워졌다고 생각했는데 점차 복잡해지며 다시 어려워졌다. 풀어본 문제를 다시 풀어봐야 될 것같다.



# IoC(Inveersion Of Control)

IoC란 Inversion of Control의 줄임말이며, 제어의 역전이라고 한다.

스프링 애플리케이션에서는 오브젝트(빈)의 생성과 의존 관계 설정, 사용, 제거 등의 작업을 애플리케이션 코드 대신 스프링 컨테이너가 담당한다.

이를 스프링 컨테이너가 코드 대신 오브젝트에 대한 제어권을 갖고 있다고 해서 IoC라고 부른다.

따라서, 스프링 컨테이너를 IoC 컨테이너라고도 부른다.

##  IoC 컨테이너

스프링에서는 IoC를 담당하는 컨테이너를 빈 팩토리, DI 컨테이너, 애플리케이션 컨텍스트라고 부른다.

오브젝트의 생성과 오브젝트 사이의 런타임 관계를 설정하는 DI 관점으로 보면, 컨테이너를 빈 팩토리 또는 DI 컨테이너라고 부른다.

그러나 스프링 컨테이너는 단순한 DI 작업보다 더 많은 일을 하는데, DI를 위한 빈 팩토리에 여러 가지 기능을 추가한 것을 애플리케이션 컨텍스트라고 한다.

정리하자면, 애플리케이션 컨텍스트는 그 자체로 IoC와 DI 그 이상의 기능을 가졌다고 보면 된다.

<details><summary>빈 팩토리와 애플리케이션 컨텍스트</summary>
<p>
  
  ![ Spring IoC와 DI란? - 빈 팩토리와 애플리케이션 컨텍스트](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbp8WIS%2FbtrtqNSKTn8%2FEPbc1AsfoDFUNPFgrV5AS1%2Fimg.png)
 

**빈 팩토리(Bean Factory)**

- 스프링 컨테이너의 최상위 인터페이스이다.
- 스프링 빈을 관리하고 조회하는 역할을 담당한다.
- 대표적으로 getBean() 메소드를 제공한다.

**애플리케이션 컨텍스트**

- 애플리케이션 컨텍스트는 빈 팩토리 기능을 모두 상속 받아서 제공한다.
-  팩토리를 상속받아 확장하여 추가 기능을 가지고 있다
</p>
</details>  




# 의존성주입(DI)

Spring프레임워크의 3가지 핵심 프로그래밍 모델중 하나로, 

외부에서 두 객체간의 관계를 결정해주는 디자인패턴으로 

인터페이스를 사이에 두고 클래스 레벨에서는 의존관계가 고정되지 않도록 하고 런타임시에 관계를 동적으로 주입하여 결합도를 낮출수 있게 하는 기법이다.
 
## DI (Dependency Injection)

의존성 주입은 **IoC(Invesoin of Control, 의존성 역전)** 원칙하에 객체간의 결합을 약하게해주고 유지보수가좋은 코드를 만들어준다.

즉, 외부에서 생성된 객체를 이용하는 것이다.

> 스프링에서는 외부의 대상이 IoC 컨테이너가 되어, 빈을 알아서 주입해 준다.

한 객체가 어떤 객체에 의존할것인지는 별도의 관심사이다. DI컨테이너를 통해 서로 강하게 결합되어있는 두 클래스를 분리하고, 

두 객체간 관계를 결정해줌으로서 결합도를 낮추고 유연성을 확보하고자 한다.

(이때 다른 빈을 주입받으려면 자기자신도 반드시 컨테이너의 빈이여야 한다.) 

**스프링의 의존성 주입**

만약 위 코드에서 PostsService와 PostRepository가 둘다 Bean(*스프링 컨테이너 상에서 생성된 객체)으로 등록되어 있다면, 

PostsService의 생성자만 만들어주면 스프링 IoC컨테이너가 PostsRepository에 의존성을 알아서 해준다. 

(*컨테이너 : 쉽게말해 bean객체들이 들어있는 통)

<details><summary>의존성 주입방법</summary>
<p>
  
  **의존성 주입방법**

@Autowired 애노테이션을 이용하면  Spring에게 의존성을 주입하라 라고 명령하는것과 같은데 생성자, 필드, 세터에 붙일수 있다.

**1.  생성자 주입**

생성자에 @Autowired를 붙여 의존성을 주입받을 수 있으며, 가장 권장되는 주입 방식이다.

(Spring 4.3부터는 클래스의 생성자가 하나이고 그 생성자로 주입받을 객체가 빈으로 등록되어있따면 @Autowired를 생략할 수 있다.)

<details><summary>권장되는 이유</summary>
<p>
  
**생성자를 통한 주입을 사용해야 하는 이유**

Spring에서 가장 권장하는 방법은 생성자를 통한 주입이다.

**1. 생성자를 사용하면 필수적으로 사용해야 하는 의존성 없이는 인스턴스를 만들지 못하도록 강제할 수 있기 때문이다.**

만약 SampleController가 SampleRepository없이는 제대로 동작할 수 없다면 SampleController에서 생성자를 통해 강제로 SampleRepository를 무조건 주입받은 후에야 인스턴스를 생성할 수 있도록 해야할것이다. 

 

**2.  생성자주입을 통해 변경의가능성을 배제하고 불변성을 보장할 수 있다.**

 

**3. final 키워드 작성 및 롬복과의 결합**

생성자주입을 사용하면 필드객체에 final키워드를 사용할 수 있다. 이는 컴파일 시점에 누락된 의존성을 확인할수 있다.

반면 생성자 주입을 제외한 다른 주입방법들은 객체생성 이후 (생성자호출이후) 에 호출되므로 final키워드를 사용할 수 없다. ( 객체생성 이후에 필드값을 변하게 하는것이니까!)

 

또한 final키워드를 붙임으로서 Lombok과 결합되어 코드를 더 간결하게 작성할 수 있다.

롬복에는 final변수를 위한 생성자를 대신해주는 @RequiredArgsConstructor가 있다.

    @Slf4j
    @RequiredArgsConstructor // Repository를 주입하기 위해 사용
    @Service
    public class PostService {

        private final PostRepository postsRepository;
        private final ContractRepository contractRepository;
        private final UserRepository userRepository;
        private final UserService userService;
    }
    
위와 같은 코드가 가능한 이유는 Spring에서 생성자가 1개인 경우 @Autowired를 생략할수 있도록 지원해주고, 해당 생성자를 Lombok(@RequiredArgsConstructor)로 구현했기 때문이다.

</p>
</details>  

 

생성자주입은 생성자 호출시점에 (해당클래스의 인스턴스생성시) 1회 호출되는것이 보장된다.

따라서 주입받은 객체가 변하지 않거나, 반드시 객체주입이 필요한 경우에 강제하기 위해 사용된다.

    @Component
    public class SampleController {
        private SampleRepository sampleRepository;

        @Autowired // 생성자가 한개만 있을시에 생략가능 
        public SampleController(SampleRepository sampleRepository) {
            this.sampleRepository = sampleRepository;
        }
    }
    
**2. 필드 주입**

멤버변수 선언부에 @Autowired애노테이션을 붙인다.

필드주입을 이용하면 코드가 간결해져서 과거에 많이 사용했던 방법이다.

하지만 필드 주입은 외부에서 변경이 불가능하다는 단점이 존재한다. 테스트코드의 중요성이 부각됨에 따라 필드의 필드객체를 수정할 수 없는 필드주입은 거의 사용하지 않게되었다.

또한 필드주입은 반드시 DI프레임워크가 존재해야 하므로 사용을 지양해야한다. 

    @Component
    public class SampleController {
        @Autowired
        private SampleRepository sampleRepository;
    }
    
**3. Setter주입**

Setter메소드에 @Autowired애노테이션을 붙인다.

필드값을 변경하는 Setter를 통해서 의존관계를 주입하는 방법이다.

Setter주입은 생성자 주입과 달리 주입받는 객체가 변경될 가능성이 있는 경우에 사용한다. (다만 실제로 변경이 필요한 경우는 극히 드뭄)

    @Component
    public class SampleController {
        private SampleRepository sampleRepository;

        @Autowired
        public void setSampleRepository(SampleRepository sampleRepository) {
            this.sampleRepository = sampleRepository;
        }
    }
 

위 3개의 코드예시는 모두 동일하게 SampleController에 SampleRepository를 주입한다.

</p>
</details>  

[자세한 내용 참고](https://steady-coding.tistory.com/600)

# 스프링 빈(Spring Bean)

Spring IoC 컨테이너가 관리하는 자바 객체를 빈(Bean)이라고 한다. 

기존의 Java Programming 에서는 Class를 생성하고 new를 입력하여 원하는 객체를 직접 생성한 후에 사용했다.


하지만 Spring에서는 직접 new를 이용하여 생성한 객체가 아니라, Spring에 의하여 관리당하는 자바 객체를 사용한다. 

이렇게 Spring(ioc 컨테이너)에 의하여 생성되고 관리되는 자바 객체를 Bean이라고 한다. 

Spring Framework 에서는 Spring Bean 을 얻기 위하여 ApplicationContext.getBean() 와 같은 메소드를 사용하여 Spring 에서 직접 자바 객체를 얻어서 사용한다.



참고 : https://esoongan.tistory.com/90, https://steady-coding.tistory.com/600, https://velog.io/@gillog/Spring-DIDependency-Injection

