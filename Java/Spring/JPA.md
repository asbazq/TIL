# JPA

JPA는 자바 진영에서 ORM(Object-Relational Mapping) 기술 표준으로 사용되는 인터페이스의 모음이다. 
그 말은 즉, 실제적으로 구현된것이 아니라 구현된 클래스와 매핑을 해주기 위해 사용되는 프레임워크이다.

## ORM(Object-relational mapping)

<details>
  
- Object-relational mapping (객체 관계 매핑)
  
  - 객체는 객체대로 설계하고, 관계형 데이터베이스는 관계형 데이터베이스대로 설계한다.
  
  - ORM 프레임워크가 중간에서 매핑해준다.
  
- 대중적인 언어에는 대부분 ORM 기술이 존재한다.
  
- ORM은 객체와 RDB 두 기둥 위에 있는 기술이다.
  
>  우리가 일반 적으로 알고 있는 애플리케이션 Class와 RDB(Relational DataBase)의 테이블을 매핑(연결)한다는 뜻이며, 
  기술적으로는 어플리케이션의 객체를 RDB 테이블에 자동으로 영속화 해주는 것이라고 보면된다.
  
</details>

## JPA

- Java 진영에서 ORM(Object-Relational Mapping) 기술 표준으로 사용하는 인터페이스 모음
- 자바 어플리케이션에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스
- 인터페이스 이기 때문에 Hibernate, OpenJPA 등이 JPA를 구현함
> 인터페이스이기에 실제로 동작하는 것이 아니다.

### JPA 사용 이유

1. SQL 중심적인 개발에서 객체 중심으로 개발

2. 생산성
- JPA를 사용하는 것은 마치 Java Collection에 데이터를 넣었다 빼는 것처럼 사용할 수 있게 만든 것이다.
- 간단한 CRUD
  - JPA는 매핑된 관계를 이용해서 SQL을 생성하고 실행하는데, 개발자는 어떤 SQL이 실행될지 생각만하면 되고, 예측도 쉽게 할 수 있다 
  - 특히, 수정이 굉장히 간단하다.
    - 객체를 변경하면 그냥 알아서 DB에 UPDATE Query가 나간다.
3. 유지보수
- 기존: 필드 변경 시 모든 SQL을 수정해야 한다.
- JPA: 필드만 추가하면 된다. SQL은 JPA가 처리하기 때문에 손댈 것이 없다.

<details><summary>JPA <> Spring JPA</summary>
  
  스프링에서 흔히 사용하는 것으로 알고있는 JPA는, JPA를 이용하는 spring-data-jpa 프레임워크이지 JPA는 아니다.
  
  ![jpa](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbFmukB%2Fbtq0qA03yL7%2FD2Sys7i6RaEBAd6cK0fuFk%2Fimg.png)

</details>
  
  출처 : https://gmlwjd9405.github.io/2019/08/04/what-is-jpa.html,  https://dbjh.tistory.com/77
          
