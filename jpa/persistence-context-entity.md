# Persistence Context, Entity

### 1. Persistence Context

> <mark style="color:blue;">**Entity를 영구적으로 저장하는 공간 및 환경**</mark>이라고 생각하면 된다. EntityManager는 Entity를 저장하거나 조회하면 Persistence Context에 Entity를 보관하고 관리한다. <mark style="color:orange;">**Persistence Context는 EntityManager를 생성할 때 하나 만들어진다.**</mark> Persistence Context에 접근하고 관리하기 위해서는 EntityManager를 통해야 한다.



### 2. Entity

#### 비영속

* <mark style="color:blue;">**Entity 객체를 생성한 후 아직 저장하지 않은 상태**</mark>를 말한다.
* Persistence Context와 EntityManager와 전혀 관련이 없다.

```
Member member = new Member();
member.setId("member1");
member.setUsername("user1");
```



#### 영속

* EntityManager를 통해 <mark style="color:green;">**Persistence Context에 저장되어 관리되는 상태**</mark>를 말한다.

```
Member member = new Member();
member.setId("member1");
member.setUsername("user1");

// Entity 객체를 저장해 영속 상태로 만든다.
em.persist(member);
```



#### 준영속

* Persistence Context가 관리하던 <mark style="color:orange;">**영속 상태의 Entity를 Persistence Context가 관리하지 않게 되는 상태**</mark>를 말한다.
* detach()를 호출하면 준영속 상태가 된다.
* close(), clear()를 호출해 Persistence Context를 초기화하는 경우에도 관리되던 영속 상태의 Entity들이 준영속 상태가 된다.

```
Member member = new Member();
member.setId("member1");
member.setUsername("user1");

// Entity 객체를 저장해 영속 상태로 만든다.
em.persist(member);

// 영속 상태의 엔티티를 준영속 상태로 만든다.
em.detach(member);
```



#### 삭제

* Entity를 <mark style="color:red;">**Persistence Context와 DB에서 삭제**</mark>한다.

```
Member member = new Member();
member.setId("member1");
member.setUsername("user1");

// Entity 객체를 저장해 영속 상태로 만든다.
em.persist(member);

// 영속 상태의 엔티티를 준영속 상태로 만든다.
em.detach(member);

// 엔티티를 삭제한다.
em.remove(member);
```
