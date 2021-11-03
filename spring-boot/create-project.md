# Create Project

### **1. STS(Spring Tool Suite) 플러그인 설치**

STS를 직접 설치해서 사용한다면 문제될 것 없지만, Eclipse를 통해 스프링을 사용하려면 스프링 전용 개발 도구인 STS 플러그인을 설치해야 한다.&#x20;

> 1. \[Help] → \[Eclipse Marketplace...] 메뉴를 선택한다.
> 2. 검색창에 'sts'를 입력후 검색한다.
> 3. STS에 해당하는 플러그인의 INSTALL을 눌러 설치를 진행한다.
> 4. 인증 관련 화면이 뜨면 \<Select All> 버튼을 누르고 \<Accept selected> 버튼을 눌러 마무리한다.
> 5. 설치가 마무리 되면 Eclipse를 재기동할 것인지 물어보는데, 이 때 \[Restart Now]를 눌러 재기동해준다.

&#x20;

### **2. Spring Boot 프로젝트 생성하기**

STS 플러그인 설치가 완료되었다면, Perspective를 변경해야 한다.

> \[Window] → \[Perspective] → \[Open Perspective] → \[Other]에서 Spring을 선택해준다.

이제 Spring Boot 프로젝트를 생성를 해보자.

> \[File] → \[New] → \[Spring Starter Project]를 선택하자.\
> Pacakage Explorer에서 우클릭 → \[New] → \[Spring Starter Project]로도 가능하다.

![\[사진 1. Spring Starter Project 생성 - 1\]](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2\&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd7pdrM%2FbtrbllfCtW8%2FwXykamXZN1fDIQS5nXOmU1%2Fimg.png)

스프링 부트에서는 라이브러리 관리와 빌드 자동화 도구로 Maven과 Gradle을 지원한다. 따라서 자신이 사용할 도구를 선택하면 되겠다. 또한, 스프링 부트는 웹 애플리케이션도 <mark style="background-color:orange;">**Jar 파일로 패키징해 실행이 가능**</mark>하다.

![\[사진 2. Spring Starter Project 생성 - 2\]](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2\&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbcKQAm%2FbtrbosZDN9H%2FdtwMe5RxPBcNrPU1aSLF7K%2Fimg.png)

프로젝트의 이름과 라이브러리 관리 및 빌드 자동화 도구, 패키징 파일 타입 등을 선택하고 나면 의존성을 선택할 차례이다. Spring Boot의 버전을 선택할 수 있고, 프로젝트에 필요한 라이브러리 의존성을 추가할 수 있다. 의존성을 선택한 후 \[Finish]를 누르면 프로젝트 생성이 완료된다.
