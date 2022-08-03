# @Controller와 @RestController 차이

Spring에서 컨트롤러를 지정해주기 위한 어노테이션은 @Controller와 @RestController가 있습니다. 

전통적인 Spring MVC의 컨트롤러인 @Controller와 Restuful 웹서비스의 컨트롤러인 @RestController의 주요한 차이점은 HTTP Response Body가 생성되는 방식입니다. 

이번에는 2가지 어노테이션의 차이와 사용법에 대해 알아보도록 하겠습니다.
 
## @Controller

**Controller로 View 반환하기**

전통적인 Spring MVC의 컨트롤러인 @Controller는 주로 View를 반환하기 위해 사용합니다. 

아래와 같은 과정을 통해 Spring MVC Container는 Client의 요청으로부터 View를 반환합니다.

![controller](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbED6o9%2Fbtrx1wyKwpF%2FNtSlrTohpAI79l6MA95SZ1%2Fimg.png)

1. Client는 URI 형식으로 웹 서비스에 요청을 보낸다.
2. DispatcherServlet이 요청을 위임할 HandlerMapping을 찾는다.
3. HandlerMapping을 통해 요청을 Controller로 위임한다.
4. Controller는 요청을 처리한 후에 ViewName을 반환한다.
5. DispatcherServlet은 ViewResolver를 통해 ViewName에 해당하는 View를 찾아 사용자에게 반환한다.

Controller가 반환환 뷰의 이름으로부터 View를 렌더링하기 위해서는 ViewResolver가 사용되며, ViewResolver 설정에 맞게 View를 찾아 렌더링합니다.

**Controller로 Data 반환하기**

하지만 Spring MVC의 컨트롤러를 사용하면서 Data를 반환해야 하는 경우도 있습니다. 

컨트롤러에서는 데이터를 반환하기 위해 @ResponseBody 어노테이션을 활용해주어야 합니다. 

이를 통해 Controller도 Json 형태로 데이터를 반환할 수 있습니다.

![date](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb3McJC%2Fbtrx1IGcnGs%2F2iHFmw3bbqasfCJzwCKYuK%2Fimg.png)

1. Client는 URI 형식으로 웹 서비스에 요청을 보낸다.
2. DispatcherServlet이 요청을 위임할 HandlerMapping을 찾는다.
3. HandlerMapping을 통해 요청을 Controller로 위임한다.
4. Controller는 요청을 처리한 후에 객체를 반환한다.
5. 반환되는 객체는 Json으로 Serialize되어 사용자에게 반환된다.

컨트롤러를 통해 객체를 반환할 때에는 일반적으로 ResponseEntity로 감싸서 반환을 합니다. 

그리고 객체를 반환하기 위해서는 viewResolver 대신에 HttpMessageConverter가 동작합니다. 

HttpMessageConverter에는 여러 Converter가 등록되어 있고, 반환해야 하는 데이터에 따라 사용되는 Converter가 달라집니다. 

단순 문자열인 경우에는 StringHttpMessageConverter가 사용되고, 객체인 경우에는 MappingJackson2HttpMessageConverter가 사용되며, 
데이터 종류에 따라 서로 다른 MessageConverter가 작동하게 됩니다. 

Spring은 클라이언트의 HTTP Accept 헤더와 서버의 컨트롤러 반환 타입 정보 둘을 조합해 적합한 HttpMessageConverter를 선택하여 이를 처리합니다.

**@Controller 예제 코드**

    @Controller
    @RequiredArgsConstructor
    public class UserController {

        private final UserService userService;

        @GetMapping(value = "/users")
        public @ResponseBody ResponseEntity<User> findUser(@RequestParam("userName") String userName){
            return ResponseEntity.ok(userService.findUser(user));
        }

        @GetMapping(value = "/users/detailView")
        public String detailView(Model model, @RequestParam("userName") String userName){
            User user = userService.findUser(userName);
            model.addAttribute("user", user);
            return "/users/detailView";
        }
    }

 
위 예제의 findUser는 User 객체를 ResponseEntity로 감싸서 반환하고 있고, User를 json으로 반환하기 위해 @ResponseBody라는 어노테이션을 붙여주고 있습니다. 

detailView 함수에서는 View를 전달해주고 있기 때문에 String을 반환값으로 설정해주었습니다. 

(물론 이렇게 데이터를 반환하는 RestController와 View를 반환하는 Controller를 분리하여 작성하는 것이 좋습니다.)

## @RestController

@RestController는 @Controller에 @ResponseBody가 추가된 것입니다. 

당연하게도 RestController의 주용도는 Json 형태로 객체 데이터를 반환하는 것입니다. 

최근에 데이터를 응답으로 제공하는 REST API를 개발할 때 주로 사용하며 객체를 ResponseEntity로 감싸서 반환합니다. 

이러한 이유로 동작 과정 역시 @Controller에 @ReponseBody를 붙인 것과 완벽히 동일합니다.

![restC](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FH03z4%2Fbtrx1IGclWg%2FcMTcF0HrJBYiahwCPsFME0%2Fimg.png)

1. Client는 URI 형식으로 웹 서비스에 요청을 보낸다.
2. DispatcherServlet이 요청을 위임할 HandlerMapping을 찾는다.
3. HandlerMapping을 통해 요청을 Controller로 위임한다.
4. Controller는 요청을 처리한 후에 객체를 반환한다.
5. 반환되는 객체는 Json으로 Serialize되어 사용자에게 반환된다.

**@RestController 예제 코드**

    @RestController
    @RequestMapping("/user")
    @RequiredArgsConstructor
    public class UserController {

        private final UserService userService;

        @GetMapping(value = "/users")
        public User findUser(@RequestParam("userName") String userName){
            return userService.findUser(user);
        }

        @GetMapping(value = "/users")
        public ResponseEntity<User> findUserWithResponseEntity(@RequestParam("userName") String userName){
            return ResponseEntity.ok(userService.findUser(user));
        }
    }
 
 
findUser는 User 객체를 그대로 반환하고 있습니다. 이러한 경우의 문제는 클라이언트가 예상하는 HttpStatus를 설정해줄 수 없다는 것입니다. 

예를 들어 어떤 객체의 생성 요청이라면 201 CREATED를 기대할 것이지만 객체를 그대로 반환하면 HttpStatus를 설정해줄 수 없습니다. 

그래서 객체를 상황에 맞는 ResponseEntity로 감싸서 반환해주어야 합니다.

출처: https://mangkyu.tistory.com/49 [MangKyu's Diary:티스토리]

## 생성자 생성

@NoArgsConstructor : 파라미터가 없는 기본 생성자를 생성

@AllArgsConstructor : 모든 필드 값을 파라미터로 받는 생성자를 만듦

@RequiredArgsConstructor : final이나 @NonNull인 필드 값만 파라미터로 받는 생성자 만듦

        @NoArgsConstructor
        @RequiredArgsConstructor
        @AllArgsConstructor
        public class User {

          private Long id;

          @NonNull
          private String name;

          @NonNull
          private String pw;

          private int age;

        }


생성자 모습

        User user1 = new User(); // @NoArgsConstructor
        User user2 = new User("user2", "1234"); // @RequiredArgsConstructor
        User user3 = new User(1L, "user3", "1234", null); // @AllArgsConstructor
