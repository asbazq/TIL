# Spring Security

Spring Security는 Spring 기반의 애플리케이션에서 보안(Authentication인증과 권한, Authorization 인가)을 처리해주는 Spring 하위 프레임워크라고 한다. 

![security](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FzAwPR%2Fbtq5nbiTUjR%2F5Gd1Nk5026vN2kjEK7aVS1%2Fimg.png)

1. 사용자가 form을 통해 로그인 정보가 담긴 Request를 보냄.

2. AuthenticationFilter(사용할 구현체 UsernamePasswordAuthenticationFilter)가 HttpServletRequest에서 사용자가 보낸 아이디와 패스워드를 인터셉트한다. 프론트에서 유효성검사rk 가능하지만, 보안을 위해 사용자가 보낸 아이디와 패스워드의 유효성 검사를 해줄 수 있다.(아이디 혹은 패스워드가 null인 경우 등) HttpServletRequest에서 꺼내온 사용자 아이디와 패스워드를 진짜 인증을 담당할 AuthenticationManager 인터페이스(구현체 - ProviderManager)에게 인증용 객체(UsernamePasswordAuthenticationToken)로 만들어줘서 위임한다.

3. AuthenticationFilter에게 인증용 객체(UsernamePasswordAuthenticationToken)을 전달받는다.

4. 실제 인증을 할 AuthenticationProvider에게 Authentication객체(UsernamePasswordAuthenticationToken)을 다시 전달한다.

5. 인증 절차가 시작되면 AuthenticationProvider 인터페이스가 실행됨 -> DB에 있는 이용자의 정보와 화면에서 입력한 로그인 정보를 비교하게 됨.

6. AuthenticationProvider 인터페이스에서는 authenticate() 메소드를 오버라이딩 하게 되는데 이 메소드의 파라미터인 Authentication 으로 화면에서 입력한 로그인 정보를 가져올 수 있다.

7. AuthenticationProvider 인터페이스에서 DB에 있는 이용자의 정보를 가져오려면, UserDetailsService 인터페이스를 사용한다.

8. UserDetailsService 인터페이스는 화면에서 입력한 이용자의 이름(username)을 가지고 loadUserByUsername() 메소드를 호출하여 DB에 있는 이용자의 정보를 UserDetails 형으로 가져온다. 만약 이용자가 존재하지 않으면 예외를 던진다. 이렇게 DB에서 가져온 이용자의 정보와 화면에서 입력한 로그인 정보를 비교하게 되고, 일치하면 Authentication 참조를 리턴하고, 일치 하지 않으면 예외를 던진다.

9. 인증이 완료되면 사용자 정보를 가진 Authentication 객체를 SecurityContextHolder에 담은 이후 AuthenticationSuccessHandle를 실행한다.(실패시 AuthenticationFailureHandler를 실행한다.)

## (UsernamePassword)AuthenticationFilter
인증(authentication) 요청을 Spring Security에서 처리할 수 있도록 Authentication 객체로 변환시킨 뒤 이를 AuthenticationManager로 처리를 위임한다.

인증 성공 시, 얻은 Authentication 객체를 SecurityContext에 저장 후 AuthenticationSuccessHandler 실행

인증 실패 시, AuthenticationFailureHandler 실행

## AuthenticationManager
(implementation: ProviderManager)

AuthenticationFilter에서 받은 Authentication 객체를 처리할 수 있는 AuthenticationProvider를 찾아 인증 처리를 위임한다.

## AuthenticationProvider
DB 정보와 화면에서 client 정보 비교

Spring Security의 AuthenticationProvider을 구현한 클래스로 security-context에 provider로 등록 후 인증절차를 구현

ID/PW 방식을 처리하기 위해 사용할 수 있는 기본 Spring Security Authentication와 AuthenticationProvider는 다음과 같다.

Authentication: UsernamePasswordAuthenticationToken
AuthenticationProvider: DaoAuthenticationProvider (AbstractUserDetailsAuthenticationProvider class)
ID/PW 방식의 경우 UserDetaile, UserDetailsService와 PasswordEncoder가 필요하다.


login view에서 login-processing-url로의 form action 진행 시 해당 클래스의 supports() > authenticate() 순으로 인증 절차 진행

## UserDetailsService
UserDetailsService 인터페이스는 DB에서 유저 정보를 가져오는 역할을 한다. UserDetails를 username(ID)로 조회하기 위해 사용(loadUserByUsername 메서드)되는 interface

