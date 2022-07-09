# Spring MVC

- Spring 프레임워크에서 제공하는 웹 모듈이다.
- MVC 는 Model-View-Controller 의 약자로, 기본 시스템 모듈을 MVC 로 나누어 구현되어있다.
  - Model 은 '데이터' 디자인을 담당한다.
    - ex. 상품 목록, 주문 내역 등
  - View 는 '실제로 렌더링되어 보이는 페이지' 를 담당한다.
    - ex. .JSP 파일들이 여기에 해당된다.
  - Controller 는 사용자의 요청을 받고, 응답을 주는 로직을 담당한다.
    - ex. GET 등의 uri 매핑이 여기에 해당된다.
- Spring MVC 모듈을 사용하여, 백엔드 프로그래밍의 기본 프레임워크를 잡는다.
  - Web 서버에 특화되어 만들어진 모듈이라, 개발자가 해야할 영역을 더 적게 만들어준다.
  - 즉 기존에 Spring 보다 더 깔끔하고 간편하게 개발 가능.

### 모델 (Model) 컴포넌트

- 데이터 저장소(ex:  데이터베이스 등)와 연동하여 사용자가 입력한 데이터나 사용자에게 출력할 데이터를 다루는 일은 함 
 
- 여러 개의 데이터 변경 작업(추가, 변경, 삭제)을 하나의 작업으로 묶는 트랜잭션을 다루는 일도 함 
 
- DAO클래스 Service 클래스에 해당

### 뷰(View) 컴포넌트
 
- 모델이 처리한 데이터나 그 작업 결과를 가지고 사용자에게 출력할 화면을 만드는 일을 함 
 
- 생성된 화면은 웹 브라우저가 출력하고, 뷰 컴포넌트는 HTML/CSS/JS를 사용하여 웹 브라우저가 출력할 UI를 만듦 
 
- HTML과 JSP를 사용하여 작성할 수 있음

### 컨트롤러(Controller)  컴포넌트

- 클라이언트의 요청을 받았을 때 그 요청에 대해 실제 업무를 수행하는 모델 컴포넌트를 호출하는 일을 함 
  
- 클라이언트가 보낸 데이터가 있다면, 모델을 호출할 때 전달하기 쉽게 데이터를 적절히 가공하는 일을 함 
  
- 모델이 업무 수행을 완료하면, 그 결과를 가지고 화면을 생성하도록 뷰에게 전달(클라이언트 요청에 대해 모델과 뷰를 결정하여 전달)
 
- Servlet 과 JSP를 사용하여 작성할 수 있음

출처: https://emongfactory.tistory.com/121 [Emong's Factory:티스토리], https://dailyheumsi.tistory.com/159

![동작](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdJDooL%2FbtqBpP4NxVG%2Fi9C3OlKdgILgixFKny52EK%2Fimg.png)
![동작2](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F2d7b8346-03a9-4fe8-b8e4-ce9ca79df02d%2FUntitled.png?table=block&id=94f0bb39-4a3c-4c11-94a6-4f2bcb2bc680&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=2000&userId=&cache=v2)

<details><summary>동작 원리</summary>
<p>

1. Client → DispatcherServlet
    1. 가장 앞 단에서 요청을 받아 FrontController 라고도 불림
2. DispatcherServlet → Controller
    - API 를 처리해 줄 Controller 를 찾아 요청을 전달
    - Handler mapping 에는 API path 와 Controller 함수가 매칭되어 있음
    
          💡 [Sample]

          GET /hello/html/dynamic → `HomeController` 의 helloHtmlFile() 함수
          GET /user/login → `UserController` 의 login() 함수
          GET /user/signup → `UserController` 의 signup() 함수
          POST /user/signup → `UserController` 의 registerUser() 함수

    
    - 함수 이름을 내 마음대로 설정 가능했던 이유!! -> Handler mapping이 Spring을 기동할 때 매칭을 한 뒤 그 다음에 동작하기 때문
    - Controller 에서 요청하는 Request 의 정보 ('Model') 전달 (DispatcherServlet -> Controller)
        
        ```java
        @Controller
        public class ItemSearchController {
        		@GetMapping("/api/search")
            @ResponseBody
            public List<ItemDto> getItems(@RequestParam String query) { // DispatcherServlet이 @RequestParam이라는 정보가 
        			// ...                                 // 클라이언트에서 왔을 때 Controller로 전달
        		}
        }
        ```
        

