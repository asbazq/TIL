java: class Main is public, should be declared in a file named Main.java
public class는 고유명사,

Exception in thread "main" java.lang.NullPointerException 

at aa.bb.cc.NullPointerException.main(NullPointerException.java:7) 와 같은 에러가 뜬다. 왜냐면, java.lang 패키지 안에 있는 클래스인 Integer의 참조변수인 myInteger가 null값을 가지니 intValue()를 불러오는데 에러가 생긴 거다. 혹은 변수 크기 미설정



 코드 myInteger는 null값이 아닌 다른 값을 이용하려고 하는데 null값이니 에러가 날 수 밖에 없는 것이다.

 

 위와 같이 간단한 코드는 틀린 점을 쉽게 찾을 수 있지만, 초기화가 필요한 경우나 커넥션을 이용하는 코드 같은 경우 꾀나 골탕을 먹힌다. 보통 코드를 다시 살펴보거나 차례대로 코드를 해석하면 이런 실수는 덜 할 것 같다.



~ cannot find(resolve) to ~

 코드에서 변수나 메서드를 찾을 수 없다는 에러문이다. 선언하지 않은 변수 혹은 메서드를 사용했거나, 변수나 메서드의 이름을 잘못 사용했을 때 일어나는 에러이다. 



 이클립스 같은 경우 해당 변수나 메서드에 주로 더블 클릭하거나 그 변수나 메서드에 마우스를 가져다 댔을때 하이라이트가 먹힌다. 이것을 이용해 틀리게 입력한 메서드나 변수를 쉽게 찾을 수 있다.



 또한, Ctrl + 클릭 시 해당 메서드의 내용으로 페이지가 옮겨가는데, 만약 Ctrl + 클릭이 먹지 않으면 그 메서드가 잘못 된 것을 쉽게 알 수 있다.



';' expected

 세미콜론 (';')이 필요하다는 뜻이다. 주로 타자를 잘못 치거나 가끔 문장에 세미콜론을 빠뜨렸을 때 나타나는 에러다.



Exception in thread "main" java.lang.NoSuchMethodError: main

 main 메서드를 찾지 못했을 때 일어나는 에러다. main이 존재하지 않거나 선언부(public static void main(String[] args))가 잘못 선언되면 일어나는 에러다. 

 main 메서드가 잘 선언되있는지 살펴보면 될 것이다.



Multiple markers at this line

 문장에 문법적 오류가 있을때 일어나는 에러다. 괄호, 수식, if문 for문 같은 문법적 오류와 private이나 static와 같은 키워드 차원에서도 일어난다.
 
 java: cannot find symbol
실행구문의 생성자가 pubic class의 이름과 다르다.
 
 missing return statement
 
 모든 경우에 대한 return 값을 가지도록 한다.
 
 expected "identifier"; SQL statement
 
 테이블 이름과 SQL명령어 중복
 테이블 이름을 바꾸거나 @Table(name = "")을 사용한다