## UserDetails
username(ID), 암호화된 password를 포함한 인증하고자하는 유저의 인증 정보를 담는 interface이다. 직접 상속받아 사용하면된다.

UserDetails 인터페이스를 구현하게 되면 오버라이드되는 메소드들이 있다. 이 메소드들에 대해 파악을 해야 된다. 그리고 회원 정보에 관한 다른 정보(이름, 나이, 생년월일, ...)도 추가해도 된다. 오버라이드되는 메소드들만 Spring Security에서 알아서 이용하기 때문에 따로 클래스를 만들지 않고 멤버변수를 추가해서 같이 사용해도 무방하다. 만든 멤버변 수들은 getter, setter를 만들어서 사용하면 된다.

## PasswordEncoder
UserDetailsService를 통해 조회한 UserDetails의 암호화된 password와

인증 요청인 Authentication의 credential(raw password)의 일치 여부를 비교할 수 있는 객체이다.

## SecurityContext
현재 Thread에 Security 정보(Authentication)를 담는 역할을 한다.

(SecurityContextHolder 를 통해 불러올 수 있다.)

Thread Pooling을 하는 경우 Thread를 재사용하기 때문에,

SecurityContext를 사용하고 해당 Thread를 Thread Pool에 반환 전에 SecurityContext를 비워줘야한다.

(using SecurityContextHolder.clearContext())

##  Filter Chain

![필터](https://velog.velcdn.com/post-images%2Fhellas4%2Fb5481370-0353-11ea-b54d-d395bd3279f1%2F14.png)
 

 



## Login Form 인증 로직 플로우
1. UsernamePasswordAuthenticationFilter
로그인 인증처리를 담당하고 인증처리에 관련된 요청을 처리하는 필터

![로직](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fd2a33003-6201-4a12-8752-c3913a80dfa0%2Floginform_.png&blockId=6cf6c762-5858-46aa-afb1-77fa8b29ae89) 
1. AntPathRequestmatcher(/login)
→ 사용자가 요청한 요청정보를 확인하여 요청정보 Url이 /login으로 시작하는지 확인한다. 
요청한다면 다음단계로(인증처리) 진행되고, 일치하지 않는다면 다음 필터로 진행된다.(chain.doFilter)
/login url은 .loginProcessingUrl()으로 변경 가능하다.

2. Authentication 에서 실제 인증처리를 하게 되는데, 로그인 페이지에서 입력한 Username과 Password를 인증객체(Authentication)에 저장해서 인증처리(AuthenticationManager)를 맡기는 역할을 한다.
→ 여기까지가 인증처리를 하기전에 필터가 하는 역할. 

3. 인증관리자(AuthenticationManager)는 내부적으로 AuthenticationProvider 에게 인증처리를 위임하게 된다. 해당 Provider가 인증처리를 담당하는 클래스로써 인증에 성공/실패를 반환하는데 실패할 경우 AuthenticationException  예외를 반환하여 UsernamePasswordAuthenticationFilter로 돌아가서 예외처리를 수행하고, 인증에 성공하게 되면, Authentication 객체를 생성하여 
User객체와 Authorities객체를 담아서 AuthenticationManager에게 반환한다. 

4. AuthenticationManager는 Provider로부터 반환받은 인증객체(인증결과 유저(User), 유저권한정보(Authorities))를 SecurityContext객체에 저장한다. 

5. SecurityContext는 Session에도 저장되어 전역적으로 SecurityContext를 참조할 수 있다. 

6. 인증 성공 이후에는 SuccessHandler에서 인증 성공이후의 로직을 수행하게 된다. 
정리

: 인증처리 필터(UsernamePasswordAuthenticationFilter)는 Form인증처리를 하는 필터로써 해당 필터는 크게 두가지로 인증전과 인증후의 작업들을 관리한다. 
인증처리전에는 사용자 인증정보를 담아서 전달하면서 인증처리를 맡기고(AuthenticationManager) 성공한 인증객체를 반환받아서  (전역적으로 인증객체를 참조할 수 있도록 설계 된)SecurityContext에 저장하고, 그 이후 SuccessHandler를 통해 인증 성공후의 후속 작업들을 처리

해당 블로그 참조 : https://catsbi.oopy.io/c0a4f395-24b2-44e5-8eeb-275d19e2a536
