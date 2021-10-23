# POST, PUT

### **1. POST**

> 1. 리소스 **생성**
> 2. URI가 <mark style="color:blue;">**컬렉션**</mark>이어야 한다. (ex. POST /users)
> 3. 리소스 생성 성공 시, **201(CREATED)** HTTP STATUS와 함께 <mark style="color:blue;">**리소스 생성 위치 정보가 담긴 Location**</mark>** 응답 헤더를 포함**한다.&#x20;

#### 사용해야 하는 경우

1. 리소스 생성
2. 요청 데이터 처리
3. 다른 메서드로 처리하기 애매한 경우 (서버에서 GET, POST만 제공하는 경우)



### **2. PUT**

> 1. 리소스 **변경**, 없는 경우에는 **생성**
> 2. URI에 변경할 <mark style="color:blue;">**리소스의 식별자가 포함**</mark>되어야 한다. (ex. PUT /users/100)

#### PATCH와의 차이점

1. <mark style="color:blue;">**PUT**</mark>은 **파일 덮어쓰기**와 같다. 따라서, 수정할 부분에 대해서만 명시할 경우, **명시되지 않은 부분은 **<mark style="color:red;">**null**</mark>** 혹은 **<mark style="color:red;">**default 값**</mark>**으로 처리**된다.
2. <mark style="color:orange;">**PATCH**</mark>는 부분적으로 수정하는 경우 사용된다. PUT과는 다르게 <mark style="color:green;">**수정할 부분에 대해서 명시하면 해당 부분만 수정**</mark> 된다.
