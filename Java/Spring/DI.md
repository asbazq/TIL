## 강한 결합의 문제점

<details><summary>강한 결합 예제</summary>
<p>
  
['**강한 결합**' 이해를 위한 예제]

1. **Contoller1**  이  **Service1** 객체를 생성하여 사용
    
    ```java
    public class Controller1 {
    	private final Service1 service1;
    
    	public Controller1() {
    		this.service1 = new Service1();
    	}
    }
    ```
    
2.  **Service1**  이 **Repostiroy1** 객체를 생성하여 사용
    
    ```java
    public class Service1 {
    	private final Repository1 repository1;
    
    	public Service1() {
    		this.repository1 = new Repository1();
    	}
    }
    ```
    
3.  **Repostiroy1** 객체 선언
    
    ```java
    public class Repository1 { ... }
    ```
    
4. 만약, 다음과 같이 변경된다면..
    1.  **Repository1**  객체 생성 시 DB 접속 id, pw 를 받아서 DB 접속 시 사용
        - 생성자에 DB 접속 id, pw 를 추가
        
        ```java
        public class Repository1 {
        
        	public Repository1(String id, String pw) {
            // DB 연결
            Connection connection = DriverManager.getConnection("jdbc:h2:mem:springcoredb", id, pw);
          }
        }
        ```
  
</p>
</details>  


**강한 결합**의 문제점

- **Controller 5 개**가 각각 Service1 을 생성하여 사용 중
- **Repository1** 생성자 변경에 의해..

⇒ **모든 Contoller** 와 **모든 Service** 의 코드 변경이 필요
![강한결합](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3cdcb5ab-5b23-473b-95f0-18baaa1679d0%2FUntitled.png?table=block&id=8761f1c7-eed4-40e4-a429-c5c905425131&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1820&userId=&cache=v2)

**강한 결합 해결방법**

1. 각 객체에 대한 객체 생성은 딱 1번만 사용
2. 생성된 객체를 모든 곳에서 재사용



    1. **Repository1**  클래스 선언 및 **객체 생성** → **repository1**

        ```java
        public class Repository1 { ... }

        // 객체 생성
        **Repository1 repository1 = new Repository1();**
        ```

        ![Untitled](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F8f2872cb-625e-4164-a9d0-f51a0c6e3853%2FUntitled.png?table=block&id=0eebb41e-814d-4cef-8ba9-854e97b5e2cd&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=400&userId=&cache=v2)


    2. **Service1**  클래스 선언 및 **객체 생성 (repostiroy1 사용)** → **service1**

        ```java
        Class Service1 {
          private final Repository1 repitory1;

          // repository1 객체 사용
          public Service1(Repository1 repository1) {
            ~~this.repository1 = new Repository1();~~
            this.repository1 = repository1;
          }
        }

        // 객체 생성
        **Service1 service1 = new Service1(repository1);**
        ```

        ![Untitled](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fa1937135-6111-42f1-8699-5384d3e2a632%2FUntitled.png?table=block&id=4fd00df5-e010-4612-9961-c247bfedf9f5&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1640&userId=&cache=v2)
        
        Service1의 맴버변수repository1을 New로 생성X, New Repository1 repository1을 가져다가 사용
        
    3. **Contoller1**  선언 ( **service1** 사용)
    
    ```java
    Class Controller1 {
    	private final Service1 service1;
    
    	// service1 객체 사용
    	public Controller1(Service1 service1) {
    		~~this.service1 = new Service1();~~
    		this.service1 = service1;
    	}
    }
    ```
    
    4. 만약, 다음과 같이 변경된다면,
        1.  **Repository1**  객체 생성 시 DB 접속 id, pw 를 받아서 DB 접속 시 사용
            - 생성자에 DB 접속 id, pw 를 추가

            ```java
            public class Repository1 {

              public Repository1(**String id, String pw**) {
                // DB 연결
                Connection connection = DriverManager.getConnection("jdbc:h2:mem:springcoredb", **id, pw**);
              }
            }

            // 객체 생성
            **String id = "sa";
            String pw = "";**
            Repository1 repository1 = new Repository1(**id, pw**);
            ```

[개선 결과]

⇒ **Repository1** 생성자 변경은 이제 누구에게도 피해(?) 를 주지 않음

⇒ **Service1** 생성자가 변경되면? **모든 Contoller** → Controller 변경 필요 X

결론적으로, **강한 결합 ⇒ 느슨한 결합**

![Untitled](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F4fadca13-f416-442e-b14f-cb1b50656105%2FUntitled.png?table=block&id=d3c9f1da-0342-456f-9e59-4c89bdd965de&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1790&userId=&cache=v2)

## 제어의 역전 (IoC: Inversion of Control)
프로그램의 제어 흐름이 뒤바뀜

![ioc](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F770a5e36-424d-4481-b7bd-2068fa24e8c7%2FUntitled.png?table=block&id=4cd66e33-0fa5-4489-b1e4-68eececba845&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=2000&userId=&cache=v2)

- 일반적: 사용자가 자신이 필요한 객체를 생성해서 사용
- IoC (제어의 역전)
    - 용도에 맞게 필요한 객체를 그냥 가져다 사용
        - "**DI (Dependency Injection)**" 혹은 한국말로 "**의존성 주입**"이라고 부릅니다.
    - 사용할 객체가 어떻게 만들어졌는지는 알 필요 없음
