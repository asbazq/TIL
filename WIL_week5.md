# 회고

이번 주의 과제는 배달 api를 만드는 것이었다. 

저번 주가 jwt를 활용한 api를 만드는 것이었다면 이번에는 1. 음식점 등록 및 조회 2. 음식 등록 및 메뉴판 조회 3. 주문하기 구현으로 조금 더 api에 치중한 느낌이다.

단순 조회 등록 api라서 어려움없이 구현할 수 있어는데 마지막 주문하기에서 조금 시간이 걸렸다. 

간단한 구현인데 생각보다 많은 부속물이 필요했고 해당 dto나 model문제로 조금 고민이 많았다. 

하지만 이번 과제를 하면 api에 대해 처음부터 생각해보고 구현해보니 api에 구조에대한 이해도를 높일 수 있던 것 같다.

# 교차 출처 리소스 공유(Cross-Origin Resource Sharing, CORS)

CROS는 추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제다.

웹 애플리케이션은 리소스가 자신의 출처(도메인, 프로토콜, 포트)와 다를 때 교차 출처(다른 출처) HTTP 요청을 실행한다.

## Same Origin / Cross Origin 차이

웹에는 크게 SOP(Same Origin Policy)와 CORS(Cross Origin Resurce Sharing) 두가지 정책이 있다.

프로토콜, 포트, 호스트 모두 동일하다면 Same Origin이며, 이들중 하나라도 일치하지 않으면 Cross Origin 이 된다.

ex)

- HTML → 기본적으로 Cross-Origin 정책을 따름
  - link 태그의 href에서 다른 origin의 css 등의 리소스에 접근하는 것이 가능
  - img 태그의 src에서 다른 리소스에 접근하는 것이 가능

- XMLHttpRequest, Fetch API 등 script 태그 내 → 기본적으로 Same-Origin 정책을 따름
  - 자바스크립트는 서로 다른 도메인에 대한 요청을 보안상 제한한다. (브라우저 기본 설정은 하나의 서버 연결만 허용)
  - 이 정책을 Same-Origin-Policy라고 한다.


출처: https://inpa.tistory.com/entry/WEB-📚-CORS-💯-정리-해결-방법-👏 [👨‍💻 Dev Scroll:티스토리]
