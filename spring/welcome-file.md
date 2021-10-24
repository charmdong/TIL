# Welcome file

### 1. Welcome file 설정하기

![\[사진 1.1\] 경로 찾기](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2\&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuTehy%2Fbtq3GCo409g%2F8zkgCbCAcTvvLtX1XEzJuk%2Fimg.png)

![\[사진 1.2\] web.xml 에서 welcome 파일 경로 추가해주기](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2\&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F3e4ON%2Fbtq3EJCpaEn%2FK8WDp449rncNkFjT6kbRkK%2Fimg.png)

* **\[사진 1.2]** 에서와 같이 <mark style="color:blue;">**web.xml**</mark> 파일에 <mark style="color:blue;">**welcome-file-list**</mark>를 설정해줘야 합니다. **welcome-file-list**는 <mark style="color:orange;">**Document Root**</mark>**를 기준으로 파일을 탐색**하게 됩니다. 저의 프로젝트 경우, **\[사진 1.1]** 과 같이 구조를 이루고 있습니다. 즉, **Document Root**는 **src/main/webapp**이 됩니다. 저는 /WEB-INF/view 에 위치한 hello.jsp 파일을 시작 페이지로 설정하고자 했으며, **\[사진 1.2]** 에서 4번째 welcome-file에 해당 파일의 경로를 정확하게 기재해줬습니다.

![\[사진 2\] Server의 module 탭에서 Path 수정하기](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2\&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtbhFZ%2Fbtq3FmAbZcD%2Fei0ujebDPcf6tcfYGoZPsk%2Fimg.png)

* 만약 현재 프로젝트가 올라가 있는 Server의 설정을 변경한 적이 없다면, 해당 Server의 **Path**는 "<mark style="color:blue;">**/프로젝트명**</mark>" 으로 되어있을 것입니다. 이런 경우, 1번까지 진행했다면 "localhost:8080/프로젝트명" 으로 접속해야 시작 페이지를 만날 수 있습니다. 여기서 나는 "localhost:8080" 으로만 시작 페이지를 만나고 싶다? 하신다면 \*\*\[사진 2]\*\*에서와 같이 Eclipse의 Server 탭에서 실행할 프로젝트가 올라가 있는 서버 설정 -> module -> 해당 프로젝트 Path를 "/" 로 Edit 해주시면 됩니다.

> 저는 서버의 기본 포트를 8080으로 사용하고 있으며, 이해를 돕기 위해 기본적으로 사용하는 포트인 8080을 기준으로 글을 포스팅한 점 참고바랍니다. 자신이 서버의 포트 번호를 수정한 경우, localhost:설정한port번호 로 접속해주시면 됩니다!
