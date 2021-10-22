# Flush

### 1. Flush

플러시란, <mark style="background-color:yellow;">**영속성 컨텍스트의 변경 내용을 데이터베이스에 반영하는 것**</mark>을 말한다. (영속성 컨텍스트에 보관된 엔티티를 지우는 것은 아니다.)



#### 플러시 실행 과정

> 1. <mark style="background-color:orange;">**변경 감지**</mark>가 동작해 <mark style="background-color:orange;">**영속성 컨텍스트에 있는 모든 Entity 스냅샷과 비교해 수정된 Entity를 찾는다**</mark>. 수정된 Entity는 UPDATE SQL를 만들어 쓰기 지연 SQL 저장소에 보관한다.
> 2. 쓰기 지연 SQL 저장소의 쿼리를 DB에 전송한다.

#### 플러시 호출 방법

> * **em.flush() 직접 호출**
>
> 테스트나 다른 프레임워크와 JPA를 함께 사용할 때를 제외하고 거의 사용하지 않음.
>
>
>
> * **트랜잭션 커밋 시 자동 호출**
>
> DB에 변경 내용을 SQL로 전달하지 않고 트랜잭션만 커밋하면 어떤 데이터도 DB에 반영되지 않는다. 그렇기 때문에 <mark style="background-color:yellow;">**트랜잭션을 커밋하기 전에 반드시 flush를 호출해 영속성 컨텍스트의 변경 내용을 DB에 반영해야 한다**</mark>. 따라서 JPA는 트랜잭션 커밋 시 flush를 자동으로 호출한다.
>
>
>
> * **JPQL 쿼리 실행 시 자동 호출**
>
> <mark style="background-color:yellow;">**Persistence Context에서 관리되나 아직 DB에 반영되지 않은 엔티티들이 존재할 때, JPQL을 실행해 해당 엔티티를 조회하고자 하면 조회되지 않는다**</mark>. 따라서, 이런 문제를 예방하기 위해 JPQL을 실행할 때 flush를 자동으로 호출한다.

#### 플러시 옵션

> * FlushModeType.AUTO - commit, query 실행 시 flush (default)
> * FlushModeType.COMMIT - commit 시에만 flush (성능 최적화를 위해 사용)



### 2. 준영속

<mark style="background-color:yellow;">**영속 상태의 엔티티가 영속성 컨텍스트에서 분리된(detached) 상태**</mark>를 말한다. 준영속 상태의 엔티티는 영속성 컨텍스트가 제공하는 기능을 사용할 수 없다.



#### 준영속 상태로 만드는 방법

> * **em.detach(entity)** - 특정 엔티티를 준영속 상태로 만든다.
>
> 호출되면 <mark style="color:blue;">**1차 캐시에서 제거**</mark>**된 후 **<mark style="color:red;">**쓰기 지연 SQL 저장소에 있는 해당 엔티티를 관리하기 위한 모든 정보가 제거**</mark>된다.
>
>
>
> * **em.clear()** - 영속성 컨텍스트를 초기화한다.
>
> 영속성 컨텍스트를 초기화해 해당 <mark style="color:blue;">**영속성 컨텍스트에서 관리하는 모든 엔티티를 준영속 상태로 만든다.**</mark> 영속성 컨텍스트를 제거하고 새로 만드는 것과 동일하게 볼 수 있다.
>
>
>
> * **em.close()** - 영속성 컨텍스트를 종료한다.
>
> <mark style="color:blue;">**영속성 컨텍스트를 종료**</mark>함으로써 해다 영속성 컨텍스트가 관리하던 영속 상태 엔티티를 모두 준영속 상태로 만든다.

#### 준영속 특징

> 1. 영속성 컨텍스트가 제공하는 기능을 사용할 수 없다.
> 2. 비영속 상태와는 다르게 식별자 값을 지니고 있다. <mark style="background-color:orange;">**한 번 영속 상태가 됐었으므로 식별자 값을 가지고 있다.**</mark>
> 3. <mark style="background-color:orange;">**1차 캐시에서 제거되어 지연 로딩을 할 수 없게 된다.**</mark>

#### 병합 (Merge)

준영속 상태의 엔티티를 다시 영속 상태로 변경하기 위해 사용된다. merge()는 **준영속 상태의 엔티티를 전달 받아 그 정보로 **<mark style="background-color:orange;">**새로운 영속 상태의 엔티티를 반환**</mark>한다.

> 1. merge() 실행.
> 2. 전달받은 준영속 상태의 엔티티의 식별자 값으로 1차 캐시에 엔티티를 조회, 존재하지 않는다면 DB에서 엔티티를 조회해 1차 캐시에 저장.
> 3. 조회한 영속 엔티티에 <mark style="background-color:yellow;">**전달 받은 엔티티의 값을 채워 넣음.**</mark>
> 4. 위 과정을 통해 <mark style="background-color:yellow;">**새롭게 생성된 엔티티를 반환**</mark>한다.
>
>
>
> 📌**전달 인자로 사용된 **<mark style="color:red;">**준영속 상태의 엔티티는 더이상 사용할 수 없**</mark>**게 된다.** 따라서, <mark style="background-color:red;">**준영속 상태의 엔티티를 참조하던 변수를 새롭게 반환된 영속 상태의 엔티티를 참조하도록 변경해주는 것이 안전**</mark>하다.
>
>
>
> 📌merge는 <mark style="background-color:yellow;">**비영속 상태의 엔티티도 영속 상태로 만든다.**</mark> **DB에서 조회한 후, 존재하지 않으면 새로 엔티티를 생성해서 병합**한다. 즉, **Save or Update 기능을 수행**한다.

