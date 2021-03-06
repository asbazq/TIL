# 회고

이번주 과제는 jwt를 활용하여 api를 만드는 것이었다. 

첫주차에 파이썬을 대충해보았기에 어려울거라 생각하지 않았다. 

강의 영상도 길이가 상당했고 내용도 복잡했기에 강의 내용중점으로 이해할려고 많은 시간을 투자하고 정리하면서 들었다.

강의를 다 듣고 과제를 할려고 하니 첫주에 한것과 많이 상이했고 복잡했다.

남은 시간은 얼마 없었고 해당 jwt에 대한 내용도 강의에선 자세하게 다루지않아 작성이 힘들었다.

결국 마감까지 작성하지 못하고 제출하게 됐다.

남는 시간에 jwt를 찾아보고 해봐야 될 것 같다.

## ORM

- Object Relational Mapping(객체-관계-매핑)의 약자이다.

- 객체와 데이터베이스의 관계를 매핑해주는 도구이다.

- 프로그래밍 언어의 객체와 관계형 데이터베이스의 데이터를 자동으로 매핑(연결)해주는 도구이다.

- 프로그래밍 언어의 객체와 관계형 데이터베이스 사이의 중계자(통역자) 역할을 한다.

- MVC 패턴에서 모델(Model)을 기술하는 도구이다.

- 객체와 모델 사이의 관계를 기술하는 도구이다.

**사용이유**

OOP vs Relational Database
객체 지향 프로그래밍은 클래스를 이용하고 관계형 데이터베이스는 테이블을 이용하는데 객체 모델과 관계형 모델 간의 불일치가 존재한다.

ORM을 이용해서 데이터베이스 접근을 프로그래밍 언어의 관점에서 맞출 수 있다.

ORM을 이용해서 객체 간의 관계를 바탕으로 SQL을 자동으로 생성하여 불일치를 해결한다.

ORM을 이용해서 SQL 문을 직접 작성하지 않고 엔티티를 객체로 표현할 수 있다.

ORM을 이용해서 객체를 통해 간접적으로 데이터베이스를 다룬다.

이를 통해 데이터베이스 세계와 프로그래밍 언어 사이의 개념의 간극을 줄여준다.

이를 통해 느슨하게 연결된, 테스트에 용이한 애플리케이션을 만들 수 있다.

## SQL(Structured Query Language) 

데이터베이스 시스템에서 자료를 처리하는 용도로 사용되는 구조적 데이터 질의 언어.

일반적인 프로그래밍 언어(범용 언어)와 달리 대화식 언어이기 때문에, 명령문이 짧고 간결합니다. 

SQL 자체는 범용 언어에 비해 한계가 있기 때문에, 단독으로 사용하기 보단 C#, Java, Python, PHP와 같은 고수준 언어와 함께 쓰는 것이 일반적입니다.

## MVC

Model View Controller의 약자로 에플리케이션을 세가지의 역할로 구분한 개발 방법론이다. 

사용자가 Controller를 조작하면 Controller는 Model을 통해서 데이터를 가져오고 그 정보를 바탕으로 시각적인 표현을 담당하는 View를 제어해서 사용자에게 전달하게 된다. 

![그림](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/327/1262.png)

ex)

1. 사용자가 웹사이트에 접속한다. (Uses)
2. Controller는 사용자가 요청한 웹페이지를 서비스 하기 위해서 모델을 호출한다. (Manipulates)
3. 모델은 데이터베이스나 파일과 같은 데이터 소스를 제어한 후에 그 결과를 리턴한다.
4. Controller는 Model이 리턴한 결과를 View에 반영한다. (Updates)
5. 데이터가 반영된 VIew는 사용자에게 보여진다. (Sees)

**Controller**

사용자가 접근 한 URL에 따라서 사용자의 요청사항을 파악한 후에 그 요청에 맞는 데이터를 Model에 의뢰하고, 데이터를 View에 반영해서 사용자에게 알려준다. 

**Model**

일반적으로 CI의 모델은 데이터베이스 테이블에 대응된다. 이를테면 Topic이라는 테이블은 topic_model이라는 Model을 만든다. 

그런데 이 관계가 강제적이지 않기 때문에 규칙을 일관성 있게 정의하는 것이 필요하다.

**View**

View는 클라이언트 측 기술인 html/css/javascript들을 모아둔 컨테이너이다. 

출처 : https://opentutorials.org/course/697/3828