1. Controller → DispathcerServlet
    1. Controller 가 Client 으로 받은 API 요청을 처리
    2. 'Model' 정보와 'View' 정보를 DispatcherServlet  으로 전달(HTML을 내려주는 경우)
  > @ResponseBody를 사용할 때는 전달되지 않음
2. DispatcherServlet → Client
    1. ViewResolver 통해 View 에 Model 을 적용(View와 Model를 합침) => Template Engine(타임리프)가 실행하고 viewResolver에게 맡김
    2. View 를  Client 에게 응답으로 전달
  
    
  </p>
</details>  
    
  > Servlet (서블릿)은 자바를 사용하여 웹페이지를 동적으로 생성하는 서버측 프로그램 혹은 그 사양을 말함
    
- 컨트롤러 중에서도, 맨 앞단에서 유저의 유청을 받는 컨트롤러를 프론트 컨트롤러라고 한다.
  - DispatcherServlet 객체가 이 역할을 한다.
  - 본격적으로 로직에 들어오기 전에, 요청에 대한 선처리 작업을 수행한다.
  - ex. 지역 정보 결정, 멀티파트 파일 업로드 처리 등
- 프론트 컨트롤러는 요청을 핸들러 매핑을 통해 해당 요청을 어떤 핸들러가 처리해야하는지를 매핑한다.
  - HandlerMapping 객체가 핸들러 매핑에 대한 정보를 담고있다.
- 이렇게 매핑된 핸들러를 실제로 실행하는 역할은 핸들러 어댑터가 담당한다.
  - HandlerAdapter 객체가 이 역할을 한다.
- 컨트롤러는 해당 요청을 처리하는 로직을 담고있다.
  - 보통 요청의 종류 혹은 로직의 분류에 따라 내부적으로 Service 단위로 나누어 모듈화 한다.
  - 각 서비스에서는 DB 접근할 수 있는 Repository 객체를 이용하여 데이터에 접근할 수 있다.
- 컨트롤러는 서비스에서의 로직 처리 후, 결과를 뷰 리졸버를 거쳐 뷰 파일을 렌더링하여 내보낸다.
  - ViewResolver 객체가 이 역할을 한다.

## Server 에서 HTML 을 내려 주는 경우

- **정적 (static) 웹 페이지**

 **Controller**
 
  1. Client 의 요청을 **Model** 로 받아 처리
      1. 예) 회원가입을 위한 개인 정보들 (id, password, name)
  2. Client 에게 **View** (정적 웹 페이지, HTML) 를 내려줌

- **동적 (dynamic) 웹 페이지**

 **Controller**
 
  1. Client 의 요청을 **Model** 로 받아 처리
  2. Template engine 에게 **View**, **Model** 전달
      1. **View**: 동적 HTML 파일
      2. **Model**: View 에 적용할 정보들
  3. Template engine
      1. **View** 에 **Model** 을 적용 → 동적 웹페이지 생성
          1. 예) 로그인 성공 시, "로그인된 사용자의 id" 를 페이지에 추가
          2. Template engine 종류: 타임리프 (Thymeleaf), Groovy, FreeMarker, Jade 등 (스프링에서 JSP 이용은 추천하지 않고 있음)
  4. Client 에게 **View** (동적 웹 페이지, HTML) 를 내려줌

![HTTP](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ffa8f4918-1a70-4e2a-84e1-92f5f8ae16ce%2FUntitled.png?table=block&id=0fa44d05-5c3b-47e6-9eec-33658152dcc5&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1170&userId=&cache=v2)

- Client 와 Server 간 Request, Response 는 **HTTP 메시지 규약**을 따름


