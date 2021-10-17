# Transaction

### 1. Transaction이란?

* 데이터베이스의 상태를 변화시키기 위해 수행되는 작업의 단위를 말한다.
* SELECT, INSERT, UPDATE, DELETE 로 이루어진 SQL을 통해 DB에 접근하는 것을 말한다.



### 2. 특징

* **원자성 (Atomicity)**
  * All or Nothing
  * 트랜잭션이 DB에 모두 반영되거나, 모두 반영이 되지 않아 한다는 것을 말한다.
* **일관성 (Consistency)**
  * 트랜잭션의 작업 처리 결과가 항상 일관성이 있어야 함을 말한다.
  * 트랜잭션이 진행되는 동안 DB가 변경되더라도 시작할 때 참조한 DB 상태를 기준으로 진행되어야 한다.
* **독립성 (Isolation)**
  * 둘 이상의 트랜잭션이 동시에 실행되고 있을 경우 어떤 하나의 <mark style="color:blue;">**다른 트랜잭션 연산에 관여해서는 안 된다.**</mark>
  * 하나의 특정 트랜잭션이 완료될 때까지 다른 트랜잭션이 특정 트랜잭션의 결과를 참조할 수 없다.
* **지속성 (Durability)**
  * 트랜잭션이 성공적으로 진행됐을 때, 그 결과가 <mark style="color:blue;">**영구적으로 반영**</mark>되어야 한다.



### 3. Commit, Rollback

* **Commit**
  * 하나의 트랜잭션이 성공적으로 진행되었고, 데이터베이스가 일관성 있는 상태에 있을 때, 하나의 트랜잭션이 끝났다는 것을 알려주기 위해 사용하는 연산.
* **Rollback**
  * 하나의 트랜잭션 처리가 비정상적으로 종료되어 트랜잭션의 원자성이 깨진 경우, 트랜잭션을 처음부터 다시 시작하거나(redo) 부분적으로 연산된 결과를 취소(undo)시키는 것을 말한다.



### 4. Transaction 격리 수준

* 종류
  1. READ UNCOMMITTED
  2. READ COMMITTED
  3. REPEATABLE READ
  4. SERIALIZABLE
* **READ UNCOMMITTED**
  * 아직 <mark style="background-color:blue;">**커밋되지 않은 데이터를 다른 트랜잭션이 읽을 수 있다**</mark>.
  * 트랜잭션 1에서 작업이 진행 중이던 데이터를 트랜잭션 2에서 읽어온 뒤, 트랜잭션 1이 롤백 되는 경우, 트랜잭션 2는 존재하지 않는 데이터를 읽어온 것이 된다.
* **READ COMMITTED**
  * READ UNCOMMITTED의 문제를 해결할 수 있는 단계의 격리 수준으로, <mark style="background-color:blue;">**커밋되지 않은 데이터를 조회**</mark>할 수 없다. 
  * 트랜잭션 1에서 커밋된 데이터를 트랜잭션 2에서 조회한 데이터를 트랜잭션 3에서 수정할 수 있어 트랜잭션 2에서 <mark style="background-color:red;">똑같은 데이터를 다시 조회했을 때 값이 다르게 되는 문제</mark>가 발생할 수 있다.
* **REPEATABLE READ**
  * <mark style="background-color:blue;">**하나의 트랜잭션이 읽은 row를 다른 트랜잭션이 수정할 수 없게 한다.**</mark>
  * 다른 트랜잭션이 새로운 row를 추가하는 것에 대한 제한은 없기 때문에, 특정 <mark style="background-color:red;">트랜잭션이 다시 조회했을 때 새로운 row가 발견될 수 있다는 문제</mark>가 존재
* **SERIALIZABLE**
  * 동시에 같은 테이블의 정보를 접근할 수 없게 하는 격리 수준이다.
  * 트랜잭션을 순차적으로 진행하는 것과 다를 바가 없어 성능이 매우 떨어지게 된다.
