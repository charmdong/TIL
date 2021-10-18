# TCP

### TCP

> 1. 장치들 사이에 논리적인 접속을 성립하기 위한 연결을 설정해 <mark style="color:orange;">**신뢰성을 보장하는 연결형 서비스**</mark>이다.
> 2. 데이터 순서를 보장한다.
>    * 서버에서 패킷 순서가 잘못 도착한 경우, 잘못된 순서부터 다시 보내라고 요청
> 3. 3 way handshaking 과정을 통해 연결 설정, 4 way handshaking을 통해 연결 해제

#### 3 way handshaking

* TCP 통신을 이용해 데이터를 전송하기 위해 <mark style="color:blue;">**네트워크 연결을 하는 과정**</mark>이다.
* 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 실제로 데이터 전달이 시작하기 전에 한 쪽이 다른 쪽에 준비되었다는 것을 알 수 있도록 하는 것이다.
* 과정
  1. A -> B (SYN): 접속 요청 프로세스 A가 <mark style="color:green;">**연결 요청**</mark> 메시지를 전송한다.
  2. B -> A (SYN + ACK): 접속 요청을 받은 프로세스 B가 <mark style="color:blue;">**요청을 수락**</mark>하고 접속 요청 프로세스 <mark style="color:green;">**A에게 포트를 열어 달라는 메시지를 전송**</mark>한다.
  3. A -> B (ACK): 접속 요청 프로세스 A가 <mark style="color:green;">**수락 확인을 보내 연결**</mark>을 맺는다.

#### 4 way handshaking

* TCP <mark style="color:red;">**연결을 해제하는 과정**</mark>이다.
* 과정
  1. A -> B (FIN): A가 <mark style="color:orange;">**연결을 종료하겠다는 FIN 플래그를 전송**</mark>한다. 
     * B가 FIN 플래그로 응답하기 전까지 연결을 유지한다. (FIN_WAIT)
  2. B -> A (ACK): B가 <mark style="color:orange;">**확인 메시지를 전송**</mark>하고 자신의 통신이 끝나길 기다린다. (TIME_WAIT)
  3. B -> A (FIN): B가 <mark style="color:orange;">**통신이 끝났으면 연결 종료 요청을 수락**</mark>한다는 의미로 A에게 FIN 플래그를 전송한다.
  4. A -> B (ACK): A가 <mark style="color:orange;">**확인했다는 메시지를 전송**</mark>한다.

