java: class Main is public, should be declared in a file named Main.java
public class는 고유명사,

Exception in thread "main" java.lang.NullPointerException 

at aa.bb.cc.NullPointerException.main(NullPointerException.java:7) 와 같은 에러가 뜬다. 왜냐면, java.lang 패키지 안에 있는 클래스인 Integer의 참조변수인 myInteger가 null값을 가지니 intValue()를 불러오는데 에러가 생긴 거다. 혹은 변수 크기 미설정



 코드 myInteger는 null값이 아닌 다른 값을 이용하려고 하는데 null값이니 에러가 날 수 밖에 없는 것이다.

 

 위와 같이 간단한 코드는 틀린 점을 쉽게 찾을 수 있지만, 초기화가 필요한 경우나 커넥션을 이용하는 코드 같은 경우 꾀나 골탕을 먹힌다. 보통 코드를 다시 살펴보거나 차례대로 코드를 해석하면 이런 실수는 덜 할 것 같다.



~ cannot find(resolve) to ~

 코드에서 변수나 메서드를 찾을 수 없다는 에러문이다. 선언하지 않은 변수 혹은 메서드를 사용했거나, 변수나 메서드의 이름을 잘못 사용했을 때 일어나는 에러이다. 



 이클립스 같은 경우 해당 변수나 메서드에 주로 더블 클릭하거나 그 변수나 메서드에 마우스를 가져다 댔을때 하이라이트가 먹힌다. 이것을 이용해 틀리게 입력한 메서드나 변수를 쉽게 찾을 수 있다.



 또한, Ctrl + 클릭 시 해당 메서드의 내용으로 페이지가 옮겨가는데, 만약 Ctrl + 클릭이 먹지 않으면 그 메서드가 잘못 된 것을 쉽게 알 수 있다.



';' expected

 세미콜론 (';')이 필요하다는 뜻이다. 주로 타자를 잘못 치거나 가끔 문장에 세미콜론을 빠뜨렸을 때 나타나는 에러다.



Exception in thread "main" java.lang.NoSuchMethodError: main

 main 메서드를 찾지 못했을 때 일어나는 에러다. main이 존재하지 않거나 선언부(public static void main(String[] args))가 잘못 선언되면 일어나는 에러다. 

 main 메서드가 잘 선언되있는지 살펴보면 될 것이다.



Multiple markers at this line

 문장에 문법적 오류가 있을때 일어나는 에러다. 괄호, 수식, if문 for문 같은 문법적 오류와 private이나 static와 같은 키워드 차원에서도 일어난다.
 
 java: cannot find symbol
실행구문의 생성자가 pubic class의 이름과 다르다.
 
 missing return statement
 
 모든 경우에 대한 return 값을 가지도록 한다.
 
 expected "identifier"; SQL statement
 
 테이블 이름과 SQL명령어 중복
 테이블 이름을 바꾸거나 @Table(name = "")을 사용한다
 
 No property 'xxx' found for type 'xxxx' Did you mean ''xxxxx''
 해당 Colum을 찾지 못해서 발생하는 오류 Colum가 철자가 다르거나 
 
 Error creating bean with name, No property '' found for type ''!
 빈 생성 에러 type''에 property ''가 없다 따라서 type에 property생성
 
 ErrorCode : creating bean with name "XXXController"

- Controller 빈 생성 에러가 발생 했다면 servlet-context.xml 같은 servlet을 확인해서  	<context:component-scan base-package="패키지명" />에 현재 작업중인 프로젝트의 패키지명, 즉 컨트롤러가 포함된 패키지의 위치를 정확하게 기재(그냥 컨트롤러에 패키지를 그대로 복사해서 넣으시는 걸 추천) 
- @Controller 어노테이션이 없어서 일수도 있다

ErrorCode : Unsatisfied dependency expressed through field

위 에러와 동시에 일어나는 경우가 많음

위와 동일하게 @Service, @Repository가 없어서 
 
 **스프링 빈의 순환 종속성(Circular dependencies)**
 
 errorCode : Unsatisfied dependency expressed through constructor parameter
  - 클래스 A와 B의 Bean이 서로 주입되도록 구성하면 Spring IoC 컨테이너는 런타임시이 순환 참조를 감지하고 BeanCurrentlyInCreationException을 발생
  - 해결하기 위해 아래와 같이 @Lazy 어노테이션을 추가한다
    - 당장 시작은 null 로 할당됩니다. 그리고 잘 동작합니다.
    - 그러나 bComponent 는 final 이기 때문에 이후에도 어떻게 변경 할 수가 없다.
    -  그래서 Spring Framework 는 AComponent 전체를 Proxy로 만들어서 처리


           @Component
           public class AComponent {
               private final BComponent bComponent;

               public AComponent(@Lazy BComponent bComponent) {
                   log.info( "bComponent is {}", bComponent);
                   this.bComponent = bComponent;
               }
           }


**@Builder 사용시 초기화할 필드가 있다면**

errorCode : @Builder will ignore the initializing expression entirely. If you want the initializing expression to serve as default, add @Builder.Default. If it is not supposed to be settable during building, make the field final.

@Builder 는 초기화 표현을 완전히 무시한다. 초기화 하고 싶으면 @Builder.Default or final 를 

**build 시 오류**

errorCode :  Caused by: org.springframework.beans.factory.UnsatisfiedDependencyException at ConstructorResolver.java:800

maven은 기본적으로 프로필 파일을 읽어오지만, gradle에서 properties를 못읽어 오기때문에 직접 넣어줘야된다.

    sourceSets {
                main {
                    resources {
                        srcDirs("src/main/resources")
                    }
                }
            }

**passwordEncoder**

errorCode : Parameter 1 of constructor in com.example.zaritalk.service.UserService required a bean of type 'org.springframework.security.crypto.password.PasswordEncoder' that could not be found.

passwordEncoder 가 빈으로 등록되지 않아서 생기는 문제
 
WebCoSecurityConfig에 BCryptPasswordEncoder를 빈으로 등록


**CorsError**

 When allowCredentials is true, allowedOrigins cannot contain the special value "*" since that cannot be set on the "Access-Control-Allow-Origin" response header. 
 - AllowCredentials(true)일 경우, AllowedOrigin("*") 설정할 수 없다.
 - AllowedOrigin("*") -> AllowedOriginPattern("*")로 

**종송성 추가Error**

errorCode :
  removeContentEntry: removed content entry url 'file://C:/Users/User/Desktop/spring/uandmeet/build/generated/sources/annotationProcessor/java/main' still exists after removing
  
  project-dir/.idea/compiler.xml, project-dir/.idea/modules.xml 를 삭제
