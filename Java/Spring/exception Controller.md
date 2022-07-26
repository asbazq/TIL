# @ExceptionHandler

@ExceptionHandler같은 경우는 @Controller, @RestController가 적용된 Bean내에서 발생하는 예외를 잡아서 하나의 메서드에서 처리해주는 기능을 한다.
→ @ExceptionHandler({ Exception1.class, Exception2.class}) 이런식으로 두 개 이상 등록

**주의사항/알아 둘 것**

- Controller, RestController에만 적용가능하다. (@Service같은 빈에서는 안됨.)
- 리턴 타입은 자유롭게 해도 된다. (Controller내부에 있는 메서드들은 여러 타입의 response를 할 것이다. 해당 타입과 전혀다른 리턴 타입이어도 상관없다.)
- @ExceptionHandler를 등록한 Controller에만 적용된다. 다른 Controller에서 NullPointerException이 발생하더라도 예외를 처리할 수 없다.
- 메서드의 파라미터로 Exception을 받아왔는데 이것 또한 자유롭게 받아와도 된다.
