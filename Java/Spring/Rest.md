# REST (Representational State Transfer)

- URI + GET/POST/PUT/DELETE
- 웹의 장점을 최대한 활용할 수 있는 아키텍쳐로써 REST를 발표
- HTTP URI를 통해 제어할 자원을 명시하고, HTTP Method를 통해 해당 자원을 제어하는 명령을 내리는 방식의 아키텍쳐.


## REST의 구성

- 자원(Resource) : URL
- 행위(Verb) : HTTP Method
- 표현(Representations) : **JSON**, XML 등으로 표현 가능
> HTML, CSS 등을 주고받을 때는 Rest 를 붙이지 않음.


## 기존 Service vs REST Service

- 기존 Service : 요청에 대한 처리를 한 후 가공된 data를 이용하여 특정 플랫폼에 적합한 형태의 View로 만들어서 반환
- REST Service : data 처리만 한다거나, 처리 후 반환될 data가 있다면 JSON이나 XML 형식으로 전달. View에 대해서는 신경쓸 필요가 없다. >> 이러한 이유로 Open API에서 많이 사용

## Rest 특징

- 기존의 전송방식과는 달리 서버는 요청으로 받은 리소스에 대해 순수한 데이터를 전송한다.
- 기존의 GET/POST 외에 PUT, DELETE 방식을 사용하여 리소스에 대한 CRUD 처리를 할 수 있다.
- HTTP URI을 통해 제어할 자원을 명시하고, HTTP METHOD(GET/POST/PUT/DELETE)를 통해 해당 자원을 제어한느 명령을 내리는 방식의 Architecture이다.
- 가장 큰 단점은 딱 정해진 표준이 없어 암묵적인 표준만 정해져 있다.
  1) 하이픈(-)은 사용 가능하지만 언더바(_)는 사용하지 않는다.
  2) 특별한 경우를 제외하고 대문자 사용은 하지 않는다. (대소문자 구분함)
  3) URI 마지막에 슬래시를 사용하지 않는다.
  4) 슬래시로 계층 관계를 나타낸다.
  5) 확장자가 포함된 파일 이름을 직접 포함시키지 않는다.
  6) URI는 명사를 사용한다.
  
출처: https://jainn.tistory.com/310 [Dogfootruler Kim:티스토리]

# RESTful API

RESTful API는 두 컴퓨터 시스템이 인터넷을 통해 정보를 안전하게 교환하기 위해 사용하는 인터페이스입니다. 대부분의 비즈니스 애플리케이션은 다양한 태스크를 수행하기 위해 다른 내부 애플리케이션 및 서드 파티 애플리케이션과 통신해야 합니다. 예를 들어 월간 급여 명세서를 생성하려면 인보이스 발행을 자동화하고 내부의 근무 시간 기록 애플리케이션과 통신하기 위해 내부 계정 시스템이 데이터를 고객의 뱅킹 시스템과 공유해야 합니다. RESTful API는 안전하고 신뢰할 수 있으며 효율적인 소프트웨어 통신 표준을 따르므로 이러한 정보 교환을 지원합니다.

**RESTful이란**

RESTful은 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어이다.
‘REST API’를 제공하는 웹 서비스를 ‘RESTful’하다고 할 수 있다.
RESTful은 REST를 REST답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것이 아니다.
즉, REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭된다.

**RESTful의 목적**

이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
RESTful한 API를 구현하는 근본적인 목적이 성능 향상에 있는 것이 아니라 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것이 주 동기이니, 성능이 중요한 상황에서는 굳이 RESTful한 API를 구현할 필요는 없다.

**RESTful 하지 못한 경우**

Ex1) CRUD 기능을 모두 POST로만 처리하는 API
Ex2) route에 resource, id 외의 정보가 들어가는 경우(/students/updateName)

**REST API 설계 기본 규칙**

1. URI는 정보의 자원을 표현해야 한다.
- resource는 동사보다는 명사를, 대문자보다는 소문자를 사용한다.
- resource의 도큐먼트 이름으로는 단수 명사를 사용해야 한다.
- resource의 컬렉션 이름으로는 복수 명사를 사용해야 한다.
- resource의 스토어 이름으로는 복수 명사를 사용해야 한다.
- Ex) GET /Member/1 -> GET /members/1
2. 자원에 대한 행위는 HTTP Method(GET, PUT, POST, DELETE 등)로 표현한다.
- URI에 HTTP Method가 들어가면 안된다.
- Ex) GET /members/delete/1 -> DELETE /members/1
3. URI에 행위에 대한 동사 표현이 들어가면 안된다.(즉, CRUD 기능을 나타내는 것은 URI에 사용하지 않는다.)
- Ex) GET /members/show/1 -> GET /members/1
- Ex) GET /members/insert/2 -> POST /members/2
4. 경로 부분 중 변하는 부분은 유일한 값으로 대체한다.(즉, :id는 하나의 특정 resource를 나타내는 고유값이다.)
- Ex) student를 생성하는 route: POST /students
- Ex) id=12인 student를 삭제하는 route: DELETE /students/12


**REST API 설계 규칙**

