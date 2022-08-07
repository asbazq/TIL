# Request 객체는 API를 컨트롤하기 위한 메소드

- param
- query
- body


## req.param

- 주소에 포함된 변수를 담는다. 예를 들어 `https://naver.com/post/12345`라는 주소가 있다면 12345를 담는다.
- 서버에서 Path Variable 로 칭한다.

## req.query

- 주소 바깥, ? 이후의 변수를 담는다. 예를 들어`https://okky.com/post?q=Node.js`일 경우 Node.js를 담는다
- &로 연결하여 여러 개의 데이터를 넘길 수 있다. `https://naver.com/post?post_id=1235&key=value`
- 서버에서 Query parameter 로 칭한다.

## req.body

- XML, JSON, Multi Form 등의 데이터를 담는다. 당연히 주소에서 확인할 수 없다.
- 하지만 크롬 개발자 도구, Fiddler와 같은 툴로 요청 내용을 확인할 수 있다. 민감한 데이터의 경우 반드시 암호화해 전송해야 한다.
 

### param vs query
resource를 식별해야하는 상황에서는Path Variable가 더 적합하다.
정렬이나 필터링을 해야하는 상황에서는 Query Parameter가 더 적합하다.
 

### query string(query/parameter) vs body
- body을 사용할 때 
  - 인수에 플랫 키-값 구조가 없는 경우
  직렬화 된 이진 데이터와 같이 값이 사람이 읽을 수없는 경우
  매우 많은 수의 인수가있을 때(일부 웹 서버에는 URI 길이에 제한이 있다.) body에는 제한이 없음

- query string을 사용할 때
  - 인수가 디버깅하는 동안보고 싶을 때
  - 코드를 개발하는 동안 수동으로 호출 할 수 있기를 원할 때
    ex) curl
  - 여러 웹 서비스에서 인수가 공통적인 경우
  - 다음과 같은 다른 콘텐츠 유형을 이미 보내고있는 경우 application/octet-stream

혼합하여 일치시킬 수 있습니다. 공통된 항목, 디버그 가능해야하는 항목을 쿼리 문자열에 넣고 나머지는 json에 모두 넣습니다.


## @RequestBody

@RequestBody는 클라이언트가 전송하는 Json(application/json) 형태의 HTTP Body 내용을 Java Object로 변환시켜주는 역할을 한다.

그렇기 때문에 Body가 존재하지 않는 HTTP Get 메소드에 @RequestBody를 활용하려고 한다면 에러가 발생하게 된다.

@RequestBody로 받는 데이터는 Spring에서 관리하는 MessageConverter들 중 하나인 MappingJackson2HttpMessageConverte를 통해 Java 객체로 변환된다. 

Spring은 메세지를 변환되는 과정에서 객체의 기본 생성자를 통해 객체를 생성하고, 

내부적으로 Reflection을 사용해 값을 할당하므로 @RequestBody에는 값을 주입하기 위한 생성자나 Setter가 필요 없다.
 

추가적으로 조금 깊게 설명을 하면 Json 데이터를 변환하기 위해서는 Jackson 라이브러리가 사용되는데, 

Jackson 라이브러리 내부적으로는 Getter나 Setter, @JsonInclude 등을 통해 필드에 있는 변수들의 이름을 찾고, Reflection을 이용해 값을 할당한다.


## @RequestParam

@RequestParam은 1개의 HTTP 요청 파라미터를 받기 위해서 사용한다. 

@RequestParam은 필수 여부가 true이기 때문에 기본적으로 반드시 해당 파라미터가 전송되어야 한다. 

해당 파라미터가 전송되지 않으면 400 Error를 유발하게 된다. 

그렇기 때문에 반드시 필요한 변수가 아니라면 required의 값을 false로 설정해둘 수 있으며 

해당 Parameter를 사용하지 않고 요청을 보낼 경우에 default로 받을 값을 defaultValue 옵션을 통해 설정할 수도 있다.
 
**[JPA에서 Query사용](https://sundries-in-myidea.tistory.com/91)


## [ RequestBody, ModelAttribute, RequestParam 간단 정리 ]

* RequetParam

1개의 HTTP 파라미터를 얻기 위해 사용됨

필수 여부가 true이기 때문에 반드시 필요한 경우가 아니라면 required=false 설정이 필요함


* RequestBody

Json 형태로 받은 HTTP Body 데이터를 MessageConverter를 통해 변환시킴

값을 주입하지 않고 변환을 시키므로(엄밀히는 Reflection을 사용하여 할당), 변수들의 생성자나 Setter함수가 없어도 정상적으로 값이 할당됨


* ModelAttribute

multipart/form-data 형태로 받은 HTTP Body 데이터와 HTTP 파라미터들을 Setter를 통해 1대1로 객체에 바인딩시킴

변환이 아닌 값을 주입시키므로, 변수들의 생성자나 Setter함수가 없으면 변수들이 저장되지 않음


출처: https://mangkyu.tistory.com/72 [MangKyu's Diary:티스토리]
