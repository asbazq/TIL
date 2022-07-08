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
![동작2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcAkzFN%2FbtqBp4AIlD3%2FmE8PbHZQh0WtvB0wqULb3k%2Fimg.png)

    요청 -> 프론트 컨트롤러 -> 핸들러 매핑 -> 핸들러 어댑터 -> 컨트롤러 -> 로직 수행(서비스) -> 컨트롤러 -> 뷰 리졸버 -> 응답(jsp, html)
    
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
