# @ManyToOne과 @OneToMany

@ManyToOne 어노테이션은 @OneToMany와 크게 다르지 않다. 
다만 @OneToMany가 1:N이라고 한다면 @ManyToOne은 N:1 관계다. 
예를 들어 은행에서 사용자는 여러 개의 계좌번호를 가지지만 계좌번호는 하나의 사용자만을 가진다.
사용자쪽에서 계좌을 바라본다면 @OneToMany, 계좌가 사용자를 바라본다면 @ManyToOne

## @ManyToOne 속성

- targetEntity
- cascade
- fetch
- optional - false로 설정했을 때 해당 객체에 null이 들어갈 수 있다. 반대로 반드시 값이 필요하다면 true(기본값은 true)
