# Persistence Context

### 1. 영속성 컨텍스트의 특징

1. **식별자 값**
   * 영속성 컨텍스트는 **엔티티를 식별자 값(**<mark style="color:blue;">**@Id로 테이블의 기본 키와 매핑한 값**</mark>**)으로 구분**한다. 그러므로 **영속 상태에 있는 엔티티는 반드시 식별자 값을 가져야 한다.**
2. **데이터베이스 저장**
   * JPA는 보통 **Transaction을 commit하는 순간 영속성 컨텍스트에 새로 저장된 엔티티를 데이터베이스에 반영**하며, 이를 <mark style="background-color:orange;">**Flush**</mark>라고 한다.
3. **장점**
   * 1차 캐시
   * 동일성 보장
   * 쓰기 지연
   * 변경 감지 (dirty checking)
   * 지연 로딩 (lazy loading)



### 2. Entity 조회

영속성 컨텍스트는 내부에 <mark style="background-color:orange;">**1차**</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">**캐시**</mark>를 가지고 있어 **영속 상태의 엔티티가 모두 이곳에 저장**된다. 영속성 컨텍스트 안에 <mark style="background-color:orange;">**\[Key: @Id로 매핑된 식별자, Value: 엔티티 인스턴스]**</mark>** 구조로 된 Map**이 존재한다.

1차 캐시의 Key는 식별자 값이다. 이 <mark style="background-color:blue;">**식별자 값은 데이터베이스 기본 키와 매핑**</mark>된다. 따라서 영속성 컨텍스트에 데이터를 저장하고 조회하는 모든 <mark style="background-color:red;">**기준은 DB의 기본 키 값**</mark>이다.

```java
Member member = em.find(Member.class, "member1");
```

find() 메소드의 첫 번째 전달인자는 엔티티 클래스 타입이고, 두 번째 전달인자는 조회하고자 하는 엔티티의 식별자 값이다.

#### find() 호출 시 동작 과정

> 1. 1차 캐시에서 식별자 값을 기반으로 엔티티를 탐색한다.
> 2. 1차 캐시에 찾는 엔티티가 존재하지 않으면 데이터베이스에서 조회한다.
> 3. 데이터베이스에서 조회해 **엔티티를 생성**하고, 이렇게 **생성된 엔티티를 1차 캐시에 저장한 뒤 영속 상태의 엔티티를 반환**한다.

#### 영속 엔티티의 동일성 보장

```java
Member memberA = em.find(Member.class, "member1");
Member memberB = em.find(Member.class, "member1");

// 동일성 비교
System.out.println(memberA == memberB);
```

위 코드를 실행하게 되면 True가 출력된다. find() 메소드를 반복해서 호출하더라도 **영속성 컨텍스트는 1차 캐시에 있는 동일한 인스턴스를 반환**하기 때문이다.