![비교](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F154b3cb0-7202-4958-9a6e-7c30f6422d67%2FUntitled.png?table=block&id=ad1a5156-70d2-458d-832c-625101ec21fa&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1650&userId=&cache=v2)

<details><summary>정적 웹페이지</summary>
<p>

1. static 폴더
    
        🌐http://localhost:8080/hello.html
    
      resources/static/hello.html
  > static 폴더 내의 hello.html을 출력
  
2. Redirect
    
    <aside>
    🌐 http://localhost:8080/hello/response/html/redirect
    
    </aside>
    
    ```java
    @Controller
    @RequestMapping("**/hello/response**")
    public class HelloResponseController {
    		@GetMapping("/html/redirect")
        public String htmlFile() {
            return "redirect:/hello.html";
        }
    }
    ```
  >   🌐 http://localhost:8080/hello.html으로 출력
  > redirect:/를 사용하면 해당 주소를 입력하면 redirect:/뒤에 오는 location을 출력
    
3. Template engine 에 View 전달
    
    <aside>
    🌐 http://localhost:8080**/hello/response/html/templates**
    
    </aside>
    
    ```java
    @GetMapping("/html/templates")
    public String htmlTemplates() {
        return "hello";
    }
    ```
  > "Hello"라는 string이 View를 전달함 즉, 템플릿 엔진에 View를 전달(Hello를 ViewName으로 전달) 
    
    타임리프 default 설정
    
    - prefix: classpath:/templates/
    - suffix: .html
  
  > 타임리프 설정 templates에서 `View`.html을 찾아라
  
  따라서 resources/templates/hello.html 출력
    
4. @ResponseBody
    
    <aside>
     🌐http://localhost:8080/hello/response/html/templates
    
    </aside>
    
    ```java
    @GetMapping("/body/html")
    @ResponseBody
    public String helloStringHTML() {
        return "<!DOCTYPE html>" +
               "<html>" +
                   "<head><title>By @ResponseBody</title></head>" +
                   "<body> Hello, 정적 웹 페이지!!</body>" +
               "</html>";
    }
    ```
    
    - @ResponseBody
        - View 를 사용하지 않고, HTTP Body 에 들어갈 String 을 직접 입력
</p>
</details>

<details><summary>동적 웹페이지</summary>
<p>

- (2) 동적 웹페이지
    
    <aside>
    🌐 http://localhost:8080**/hello/response/html/dynamic**
    
    </aside>
    
    ```java
    private static long visitCount = 0;
    
    @GetMapping("/html/dynamic")
    public String helloHtmlFile(Model model) {
        visitCount++;
        model.addAttribute("visits", visitCount);
        return "hello-visit";
    }
    ```
    
    - View,  Model 정보 → 타임리프에게 전달
    - 타임리프 처리방식
        - View 정보
            - "hello-visit" → resources**/templates/**hello-visit**.html**
            
            ```html
            <div>
              (방문자 수: <span th:text="${**visits**}"></span>)
            </div>
            ```
            
        - Model 정보
            - **visits**: 방문 횟수 (visitCount)
            - 예) 방문 횟수: **1,000,000** 번
            
            ```html
            <div>
              (방문자 수: <span>**1000000**</span>)
            </div>
            ```
            
- (3) JSON 데이터
    1. 반환값: String 
        
        <aside>
        🌐 http://localhost:8080**/hello/response/json/string**
        
        </aside>
        
        ```java
        @GetMapping("/json/string")
        @ResponseBody
        public String helloStringJson() {
            return "{\"name\":\"BTS\",\"age\":28}";
        }
        ```
        
    2. 반환값: String 외 자바 클래스
        
        <aside>
        🌐 http://localhost:8080**/hello/response/json/class**
        
        </aside>
        
        ```java
        @GetMapping("/json/class")
        @ResponseBody
        public Star helloJson() {
            return new Star("BTS", 28);
        }
        ```
        
        - "자바 객체 → JSON 으로 변환" 은 스프링이 해 줌
  
  </p>
</details>
