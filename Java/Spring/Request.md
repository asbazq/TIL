#  Spring에서 Client로 받은 요청을 객체로 바인딩하기 위해 사용하는 방법


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
@RequestParam은 필수 여부가 true이기 때문에 기본적으로 반드시 해당 파라미터가 전송되어야 한다. 해당 파라미터가 전송되지 않으면 400 Error를 유발하게 된다. 
그렇기 때문에 반드시 필요한 변수가 아니라면 required의 값을 false로 설정해둘 수 있으며 해당 Parameter를 사용하지 않고 요청을 보낼 경우에 default로 받을 값을 defaultValue 옵션을 통해 설정할 수도 있다.
 
## [JPA에서 Query사용](https://sundries-in-myidea.tistory.com/91)


## [ RequestBody, ModelAttribute, RequestParam 간단 정리 ]

* RequetParam

1개의 HTTP 파라미터를 얻기 위해 사용됨
필수 여부가 true이기 때문에 반드시 필요한 경우가 아니라면 required=false 설정이 필요함


* RequestBody

Json 형태로 받은 HTTP Body 데이터를 MessageConverter를 통해 변환시킴
값을 주입하지 않고 변환을 시키므로(엄밀히는 Reflection을 사용하여 할당), 변수들의 생성자나 Setter함수가 없어도 정상적으로 값이 할당됨


ModelAttribute

multipart/form-data 형태로 받은 HTTP Body 데이터와 HTTP 파라미터들을 Setter를 통해 1대1로 객체에 바인딩시킴
변환이 아닌 값을 주입시키므로, 변수들의 생성자나 Setter함수가 없으면 변수들이 저장되지 않음
출처: https://mangkyu.tistory.com/72 [MangKyu's Diary:티스토리]
