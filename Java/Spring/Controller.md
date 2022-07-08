# controller

1. 사용자의 요청이 진입하는 지점(entry point)이며 요청에 따라 어떤 처리를 할지 결정해준다.
2. 단, controller는 단지 결정만 해주고 실질적인 처리는 서비스(Layered Architecture)에서 담당한다.
3. 사용자에게 View(또는 서버에서 처리된 데이터를 포함하는 View)를 응답으로 보내준다.

 즉, Controller는 클라이언트의 요청을 전달받는 코드로, 역할은 요청에 따라 로직처리를 위한 분기를 담당하고 사용자에게 서버에서 처리된 데이터를 포함한 View를 리턴하는 자동 응답기
>Json만 돌려주는 것은 RestController

### controller를 왜 쓰는가?

대규모 서비스로 갈수록 처리해야할 서비스들이 많아지는데, 이를 하나의 클래스에서 몰아 처리할 게 아니라 controller라는 중간 제어자 역할을 하는 것을 만들어서 A요청에 대한 것은 A-controller가 맡아 필요한 로직처리를 위한 서비스를 호출하게 된다.
controller는 MVC 패턴에 포함되는 것인데, Model View Controller의 역할에 따라 설계하고 코딩하면 주먹구구식으로 개발할 때보다 개발비용이나 유지보수비용이 대폭 줄어든다. 역할분담이 핵심이다.

<details><summary>1. HTTP request, response 처리를 위해 매번 작성해 줘야하는 중복코드들 생략 가능</summary>
<p>
(1) Servlet Code

```java
@WebServlet(urlPatterns = "/api/search")
public class ItemSearchServlet extends HttpServlet {
	@Override
  protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
      String query = request.getParameter("query");
			
			// ...

      response.setContentType("application/json");
      response.setCharacterEncoding("UTF-8");
      PrintWriter out = response.getWriter();
      String itemDtoListJson = objectMapper.writeValueAsString(itemDtoList);
      out.print(itemDtoListJson);
      out.flush();
	}
}
```

(2) Controller Code
 
    @Controller
    public class ItemSearchController {
     @GetMapping("/api/search")
     @ResponseBody
     public List<ItemDto> getItems(@RequestParam String query) throws IOException {

       // ...

       return itemDtoList;
      }
    }
 
</p>
</details>

<details><summary>2. API 이름마다 파일을 만들 필요 없음</summary>
<p>
 
 |기능|Method|URL|반환
 |---|---|---|---|
 |로그인 페이지|	GET	|/user/login|	login 페이지|
 |로그아웃 처리|	GET	|/user/logout|	"/" 으로 redirect| 
 |회원 가입 페이지|	GET	|/user/signup|	signup 페이지|
 |회원 가입 처리|	POST	|/user/signup|	"/" 으로 redirect| 
 
 (1) Servlet Code

```java
@WebServlet(urlPatterns = "/user/login")
public class UserLoginServlet extends HttpServlet {
	@Override
  protected void doGet(HttpServletRequest request, HttpServletResponse response) {
		// ... 
	}
}
```
      @WebServlet(urlPatterns = "/user/logout")
     public class UserLogoutServlet extends HttpServlet {
      @Override
       protected void doGet(HttpServletRequest request, HttpServletResponse response) {
       // ... 
      }
     }
 
 ...API개수 만큼 생성
 
 (2) Controller Code

- API 마다 파일을 만들 필요 없음
    - 보통 하나의 Contoller 에 모든 API 를 넣지는 않음
    - 유사한 성격의 API 를 하나의 Controller 로 관리
- 함수 이름도 내 마음대로 설정 가능 (단, 클래스 내의 중복함수명 불가)
 
        @Controller
       public class UserController {
        @GetMapping("/user/login")
        public String login() {
            // ...
        }

         @GetMapping("/user/logout")
         public String logout() {
             // ...
         }

        @GetMapping("/user/signup")
        public String signup() { 
         // ... 
        }

        @PostMapping("/user/signup")
         public String registerUser(SignupRequestDto requestDto) {
         // ... 
        }
       }
</p>
</details>
