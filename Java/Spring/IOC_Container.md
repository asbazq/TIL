# 스프링 IoC 컨테이너

DI 를 사용하기 위해서는 객체 생성이 우선 되어야 한다. 객체 생성을 하는 곳은 바로 ioc컨테이너로 스프링 프레임워크가 필요한 객체를 생성하여 관리하는 역할을 대신해 준다.
- **빈 (Bean)**: 스프링이 관리하는 객체
- **스프링 IoC 컨테이너**: **빈**을 모아둔 통

## 빈 등록 

1. @Component
    - 클래스 선언 위에 설정
    - @Component를 갖는 어노테이션으로 @Controller, @Service, @Repository 등이 있으며, @Configuration 역시 안에 @Component를 가지고 있다.
        
        ```java
        @Component
        public class ProductService { ... }
        ```
        
    
    - 스프링 서버가 뜰 때 스프링 IoC 에 '빈' 저장
        - @Component 클래스에 대해서 스프링이 해 주는 일
            
            ```java
            // 1. ProductService 객체 생성
            ProductService productService = new ProductService();
            
            // 2. 스프링 IoC 컨테이너에 빈 (productService) 저장
            // productService -> 스프링 IoC 컨테이너
            ```
            
        - 스프링 '빈' 이름: 클래스의 앞글자만 소문자로 변경
            - public class **ProductServcie** → **productServcie**
        
    - '빈' 아이콘 확인 → 스프링 IoC 에서 관리할 '빈' 클래스라는 표시
        
        ![Untitled](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fbb112785-5de6-4ff5-adcb-fabcfc7bc5fb%2FUntitled.png?table=block&id=a33e23b4-6415-47fb-a41a-893204fd6b20&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=890&userId=&cache=v2)
        
    
    - @Component 적용 조건
        - @ComponentScan 에 설정해 준 packages 위치와 하위 packages 들
            
            ```java
            @Configuration
            @ComponentScan(basePackages = "com.sparta.springcore")
            class BeanConfig { ... }
            ```
            
        - @SpringBootApplication 에 의해 default 설정이 되어 있음
            
            com.sparta.springcore/**SpringcoreApplication.java**
            
            ![Untitled](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F2309e5ce-0339-4924-9b9d-8a54ba08d8c6%2FUntitled.png?table=block&id=089f8a7d-3500-4020-a23c-44202b90159e&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=910&userId=&cache=v2)
            
            ![Untitled](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F5842f7f3-f23d-434f-940e-6ccef4ec0b12%2FUntitled.png?table=block&id=7a835ed7-8e7a-471c-8648-19ab2f15b222&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=2000&userId=&cache=v2)
     
            
2. @Bean, @Configuration


    - 직접 객체를 생성하여 빈으로 등록 요청
    - 설정 클래스는 다음과 같이 @Configuration 어노테이션을 클래스에 붙여주면 되는데, @Bean을 사용해 수동으로 빈을 등록해줄 때에는 메소드 이름으로 빈 이름이 결정된다. 

        - **[코드스니펫] BeanConfiguration**
            
            ```java
            import org.springframework.context.annotation.Bean;
            import org.springframework.context.annotation.Configuration;
            
            @Configuration
            public class BeanConfiguration {
            
                @Bean
                public ProductRepository productRepository() {
                    String dbUrl = "jdbc:h2:mem:springcoredb";
                    String dbId = "sa";
                    String dbPassword = "";
            
                    return new ProductRepository(dbUrl, dbId, dbPassword);
                }
            }
            ```
            
        
    - 스프링 서버가 뜰 때 스프링 IoC 에 '빈' 저장
        
        ```java
        // 1. @Bean 설정된 함수 호출
        ProductRepository productRepository = beanConfiguration.productRepository();
        
        // 2. 스프링 IoC 컨테이너에 빈 (productRepository) 저장
        // productRepository -> 스프링 IoC 컨테이너
        ```
        
        - 스프링 '빈' 이름: @Bean 이 설정된 함수명
            - public ProductRepository **productRepository()** {..} → **productRepository**
            - 그러므로 중복된 빈(bean) 이름이 존재하지 않도록 주의
            
    - '빈' 아이콘 확인 → 스프링 IoC 에 '빈' 에 등록될 것이라는 표시
        
        ![Untitled](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fb513f3d9-2a4f-473c-8d46-1f41080e98d7%2FUntitled.png?table=block&id=2d877c01-3bcb-4b6b-9379-4387fafd1d72&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1660&userId=&cache=v2)
        
- @Configuration 안에서 @Bean이 빈으로 등록되는 과정

    - 스프링 컨테이너는 @Configuration이 붙어있는 클래스를 자동으로 빈으로 등록해두고, 해당 클래스를 파싱해서 @Bean이 있는 메소드를 찾아서 빈을 생성해준다.
    -  @Bean을 사용하는 클래스에는 반드시 @Configuration 어노테이션을 활용하여 해당 클래스에서 Bean을 등록한다. (@Bean으로 직접 빈을 등록해주는 것도 동작은 한다.)
    -   하지만 @Configuration 안에서 @Bean을 사용해야 싱글톤을 보장받을 수 있으므로 @Bean 어노테이션은 반드시 @Configuration과 함께 사용해주어야 한다.

        
## 빈사용 방법

  1. @Autowired
      - 멤버변수 선언 위에 @Autowired → 스프링에 의해 DI (의존성 주입) 됨

          ```java
          @Component
          public class ProductService {

              **@Autowired**
              private ProductRepository productRepository;

              // ...
          }
          ```

      - '빈' 을 사용할 함수 위에 @Autowired → 스프링에 의해 DI 됨

          ```java
          @Component
          public class ProductService {

              private final ProductRepository productRepository;

              **@Autowired**
              public ProductService(ProductRepository productRepository) {
                  this.productRepository = productRepository;
              }

              // ...
          }
          ```

      - @Autowired 적용 조건
          - 스프링 IoC 컨테이너에 의해 관리되는 클래스에서만 가능

              ![Untitled](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fbb112785-5de6-4ff5-adcb-fabcfc7bc5fb%2FUntitled.png?table=block&id=f8dce8a2-41a1-4c74-b59c-8e7965a4cb89&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=890&userId=&cache=v2)

      - @Autowired 생략 조건
          - Spring 4.3 버젼 부터 @Autowired 생략가능
          - 생성자 선언이 1개 일 때만 생략 가능
              - 파라미터가 다른 생성자들

              ```java
              public class A {
                @Autowired // 생략 불가
                public A(B b) { ... }

                @Autowired // 생략 불가
                public A(B b, C c) { ... }
              }
              ```

          - Lombok 의 **@RequiredArgsConstructor** 를 사용하면 다음과 같이 코딩 가능

              ```java
              **@RequiredArgsConstructor** // final로 선언된 멤버 변수를 자동으로 생성합니다.
              @RestController // JSON으로 데이터를 주고받음을 선언합니다.
              public class ProductController {

                  private final ProductService productService;

                  // 생략 가능
                  // @Autowired
                  // public ProductController(ProductService productService) {
                  //     this.productService = productService;
                  // }
              }
              ```


  2. ApplicationContext
      - 스프링 IoC 컨테이너에서 빈을 수동으로 가져오는 방법

          ```java
          @Component
          public class ProductService {
              private final ProductRepository productRepository;

              @Autowired
              public ProductService(ApplicationContext context) {
                  // 1.'빈' 이름으로 가져오기
                  ProductRepository productRepository = (ProductRepository) context.getBean("productRepository");
                  // 2.'빈' 클래스 형식으로 가져오기
                  // ProductRepository productRepository = context.getBean(ProductRepository.class);
                  this.productRepository = productRepository;
              }

              // ...		
          }
          ```


참고 블로그 : https://mangkyu.tistory.com/75
