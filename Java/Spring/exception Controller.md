# @ExceptionHandler

@ExceptionHandler같은 경우는 @Controller, @RestController가 적용된 Bean내에서 발생하는 예외를 잡아서 하나의 메서드에서 처리해주는 기능을 한다.
→ @ExceptionHandler({ Exception1.class, Exception2.class}) 이런식으로 두 개 이상 등록

**주의사항/알아 둘 것**

- Controller, RestController에만 적용가능하다. (@Service같은 빈에서는 안됨.)
- 리턴 타입은 자유롭게 해도 된다. (Controller내부에 있는 메서드들은 여러 타입의 response를 할 것이다. 해당 타입과 전혀다른 리턴 타입이어도 상관없다.)
- @ExceptionHandler를 등록한 Controller에만 적용된다. 다른 Controller에서 NullPointerException이 발생하더라도 예외를 처리할 수 없다.
- 메서드의 파라미터로 Exception을 받아왔는데 이것 또한 자유롭게 받아와도 된다.

<details><summary> @ExceptionHandler예시 </summary>
<p>
  
    @RestController
    public class MyRestController {
        @Autowired
        private MyService myService;
        @GetMapping("/hello")
        public String hello() {
            return "hello";//문자열 반환
        }
        @GetMapping("/myData")
        public MyData myData() {
            return new MyData("myName");//object 반환
        }
        @GetMapping("/service")
        public String serviceCall() {
            return myService.serviceMethod();//일반적인 service호출
        }
        @GetMapping("/serviceException")
        public String serviceException() {
            return myService.serviceExceptionMethod(); //service에서 예외발생
        }
        @GetMapping("/controllerException")
        public void controllerException() {
            throw new NullPointerException();//controller에서 예외발생
        }
        @GetMapping("/customException")
        public String custom() {
            throw new CustomException();//custom예외 발생
        }
        @ExceptionHandler(NullPointerException.class)
        public Object nullex(Exception e) {
            System.err.println(e.getClass());
            return "myService";
        }
    }
  
String타입과 MyData라는 나만의 객체타입을 리턴하는 메서드등의 존재하지만 ExceptionHandler하나로 다 처리할 수 있다.
myService.serviceExceptionMethod는 Service안에서 Exception이 발생하는데 이 메서드를 호출하면 서비스에서 예외가 발생했지만 결국 컨트롤러 내에서 발생한 것과 같으므로 ExceptionHandler가 예외를 잡아내어 "myService"가 리턴된다.

    public class CustomException extends RuntimeException{
      private static final long serialVersionUID = 1L;
    }

이 예외는 NullPointerException이 아니기 때문에 발생하더라도 ExceptionHandler에 의해서 처리되지 않는다

  
만약 하나로 더 많은 예외 처리를 하길 원한다면 모든 예외의 부모클래스인 Exception.class를 핸들링하게하면 된다.

  **@ExceptionHandler(Exception.class)**

</p>
</details>

# @ControllerAdvice

@ExceptionHandler가 **하나의 클래스**에 대한 것이라면, @ControllerAdvice는 **모든 @Controller** 즉, 전역에서 발생할 수 있는 예외를 잡아 처리해주는 annotation이다.

    @RestControllerAdvice
    public class MyAdvice {
        @ExceptionHandler(CustomException.class)
        public String custom() {
            return "hello custom";
        }
    }

## @RestControllerAdvice와 @ControllerAdvice

@RestControllerAdvice 어노테이션은 @ControllerAdvice와 동일한 역할 즉, 예외를 잡아 핸들링 할 수 있도록 하는 기능을 수행하면서 @ResponseBody를 통해 객체를 리턴 가능

ViewResolver를 통해서 예외 처리 페이지로 리다이렉트 시키려면 @ControllerAdvice만 써도 되고, API서버여서 에러 응답으로 객체를 리턴해야한다면 @ResponseBody 어노테이션이 추가된 @RestControllerAdvice를 적용하면 되는 것이다.

@RestController에서 예외가 발생하든 @Controller에서 예외가 발생하든 @ControllerAdvice + @ExceptionHandler 조합으로 다 캐치할 수 있고 @ResponseBody의 필요 여부에 따라 적용하면 된다는 것이다. 

또한, 만약에 전역의 예외를 잡긴하되 패키지 단위로 제한할 수도있다.

@RestControllerAdvice("com.example.demo.login.controller")

login모듈에 있는 RestController에서 발생하는 예외를 잡으려면 위와 같이 하면 된다

출처: https://jeong-pro.tistory.com/195 [기본기를 쌓는 정아마추어 코딩블로그:티스토리]

# ResponseEntity

Spring Framework에서 제공하는 클래스 중 HttpEntity라는 클래스가 존재한다. 이것은 HTTP 요청(Request) 또는 응답(Response)에 해당하는 HttpHeader와 HttpBody를 포함하는 클래스이다. 

HttpEntity 클래스를 상속받아 구현한 클래스가 RequestEntity, ResponseEntity 클래스이다. 

ResponseEntity는 사용자의 HttpRequest에 대한 응답 데이터를 포함하는 클래스이다. 따라서 **HttpStatus, HttpHeaders, HttpBody**를 포함한다. 

참고

- http header에는 (요청/응답)에 대한 요구사항 
- http body에는 그 내용 
- Response header 에는 웹서버가 웹브라우저에 응답하는 메시지
- Reponse body에는 데이터 값

ResponseEntity의 생성자를 보면 this( )를 통해서 매개변수가 3개인 생성자를 호출해 결국엔 아래 보이는 매개변수가 3개인 생성자로 가게된다. 

    public ResponseEntity(HttpStatus status) {
      this(null, null, status);
    }

    public ResponseEntity(body, Headers, HttpStatus status) {
      this(body, Headers, status);
    }
    
결론은 ResponseEntity 클래스를 사용하면, [결과값 상태코드 헤더값]을 모두 프론트에 넘겨줄 수 있고, 에러코드 또한 설정해서 보내줄 수 있다

