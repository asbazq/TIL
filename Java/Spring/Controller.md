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

## AllInOneController의 문제점

Controller를 하나에 다 몰아 사용할 경우의 문제점

1. 한 개의 클래스에 너무 많은 양의 코드가 존재
    1. 코드 이해가 어려움: 처음부터 끝까지 다 읽어야 코드 내용을 이해할 수 있음
2. 현업에서는 코드 추가 혹은 변경 요청이 계속 생김
    
    [변경 요청의 예]
    
    1. 신규 상품 등록 시 Client 에게 응답 (Response) 하는 값 변경
        1. 등록된 Product 전체 정보 → 등록된 Product 의 id
    2. 최저가 (Myprice) 업데이트 조건 변경
        1. Client 가 최저가를  0원 이하로 입력 → 에러 발생
    3. DB 테이블 이름 변경
        1. Product 테이블의 **lprice** → **lowprice** 변경

따라서  Controller, Service, Repository로 역할을 분리함

1. **Controller**
    
    
    ![controller](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F9ab055dc-a05c-475b-9ca1-f7b986983024%2FUntitled.png?table=block&id=c3cb34db-cdf5-4125-b5e1-020fabe2d7ef&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=780&userId=&cache=v2)
    
    ![기능](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F900531e6-7bee-4f27-8934-7c7091245e62%2FUntitled.png?table=block&id=fe4d8667-90dd-42d8-bf79-7cc6ebd6f596&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1660&userId=&cache=v2)
    
    
    - 클라이언트의 요청을 받음
    - 요청에 대한 처리는 서비스에게 전담
    - 클라이언트에게 응답
    
2. **Service**
    
    ![Service](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F326eac47-e0a1-4871-a29b-4e7d80704a84%2FUntitled.png?table=block&id=41202e27-8919-4996-a96a-1ae8ac605f0b&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=870&userId=&cache=v2)
    
    ![기능](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F6e98050f-e496-43b0-8eba-2e458055ea44%2FUntitled.png?table=block&id=93dc5d7d-6818-4c42-85fd-d02d4c53736c&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=2000&userId=&cache=v2)
   *굳이 말하면 빨간 선 부분이지만 Repository에게 외주맡겨서 하는 느낌*
   
    - 사용자의 요구사항을 처리 ('비즈니스 로직') 하는 **실세 중에 실세!!!** 
        - 현업에서는 서비스 코드가 계속 비대해짐
    - DB 정보가 필요할 때는 Repository 에게 요청
    
3. **Repository**
    
    ![Repository](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F914029fa-aa47-4ddd-96e1-c41e9d090332%2FUntitled.png?table=block&id=b6157b34-f382-488b-bf7d-5cec6e849f1e&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=760&userId=&cache=v2)
    
    ![기능](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ffd45076b-cce4-462f-b3da-0188b10da5b2%2FUntitled.png?table=block&id=daabaa27-45e3-4531-b43a-fd27f949f9b6&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1660&userId=&cache=v2)
    
    
    
    - DB 관리 (연결, 해제, 자원 관리)
    - DB CRUD 작업 처리
    
**전체 처리과정**

![ALL](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F25b09b2a-863b-4fa5-9ac0-1eab0f31bdba%2FUntitled.png?table=block&id=25a373f0-2449-44b4-bea6-884509660860&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1770&userId=&cache=v2)
