# Docker

### 도커 이미지와 컨테이너

도커 이미지

* 코드, 런타임, 시스템 도구, 시스템 라이브러리 및 설정과 같은 응용프로그램을 실행하는 데 필요한 모든 것을 포함하는 소프트웨어 패키지를 말한다.

도커 컨테이너

* 도커 이미지의 인스턴스이다.
* 응용프로그램을 실행한다.

***

### 도커 work flow

1. 도커 클라이언트가 도커 서버에 실행하고자 하는 이미지를 명령어 기반으로 전달한다.
2. 로 내 이미지 캐시 저장소에서 해당 이미지를 탐색한다.
3. 캐시 저장소에 실행하려는 이미지가 존재한다면 실행하고, 그렇지 않으면 도커 허브에서 이미지를 탐색해 캐시 저장소로 가져온 뒤 실행한다.

***

### 컨테이너 생성

* 도커 이미지는 사용하고자 하는 프로그램에 필요한 파일을 포함한다.
  * 스냅샷: 프로그램 설치에 필요한 파일
  * 실행 명령어: 스냅샷이 컨테이너에 적재된 뒤, 해당 프로그램을 실행하는 명령어

1. 도커 클라이언트 - docker run \[이미지명]
2. 도커 이미지에 있는 스냅샷을 컨테이너 HD에 적재한다.
3. run \[실행할 프로그램명] 명령어를 실행해준다.



### 도커 클라이언트 명령어

* docker run \[이미지명] \[명령어]
  * 명령어 자리가 비어 있지 않다면 이미지가 지니고 있는 시작 명령어를 무시하고 해당 명령어를 실행.
  * 이미지 내 존재하는 명령어만 사용할 수 있다.
* docker ps
  * 현재 실행 중인 컨테이너 목록 확인
  * \-a : 모든 컨테이너 목록 조회
* docker run \[이미지명] : docker create \[이미지명] + docker start \[컨테이너 아이디/이름]
  * docker create \[이미지명] : 컨테이너가 생성되면서 아이디를 출력한다.
  * docker start \[컨테이너 아이디/이름] : 컨테이너 실행
    * \-a :
* docker stop : 컨테이너가 하던 작업을 완료하고 중지시킨다.
  * SIGTERM(종료 신호) → SIGKILL(15) → Main process
* docker kill : 바로 컨테이너를 종료시킨다.
  * SIGKILL → Main process
* docker rm \[컨테이너 아이디/이름] : 컨테이너 삭제
  * 중지 상태의 컨테이너만 삭제할 수 있다.
  * docker rm ‘docker ps -a -q’ : 중지 상태 컨테이너 모두 삭제
* docker rmi \[이미지 ID] : 이미지 삭제
* docker system prune : 도커를 사용하지 않는 경우 컨테이너, 이미지, 네트워크 삭제
  * 중지 상태 컨테니어만 정리됨
* 실행 중인 컨테이너에 명령어 전달하기
  * docker exec \[컨테이너 아이디] \[실행할 명령어]
  * \-it : interactive terminal → 계속 명령어를 적을 수 있게 해주는 옵션

***

### 도커 이미지 생성 순서

1. dockerfile 작성
   * 설정 파일
   * 컨테이너가 어떻게 실행돼야 하는 지에 대한 설정 정의
2. 도커 클라이언트 전달 (임시 컨테이너)
   * dockerfile에 입력된 정보 전달
3. 도커 서버 전달 (임시 컨테이너)
4. 이미지 생성

***

### Dockerfile

* 도커 이미지를 만들기 위한 설정 파일
* 작성 순서
  1. 베이스 이미지 명시 (파일 스냅샷에 해당됨)
  2. 추가적으로 필요한 파일을 다운로드하기 위한 명령어를 명시 (파일 스냅샷에 해당됨)
  3. 컨테이너 시작시 실행 될 명령어 명시
* 베이스 이미지
  * 도커 이미지는 여러 개의 레이어로 구성되는데, 그 중 기반이 되는 이미지를 말한다.
  * 레이어 : 중간 단계의 이미지라고 생각하면 된다.
*   구성

    FROM

    * \[이미지명]:\[태그] 형식으로 작성한다.
    * 태그를 붙이지 않으면 자동으로 최신 버전으로 다운 받음.

    RUN

    * 도커 이미지가 생성되기 전에 수행할 쉘 명령어
    * 추가 파일 다운로드

    CMD

    * 컨테이너 시작 시 실행할 파일 혹은 셸 스크립트
    * 해당 명령어는 Dockerfile 내 1회만 사용 가능.



### Dockerfile → Docker Image

docker build ./ or .

* 해당 디렉토리 내에서 dockerfile이라는 파일을 찾아 도커 클라이언트에 전달해준다.

순서

1. 이미지 생성
2. 임시 컨테이너 생성
   1. 새로운 명령어
   2. 새로운 파일 스냅샷
3. 새로운 이미지 생성

도커 이미지에 이름 부여

* docker build -t 계정명/저장소 or 프로젝트명:버전 - 관례

이름으로 도커 이미지 실행하기

* docker run 계정명/저장소 or 프로젝트명

docker run -p \[로컬에서 사용할 포트] : \[컨테이너에서 사용할 포트]

* localhost:\[로컬에서 사용할 포트] 로 접속 시 컨테이너에서 사용할 포트로 매핑

WORKDIR

* 이미지 안에서 어플리케이션 소스 코드를 갖고 있을 디렉토리
* 따로 지정해주지 않으면 모든 파일들이 root 디렉토리 내 위치하게 된다. 만약 이미지에 동일한 이름의 파일이 존재하는 경우, COPY 과정에서 파일이 덮어씌워지는 문제가 발생할 수 있다.

### Docker Volume

* 도커 컨테이너에서 로컬에 위치하는 파일을 참조하도록 함.
* 복사를 통해 빌드 시, 수정이 발생할 때 마다 재빌드가 필요하다는 불편함을 해결하기 위한 방법이다.
* 처음 컨테이너 생성 시를 제외하고 수정이 발생할 경우 로컬 파일을 참조하도록 옵션을 줘 도커 컨테이너를 실행하는 방법이다.
