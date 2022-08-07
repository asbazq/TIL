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

참고 : https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html

[참고 유튜브](https://www.youtube.com/watch?v=iOueE9AXDQQ&ab_channel=%EC%96%84%ED%8C%8D%ED%95%9C%EC%BD%94%EB%94%A9%EC%82%AC%EC%A0%84)

[aws제공 rest](서버가 하는 연결관리를 클라이언트에게 맞기고 서버는 작업 처리만 => 자원을 아낌, 많은 서비스 제공)

[자세한 사항](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)
