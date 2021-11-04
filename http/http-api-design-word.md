# HTTP API Design Word

### 문서 (document)

* 하나의 파일, 객체 인스턴스, DB row과 같은 단일 개념을 말한다.
* ex) /files/image.png



### 컬렉션 (collection)

* 서버가 관리하는 리소스 저장소를 말한다.
* 서버가 리소스의 URI를 생성하고 관리한다.
* POST 방식을 통해 신규 리소스를 생성시에 사용되는 URI 타입이다.
* ex) /users



### 스토어 (store)

* 클라이언트가 관리하는 리소스 저장소를 말한다.
* 클라이언트가 리소스의 URI를 인지하고 관리한다.
* 파일같은 리소스를 관리할 때 사용된다.
* ex) /files



### 컨트롤 URI

* 위 3개의 개념으로 해결하기 어려운 프로세스를 실행하기 위해 사용되는 개념이다.
* URI에 동사를 이용해 사용한다.
* ex) /users/{id}/delete
