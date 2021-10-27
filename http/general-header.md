# General Header

### **Header 종류**

> 1. General Header: **메시지 전체에 적용되는 정보**에 대한 표현
> 2. Request Header: **요청**에 대한 정보
> 3. Response Header: **응답**에 대한 정보
> 4. Entity Header: **Entity Body에 대한 정보** ex) Content-type: application/json

HTTP message는 <mark style="color:blue;">**Header**</mark>와 <mark style="color:purple;">**Body**</mark>로 구성되는데, 각각을 <mark style="color:blue;">**표현 헤더**</mark>와 <mark style="color:purple;">**표현 데이터**</mark>라고 칭한다. 표현이란 요청이나 응답에서 전달하는 실제 데이터를 말하며, <mark style="background-color:yellow;">**표현 헤더는 표현 데이터를 해석할 수 있도록 데이터 유형, 데이터 길이와 같은 정보를 제공**</mark>**한다.**

### ****

### **표현 헤더**

> **• Content-Type**: 표현 데이터의 타입\
> 미디어 타입, 문자 인코딩 정보를 넣어준다. ex) text/html; charset=utf-8, application/json
>
> **• Content-Encoding**: 표현 데이터의 압축 방식\
> 데이터를 전달하는 곳에서 Body 부분을 압축 한 뒤, 전달받는 곳에서 어떻게 압축했는지를 알기 위해 인코딩 정보를 제공한다.\
> ex) gzip
>
> **• Content-Language**: 표현 데이터의 자연어\
> 표현 데이터의 자연 언어에 대한 정보를 제공한다. ex) ko, en
>
> **• Content-Length**: 표현 데이터의 길이\
> 바이트 단위로 데이터의 길이 정보를 제공한다.

***

### **Content negotiation**

> 클라이언트가 요청 시에 <mark style="color:blue;">**선호하는 표현 형식에 대한 정보**</mark>를 제공한다. (요청 시에만 사용된다.)
>
> **• Accept**: 선호하는 미디어 타입\
> **• Accept-Charset**: 선호하는 문자 인코딩 방식\
> **• Accept-Encoding**: 선호하는 압축 인코딩 방식\
> **• Accept-Language**: 선호하는 자연어

### ****

### **우선순위**

> 만약 클라이언트가 선호하는 자연어를 지정해 요청을 했으나, 서버에서는 해당 자연어에 대한 지원이 없는 경우에는 서버에서 기본 값으로 설정되어 있는 자연어로 응답하게 될 것이다. 따라서, 선호하는 자연어에 대한 우선순위를 지정해 요청을 보내면, 서버에서 지원하는 언어 중 우선순위가 높은 언어로 응답해줄 수 있다.
>
> *   **q값을 사용한 우선순위 설정**\
>     ![](<../.gitbook/assets/image (4).png>)
>
>     0\~1 사이의 수를 사용하고, 클수록 높은 우선순위를 갖는다.
>
>
>
> *   **구체적인 타입 명시**\
>     ![](<../.gitbook/assets/image (1).png>)
>
>     구체적으로 명시된 것이 높은 우선순위를 갖는다.

***

### **일반 정보**

> **• Referer**: <mark style="background-color:blue;">**이전 웹 페이지 주소**</mark>\
> \- 현재 요청된 페이지의 이전 웹 페이지 주소에 대한 정보를 갖는다.\
> \- 유입 경로 분석이 가능하다.\
> \- 요청에서만 사용된다.

***

### **특별 정보**

> **• Host**\
> <mark style="background-color:blue;">**요청 시에 필수적으로 사용해야 하는 헤더**</mark>로, _하나의 서버에는 여러 개의 도메인이 존재할 수 있기 때문에 서버의 어떤 도메인으로 요청을 날리는 것인지를 명시_해줘야 한다.\
>
>
> ![](<../.gitbook/assets/image (2).png>)
>
> \
> **• Location**: 리다이렉션할 경로\
> **• Allow**: 허용 가능한 HTTP Method\
> **• Retry-After**: User Agent가 다음 요청을 하기까지 기다려야 하는 시간\
> \- 503 (Service Unavailable) 서비스가 언제까지 사용 불가능한 지 알려줄 수 있음.\
> ex) Retry-After: Fri, 31 Dec 2021 23:59:59 GMT (날짜 표기) / Retry-After: 120 (초 단위 표기)

***

### **인증**

> **• Authorization**\
> \- 클라이언트의 인증 정보를 서버에 전달한다.
>
> **• WWW-Authenticate**\
> \- 리소스에 접근하기 위해 필요한 인증 방법에 대해 정의\
> \- 401 (Unauthorized) 와 함께 사용된다.
