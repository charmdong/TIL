# GET, POST

### **1. GET**

* 서버로부터 정보를 조회하기 위해 <mark style="color:blue;">**Idempotent**</mark>하게 설계된 Method이다.
* 서버에 동일한 요청을 여러 번 전송하더라도 동일한 응답이 돌아와야 한다.
* 주로 데이터를 <mark style="color:blue;">**조회**</mark>할 때 사용한다.
* 요청을 전송할 때, 필요한 데이터를 Body에 담지 않는다.
* **QueryString을 사용해 필요한 데이터를 전달하고, 이에 따라 **<mark style="color:red;">**길이의 제한**</mark>**이 존재**한다.

> https://aaa.com\*\*?**name=honggildong**&\*\*id=sample
>
> 물음표 이후의 문자열을 QueryString이라 부른다.

* GET은 불필요한 요청을 제거하기 위해 요청이 <mark style="background-color:orange;">**캐싱**</mark>될 수 있다. js, css, 이미지와 같은 정적 컨텐츠들은 데이터의 양이 크고 변경될 일이 많지 않아 동일한 요청을 반복할 필요가 없다. **정적 컨텐츠를 요청하게 되면 브라우저에서 요청을 캐싱해두고, 동일한 요청이 들어오면 서버로 요청하지 않고 캐싱된 데이터를 사용**한다.

### **2. POST**

* 자원을 생성(CREATE), 수정(UPDATE)하기 위해 <mark style="color:blue;">**Non-idempotent**</mark>하게 설계된 Method이다. (**캐싱 X**)
* 서버에 동일한 요청을 하더라도 응답이 항상 다를 수 있다.
* Http 메시지의 **Body에 데이터를 담아 요청을 전송**한다.&#x20;
* Http 메세지의 **Body는 **<mark style="color:green;">**길이의 제한 없이**</mark>** 데이터를 전송**할 수 있다.
* Body안에 데이터를 담아 전송하기 때문에 안전하다고 생각할 수 있지만, 개발자 도구와 같은 툴로 요청 내용을 확인할 수 있기 때문에 숨겨야 하는 데이터의 경우 반드시 <mark style="color:blue;">**암호화**</mark>해 전송해야 한다.
* POST로 요청을 보내는 경우, **Request Header**의 **Content-Type**에 요청 데이터 타입을 알려줘야 한다. 데이터 타입을 명시하지 않으면 서버는 내용이나 URL에 포함된 리소스의 확장자명 등으로 데이터 타입을 유추한다. 알 수 없는 경우에는 **application/octet-stream**으로 요청을 처리한다.

