#  DB 의 연관관계 이해

- DB 의 연관관계
    - JPA 가 제공하는 연관관계는 결국 DB 의 연관관계를 표현하기 위함
    - 따라서 먼저 DB 의 연관관계를 이해해야 함
    - DB 의 연관관계는 비즈니스 요구사항에 맞춰 이루어짐

# JPA 연관관계

JPA 의 경우는 Enitity 클래스의 필드 위에 연관관계 어노테이션 (@) 을 설정해 주는 것만으로 연관관계가 형성

**배달음식 서버일때**

|관계|코드선언|Entity|Example|
|---|---|---|---|
|일대다 (1:N)|	@OneToMany|	Order (1) : Food (N)|	배달 주문 1개에 음식 여러개 선택 가능|
다대일 (N:1)|	@ManyToOne|	Owner (N) : Restaurant(1)	|음식점 주인 여러명이 하나의 음식점을 소유 가능|
일대일 (1:1)	|@OneToOne|	Order (1) : Coupon (1)|	배달 주문 1개 주문 시, 쿠폰 1개만 할인 적용 가능|
다대다 (N:N)	|@ManyToMany|	User (N) : Restaurant(N)|	고객은 음식점 여러개 찜 가능, 음식점은 고객 여러명에게 찜 가능|

> @ManyToMany를 사용하기 보다는 @ManyToOne으로 나눠서 사용하기를 권장

**항상 Enitity 본인 중심으로 관계를 생각!**

- 주문 (Order) 코드
    
    ```java
    @Enitity
    public class Order {
        @OneToMany
        private List<Food> foods;
    
    		@OneToOne
    		private Coupon coupon;
    }
    ```
    
- 음식점주 (Owner)
    
    ```java
    @Entity
    public class Owner {
    	@ManyToOne
    	Restaurant restaurant;
    }
    ```
    
- 고객 (User)
    
    ```java
    @Entity
    public class User {
    	@ManyToMany
    	List<Restaurant> likeRestaurants;
    }
    ```
