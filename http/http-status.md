# HTTP Status

### **2XX - 요청 정상 처리**

> **• 201 Created**\
> \- 요청이 성공적으로 처리되어 <mark style="color:orange;">**새로운 리소스가 생성**</mark>되었음을 의미한다.\
> \- 생성된 리소스는 응답의 <mark style="color:orange;">**Location 헤더 필드**</mark>로 식별할 수 있다.\
> \- <mark style="color:orange;">**POST 요청**</mark>으로 신규 리소스를 생성했을 때 응답이다.\
> \
> **• 204 No Content**\
> \- 요청을 성공적으로 처리했으나, 응답 Payload에 보낼 데이터가 없음을 의미한다.\
> \- 웹 문서 편집기에서 \[저장]을 요청할 경우가 대표적인 예시이다.\
> \- \[저장]의 결과로 어떤 내용도 없어도 괜찮다.\
> \- \[저장]을 하더라도 같은 화면을 유지해야 한다.

***

### **3XX (Redirection) - 요청을 완료하기 위해서 추가 행동이 필요**

> • 웹 브라우저는 <mark style="color:blue;">**3XX 응답에 Location 헤더가 존재하면, Location 위치로 이동**</mark>한다.\
> \
> **◆ 영구 Redirection**\
> \- 특정 리소스의 URI가 영구적으로 이동함\
> \- 기존 URL은 더 이상 사용하지 않는다. \
> \- 실무에서 사용할 일 드물다.\
> \
> **• 301 Moved Permanently**\
> \- 리다이렉트 시, 요청 메서드가 <mark style="color:purple;">**GET으로 변경되고, 본문이 제거될 수도 있다**</mark><mark style="color:purple;">.</mark> (반드시 변경되는 것은 아님)\
> (ex.처음 요청 시 POST로 요청했더라도 리다이렉트시에는 GET으로 요청 메서드가 변경되고, 이에 따라 본문이 제거될 수 있음)\
> \
> **• 308 Permanent Redirect**\
> \- 301과 동일한 기능\
> \- 리다이렉트 시, <mark style="color:purple;">**요청 메서드와 본문을 유지한다.**</mark>\
>
>
> \
> **◆ 일시 Redirection**\
> \- 일시적인 URI 변경 (주문 완료 후 주문 내역 화면으로 이동 - PRG(POST-REDIRECT-GET)패턴)\
> \
> **• 302 Found**\
> \- 리다이렉트 시 요청 메서드가 <mark style="color:purple;">**GET으로 변하고, 본문이 제거될 수도 있다**</mark><mark style="color:purple;">.</mark> (가능성이 있음)\
> \
> **• 307 Temporary Redirect**\
> \- 리다이렉트 시 <mark style="color:purple;">**요청 메서드와 본문을 유지**</mark>한다. (요청 메서드를 변경하면 안됨)\
> \
> **• 303 See Other**\
> \- 리다이렉트 시 <mark style="color:purple;">**요청 메서드가 GET으로 변경**</mark>된다.\
> \
> <mark style="background-color:green;">**✓ PRG 패턴**</mark>\
> \- POST / REDIRECT / GET\
> \- POST로 요청을 보낸 후 웹 브라우저를 새로고침하게 되면 중복으로 요청을 발생할 수 있다.\
> \- POST로 요청을 보낸 후 결과 화면을 GET메서드로 리다이렉트하면, 새로고침을 하더라도 결과 화면에 대해 GET요청을 보내게 되어 POST에 대한 중복 요청이 발생하지 않는다.\
> \- 리다이렉트 된 이후에는 새로고침을 하더라도 GET으로 결과 화면만 조회한다.\
>
>
> ***
>
> **◆ 특수 Redirection**\
> \- 캐시 사용\
> \
> <mark style="color:blue;">**• 304 Not Modified**</mark>\
> \- 캐시를 사용하기 위한 목적으로 사용한다.\
> \- 클라이언트가 <mark style="background-color:orange;">요청한 리소스가 수정되지 않았음을 알려주는 역할</mark>을 한다.\
> \- 클라이언트가 <mark style="background-color:orange;">로컬 PC에 저장된 캐시를 재사용</mark>한다. (<mark style="background-color:blue;">**캐시로 리다이렉트**</mark>)\
> \- 조건부 GET, HEAD 요청시에 사용할 수 있다.

***

### **4XX - 클라이언트 에러**

> \- 클라이언트의 요청에 잘못된 문법과 같은 문제로 서버가 요청을 수행할 수 없음을 의미한다.\
> \- 클라이언트가 잘못된 요청을 보낸 것이기 때문에 똑같은 요청을 하더라도 에러가 발생한다.\
> \
> **• 401 Unauthorized**\
> \- 클라이언트가 해당 리소스에 접근하기 위해서는 인증이 필요함을 의미한다.\
> \- 응답에 **WWW-Authenticate** 헤더와 함께 인증 방법을 알려준다.\
> \- 비하인드 : 인증에 대한 에러 메시지인데 에러명은 \[인가]이다. 처음에 잘못 설정해서 그냥 쓴다고 한다.\
> \
> **• 403 Forbidden**\
> \- 요청을 이해는 했지만 승인을 거부함을 의미한다.\
> \- 인증은 됐으나, 접근 권한이 불충분한 경우에 사용된다.\
> \
> **• 404 Not Found**\
> \- 요청 리소스를 찾을 수 없음을 의미한다.\
> \- 클라이언트가 리소스에 대한 권한이 부족한 경우, 해당 리소스를 노출하지 않고 싶을 때 사용한다.

***

### **5XX - 서버 에러**

> \- 서버 문제로 인해 발생하는 에러이다.\
> \- 서버 문제가 해결되면 요청이 성공할 수 있다.\
> \- 일반적으로 대부분의 서버 에러는 **500** 에러를 사용한다.\
> \
> **• 503 Service Unavailable**\
> \- 서비스 이용 불가를 의미한다.\
> \- 서버의 일시적 과부하 또는 예정된 작업으로 인해 일시적으로 요청을 처리할 수 없는 경우 사용한다