1. 슬래시 구분자(/ )는 계층 관계를 나타내는데 사용한다.
- Ex) http://restapi.example.com/houses/apartments
2. URI 마지막 문자로 슬래시(/ )를 포함하지 않는다.
- URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI도 달라져야 한다.
- REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.
- Ex) http://restapi.example.com/houses/apartments/ (X)
3. 하이픈(- )은 URI 가독성을 높이는데 사용
- 불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높인다.
4. 밑줄(_ )은 URI에 사용하지 않는다.
- 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 하므로 가독성을 위해 밑줄은 사용하지 않는다.
5. URI 경로에는 소문자가 적합하다.
- URI 경로에 대문자 사용은 피하도록 한다.
- RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문
6. 파일확장자는 URI에 포함하지 않는다.
- REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않는다.
Accept header를 사용한다.
- Ex) http://restapi.example.com/members/soccer/345/photo.jpg (X)
- Ex) GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg (O)
7. 리소스 간에는 연관 관계가 있는 경우
- /리소스명/리소스 ID/관계가 있는 다른 리소스명
- Ex) GET : /users/{use


# REST 란 ?
REST(Representational State Transfer, 자원의 상태 전달)
네트워크 아키텍쳐 원리

# RESTful 이란 ?
아래의 몇가지 조건이 잘 지켜진 api가 있을때 RESTful 한 api 라고 할 수 있다.

1. Client, Server : 클라이언트와 서버가 서로 독립적, 분리
2. Stateless : 요청에 대해서 클라이언트의 상태가 서버에 저장되지 않는다.
 - 요청하는 값을 즉각 요청
 - ex) 햄버거 가게에서 주문할때, 치즈버거 주문 , 치즈버거 + 콜라 각각 주문, 전에 주문한걸 기억하지 않는다.
3. 캐시 : 클라이언트는 서버의 응답을 캐시 할 수 있다.
 - 클라이언트가 캐시를 통해서 응답을 재사용 할 수 있어야 하며, 이를 통해 서버의 부하를 낮출 수 있다.
4. 계층화(Layered System) : 서버와 클라이언트 사이에, 방화벽, 게이트웨이, Proxy등 다계층 형태를 구성할 수 있어야 하며, 확장 할 수 있어야함
5. 인터페이스 일관성 : 아키텍쳐를 단순화 시키고 작은 단위로 분리해서, 클라이언트, 서버가 독립적으로 개선될 수 있어야 한다.
6. Code On Demand (Optional) : 자바 애플릿, 자바스크립트 플래시 등 특정 기능을 서버가 클라이언트에 코드를 전달하여 실행 할 수 있어야 한다.
 - ex) JavaScript


## 인터페이스 일관성
1.자원 식별
 - 리소스 접근 -> URI 사용
 - http://sample.co.kr/user/100
 - Resource : user
 - 식별자 : 100
2. 메시지를 통한 리소스 조작
 - 웹에서는 다양한 방법으로 데이터 전송 가능
 - HTML, XML, JSON, TEXT ..
 - 리소스 타입 알려주기 위해 header 부분에 content-type을 통해 알려줌
3. 자기 서술적 메시지
 - 요청하는 데이터가 어떻게 처리되어져야 하는지 충분한 데이터 포함
 - HTTP 기반의 REST에서는 HTTP Method와 Header의 정보로 이를 표현
4. 애플리케이션 상태에 대한 엔진으로서 하이퍼 미디어
 - REST API의 개발에는 단순히 Client 요청에 대한 데이터만 내리는게 아닌 관련된 리소스에 대한 Link 정보까지 같이 포함


## URI 설계(REST API 설계)
1. URI(Uniform Resource Identifier)
인터넷에서 특정 자원을 나타내는 주소값, 해당 값은 유일
ex) http://naver.com/resource/sample/1
response : sample1.pdf

2. URL(Uniform Resource Locator) -> URI의 하위 개념
인터넷상에서의 자원, 특정 파일이 어디에 위치 하는지 식별 하는 주소
ex) http://www.naver.com/sample1.pdf

## URI 설계(설계 원칙 RFC-3986)
1. / 는 계층관계 나타내는데 사용
2. URI 마지막 으로 / 포함하지 않는다
3. 은 가독성 높이는데 사용
4. 밑줄(_) 사용하지 않음
5. URI 경로는 소문자
6. 파일 확장자는 URI에 포함하지 않는다
7. 프로그래밍언어에 의존적인 확장자를 사용하지 않는다
8. 구현에 의존적인 경로 사용하지 않는다(servelet..)
9. 세션 ID를 포함하지 않는다
10. 프로그래밍 언어의 Method명을 이용하지 않는다
11. 명사에 단수형보다는 복수형을 사용 -> 컬렉션에 대한 표현
12. 컨트롤러 이름은 동사나 동사구 사용
13. 경로 부분중 변하는 부분은 유일한 값으로 대체
14. CRUD 기능을 나타내는 것은 URI 에 사용하지 않는다
15. URI Query Parameter 디자인 -> 컬렉션 결과 필터링 가능(page,sort..)
16. API에 있어서 서브 도메인은 일관성있게 사용해야함
17. 클라이언트 개발자 포탈 서브 도메인 일관성있게 만든다


참고 : https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html

[참고 유튜브](https://www.youtube.com/watch?v=iOueE9AXDQQ&ab_channel=%EC%96%84%ED%8C%8D%ED%95%9C%EC%BD%94%EB%94%A9%EC%82%AC%EC%A0%84)

[aws제공 rest](서버가 하는 연결관리를 클라이언트에게 맞기고 서버는 작업 처리만 => 자원을 아낌, 많은 서비스 제공)

[자세한 사항](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)
