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



### 3. Entity 등록

```java
EntityManager em = emf.createEntityManager();
EntityTransaction tx = em.getTransaction();

// 데이터 변경 시에는 엔티티 매니저가 트랜잭션을 시작한다.
tx.begin();

em.persist(memberA);
em.persist(memberB);
// 여기까지는 INSERT SQL을 DB에 보내지 않는다.

// 커밋하는 순간 INSERT SQL을 전송한다.
tx.commit();
```

엔티티 매니저는 **트랜잭션을 커밋하기 전까지 DB에 엔티티를 저장하지 않고 내부 쿼리 저장소에 INSERT SQL을 모아둔다.** 이후 트랜잭션 커밋이 이루어질 때 모아두었던 쿼리를 DB에 전송한다. 이를 <mark style="background-color:blue;">**Transactional write-behind**</mark>, <mark style="background-color:blue;">**트랜잭션을 지원하는 **</mark><mark style="background-color:purple;">**쓰기 지연**</mark>이라고 한다.

#### 쓰기 지연 과정

> 1. 엔티티를 영속화 한다. (em.persist)
> 2. 영속성 컨텍스트는 1차 캐시에 엔티티를 저장하면서 동시에 엔티티 정보로 INSERT SQL을 생성한다.
> 3. 생성된 INSERT SQL을 영속성 컨텍스트 내부의 쓰기 지연 SQL 저장소에 보관한다.
> 4. 트랜잭션을 커밋하면 엔티티 매니저가 영속성 컨텍스트를 flush한다. 즉, 쓰기 지연 SQL 저장소에 모아둔 쿼리를 DB로 전송한다.
> 5. 영속성 컨텍스트의 변경 내용을 DB에 동기화한 후, 실제 DB Transaction을 커밋한다.



### 4. Entity 수정

#### 변경 감지

```java
EntityManager em = emf.createEntityManager();
EntityTransaction tx = em.getTransaction();

tx.begin();

// 영속 상태 엔티티 조회
Member memberA = em.find(Member.class, "memberA");

// 엔티티 데이터 수정
memberA.setName("hello");
memberA.setAge(25);

tx.commit();
```

<mark style="background-color:orange;">**JPA로 엔티티의 데이터를 수정할 때는 단순하게 엔티티를 조회한 뒤 원하는 데이터를 수정하기만 하면 된다**</mark>. <mark style="background-color:orange;">**엔티티의 변경사항을 DB에서 자동으로 반영하는 변경 감지 기능이 작동하기 때문**</mark>이다.

**JPA는 영속성 컨텍스트에 엔티티를 보관**할 때, <mark style="background-color:red;">**최초의 상태를 복사해 저장하는 스냅샷을 찍는다.**</mark>&#x20;

> 1. 트랜잭션을 커밋하면 **엔티티 매니저 내부에서 먼저 flush()가 호출**된다.
> 2. **엔티티와 **<mark style="color:blue;">**스냅샷**</mark>**을 비교해 **<mark style="color:blue;">**변경된 엔티티**</mark>**를 탐색**한다.
> 3. 변경된 엔티티가 존재하면 **UPDATE 쿼리를 생성해 쓰기 지연 SQL 저장소에 보낸다.**
> 4. 쓰기 지연 SQL 저장소의 **SQL을 DB로 전송**한다.
> 5. DB 트랜잭션을 커밋한다.

위 과정에서 보듯이, 스냅샷과 현재 엔티티를 비교하기 때문에 <mark style="background-color:orange;">**변경 감지는 영속성 컨텍스트가 관리하는 영속 상태의 엔티티에만 적용**</mark>이 된다. 따라서, <mark style="background-color:red;">**변경 감지를 이용해 엔티티를 수정하기 전에 조회를 해 영속성 컨텍스트가 관리하도록 하는 것**</mark>이다.

하지만 JPA는 기본적으로 변경 사항이 존재한다면 엔티티의 모든 필드를 업데이트 하는데, 이는 데이터 전송량이 증가하는 단점이 존재하지만 여러 장점이 존재해 모든 필드를 업데이트 한다.

> 1. 모든 필드를 사용하면 수정 쿼리가 항상 동일하다. 이로 인해 애플리케이션 로딩 시점에 수정 쿼리를 미리 생성해두고 <mark style="color:blue;">**재사용**</mark>할 수 있다.
> 2. DB에 동일한 쿼리를 전송하면 DB는 이전에 파싱된 쿼리를 <mark style="color:blue;">**재사용**</mark>할 수 있다.



#### 수정된 데이터만 업데이트하기

필드가 너무 많거나 저장되는 내용의 크기가 크다면 수정된 데이터만 업데이트 하도록 동적으로 UPDATE SQL을 생성해 사용할 수 있다. 이때 엔티티 클래스에 <mark style="background-color:blue;">**@org.hibernate.annotations.DynamicUpdate**</mark> 어노테이션을 추가해주면 수정된 데이터만 동적으로 UPDATE 쿼리를 생성한다.



### 5. Entity 삭제

엔티티를 삭제하기 위해서는 **Entity 수정 시와 동일하게 먼저 조회**를 해야한다. em.remove()를 호출한다고 해서 바로 엔티티가 삭제되는 것은 아니다. 엔티티 등록과 비슷하게 **DELETE SQL을 쓰기 지연 저장소에 등록한 뒤 트랜잭션 커밋을 통해 flush가 호출되면 DB에 SQL이 전송**된다. 단, <mark style="background-color:blue;">**remove()를 호출하는 순간에 삭제하고자 하는 엔티티는 영속성 컨텍스트로부터 제거**</mark>된다. 다시 말해, <mark style="background-color:blue;">**영속성 컨텍스트에서는 바로 사라지지만 DB에서는 그렇지 않다.**</mark>
