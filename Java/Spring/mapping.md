# Mapping

객체와 테이블 매핑 : @Entity

@Table기본 키 매핑 : @Id

필드와 컬럼 매핑 : @Column

연관관계 매핑 : @ManyToOne, @JoinColumn


## @Entity
- 테이블과의 매핑
- @Entity가 붙은 클래스는 JPA가 관리하는 것으로, 엔티티라고 불림	
> 속성
  - Name : JPA에서 사용할 엔티티 이름을 지정.       
  - 보통 기본값인 클래스 이름을 사용
> 주의사항
  - 기본 생성자는 필수 (JPA가 엔티티 객체 생성 시 기본 생성자를 사용)
  - final 클래스, enum, interface, inner class 에는 사용할 수 없음
  - 저장할 필드에 final 사용 불가

## @Table
- 엔티티와 매핑할 테이블을 지정
- 생략 시 매핑한 엔티티 일므을 테이블 이름으로 사용
> 속성 
- Name : 매핑할 테이블 이름 (default. 엔티티 이름 사용)
- Catalog : catalog 기능이 있는 DB에서 catalog 를 매핑 (default. DB 명)
- Schema : schema 기능이 있는 DB에서 schema를 매핑
- uniqueConstraints : DDL 생성 시 유니크 제약조건을 만듦, 스키마 자동 생성 기능을 사용해서 DDL을 만들 때만 사용

## 기본키 매핑
- 영속성 컨텍스트는 엔티티를 식별자 값으로 구분하므로 엔티티를 영속 상태로 만들기 위해 식별자 값이 반드시 필요
@GeneratedValue
<기본 키 생성 전략>
- 직접 할당 : 기본 키를 애플리케이션에 직접 할당
 
  ㄴ em.persist()를 호출하기 전 애플리케이션에서 직접 식별자 값을 할당해야 함. 식별자 값이 없을 경우 예러 발생
- 자동 생성 : 대리 키 사용 방식
   * IDENTITY : 기본 키 생성을 데이터베이스에 위임 (= AUTO_INCREMENT)
   * SEQUENCE : 데이터베이스 시퀀스를 사용해서 기본 키를 할당,    데이터베이스 시퀀스에서 식별자 값을 획득한 후 영속성 컨텍스트에 저장   유일한 값을 순서대로 생성(오라클, PostgreSQL, DB2, H2)	
   * TABLE : 키 생성 테이블을 사용키 생성 전용 테이블 하나를 만들고 여기에 이름과 값으로 사용할 컬럼을 만들어데이터베이스 시퀀스를 흉내내는 전략. 테이블을 사용하므로 모든 데이터베이스에 적용 가능	
   * AUTO : 선택한 데이터베이스 방언에 따라 방식을 자동으로 선택(Default)  Ex) 오라클 DB 선택 시 SEQUENCE, MySQL DB 선택 시 IDENTITY 사용
출처: https://data-make.tistory.com/610 [Data Makes Our Future:티스토리]
