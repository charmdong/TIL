# Cookie, Session

### **Cookie**

> * HTTP의 일종으로 사용자가 웹 사이트를 방문할 경우 그 사이트의 서버에서 <mark style="background-color:blue;">**사용자의 PC에 저장하는 정보**</mark>이다.
> * 클라이언트 PC에 텍스트 파일로 저장되어 해당 웹 사이트를 다시 방문했을 경우 이 정보를 사용한다.
> * 클라이언트 PC에 저장되기 때문에 다른 사용자에 의해 <mark style="background-color:red;">**임의로 변경이 가능해 보안 취약점**</mark>이 존재한다.

* 동작 순서
  1. Client가 페이지를 요청한다.
  2. 웹 서버에서 쿠키를 생성한다.
  3. 생성한 쿠키에 정보를 담아 요청에 응답할 때 Client에게 쿠키를 전달한다.
  4. 전달된 쿠키는 Client PC에 저장된다.
  5. <mark style="background-color:blue;">**전달받은 쿠키는 Client가 웹 서버에 요청을 보낼 때 함께 전송**</mark>된다.
  6. Client가 동일 웹 사이트에 재방문 시, Client PC에 쿠키가 있는 경우 요청 페이지와 함께 쿠키를 전송한다.
* 구성 요소
  * Name: 쿠키의 이름
  * Value: 쿠키에 저장된 값
  * Expired: 쿠키의 만료 기간으로, 지정된 만료일이 되면 디스크에서 쿠키가 제거된다.
  * Domain: 쿠키가 사용되는 도메인
  * Path: 쿠키를 반환할 경로 (설정된 path로 접속 시, 쿠키가 전송된다.)
  * Secure: 보안 연결 설정
  * HttpOnly: HTTP외 다른 통신 사용 가능 설정

 

### **Session**

> * HTTP의 일종으로 사용자가 접속한 웹 사이트 <mark style="background-color:blue;">**서버에 저장되는 정보**</mark>다.
> * 서버에서 클라이언트에게 쿠키를 전달할 때 <mark style="background-color:blue;">**Session ID에 대한 정보도 함께 쿠키**</mark><mark style="background-color:blue;">에 담아 전달</mark>한다.
> * **브라우저를 닫거나** (application 종료) **서버에서 삭제 시에만 삭제**가 된다.
> * 서버에 저장되는 정보이므로 <mark style="background-color:blue;">**쿠키에 비해 보안성이 좋다**</mark><mark style="background-color:blue;">.</mark>
> * 모든 정보를 세션에 저장하게 되면 서버의 메모리 과부하를 초래할 수 있기에 Session만을 사용하지는 않는다.

\- 동작 순서

1. 클라이언트가 서버에 페이지 요청
2. 서버에서 Request-Header의 Cookie를 확인해 Session ID를 보냈는지 확인
3. 존재하지 않으면 생성해서 전송
4. 서버에서 클라이언트로 돌려준 Session ID를 쿠키를 사용해 서버에 저장 (JSESSIONID)
5. 클라이언트 재접속 시, 쿠키 이용해 session id 전송
