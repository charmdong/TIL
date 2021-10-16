# Mixed Content issue



> **Mixed Content 이슈란?**

* Chrome, Firefox에서 https로 통신 중 http로 연결되는 통신이 발생하는 경우 보안정책에 의해 browser가 block되는 현상.
* 하나의 웹 페이지 안에 포함된 여러 컨텐츠들 중 일부는 https, 일부는 http로 가져오는 경우 발생한다.
* 간단하게 말해, 안전한 페이지에서 안전하지 않은 페이지에 접근하려해 발생한다.
* 해당 이슈 발생시 콘솔창에서 확인되는 에러 메시지는 아래와 같다.

> Mixed Contet: The page at '<mark style="color:orange;">https</mark>://...' was loaded over HTTPS, but requested as insecure XMLHttpRequest endpoint '<mark style="color:green;">http</mark>://...'. This request has been blocked; the content must be served over HTTPS. 

 

> **해결 방법**

1\. <mark style="color:blue;">**사용자**</mark>가 해결하는 방법

[참고: 브라우저에서 혼합 컨텐츠를 사용하려면 어떻게 해야 합니까? | Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/mixed-content.html?lang=ko-KR#experiences)

 

2\. <mark style="color:orange;">**개발자**</mark>가 해결하는 방법

서비스하는 웹 페이지의 코드 중 <mark style="color:green;">http</mark>로 가져오는 컨텐를 <mark style="color:orange;">https</mark>로 가져오도록 수정한다. (단, 해당 페이지가 https로 구현되어 있지 않은 경우, https로 수정하더라도 실제로는 http로 접근하게 되는 것 같다.)
