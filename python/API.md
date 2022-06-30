# API

은행의 창구가 API와 같다. 같은 예금 창구에서도 개인 고객이냐 기업 고객이냐에 따라 처리하는 것이 다른 것처럼, 클라이언트가 요청 할 때에도, "방식"이 존재한다. 
HTTP 라는 통신 규약을 따라, 클라이언트는 요청할 때 HTTP request method(요청 메소드)를 통해, 어떤 요청 종류인지 응답하는 서버 쪽에 정보를 알려준다. 
이를 통해 프로트엔드와 백엔드가 주고받는다.

## 0. HTTP 요청메소드

[여러방식](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods)이 존재하지만, 가장 많이 쓰이는 GET, POST 방식을 본다.

* GET → 통상적으로! 데이터 조회(Read)를 요청할 때
         예) 영화 목록 조회

* POST → 통상적으로! 데이터 생성(Create), 변경(Update), 삭제(Delete) 요청 할 때
          예) 회원가입, 회원탈퇴, 비밀번호 수정