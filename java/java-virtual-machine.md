# Java Virtual Machine

### JVM이란?

> 자바 프로그램은 완전한 기계어가 아닌 바이트 코드이기 때문에 운영체제가 바로 실행할 수 없다. 그렇기 때문에 운영체제를 대신해 자바 프로그램을 실행해줄 녀석이 필요한데, 그게 바로 Java Virtual Machine이다.



### Java Application 실행 과정

> 1. 자바 프로그램을 실행하면 JVM이 해당 프로그램을 실행하는 데 필요한 메모리를 OS로부터 할당받는다.
> 2. javac가 자바 파일(.java) -> 클래스 파일(.class, 바이트 코드)로 변환한다.
> 3. 변환된 class 파일들은 Class Loader에 의해 JVM 메모리(Runtime Data Area)에 적재된다.
> 4. Rumtime Data Area에 적재된 class들은 Execution Engine에 의해서 기계어로 변환돼 명령어 단위로 실행된다.



### JVM 구성

![\[출처: https://2ssue.github.io/base/190509\_PJI/\]](https://2ssue.github.io/assets/images/java_program.png)

#### Class Loader

* 자바 컴파일러에 의해 바이트 코드로 변환된 class파일들을 JVM의 메모리인 RDA에 적재하는 역할을 한다.

#### Execution Engine

* Class Loader에 의해 메모리에 적재된 Class들을 기계어로 변경해 명령어 단위로 실행한다.
* 명령어를 실행하는 방식에는 인터프리터와 JIT(Just In Time) 방식이 있다.

#### Garbage Collector

* Heap 영역에 존재하는 객체들 중 참조되지 않는 객체를 찾아 제거하는 역할을 한다.

#### Runtime Data Area

* 자바 프로그램을 실행하기 위해 OS에서 할당받은 메모리 공간이다.



### Runtime Data Area

![\[출처: https://jithub.tistory.com/40\]](https://t1.daumcdn.net/cfile/tistory/992EE9465D08E9B903)

#### Method Area

* 클래스 멤버명, 데이터 타입, 접근 제어자 등의 <mark style="color:blue;">**필드 정보**</mark>
* 메소드명, 반환 타입, 파라미터, 접근 제어자 등의 <mark style="color:blue;">**메소드 정보**</mark>
* Interface, Class Type 정보
* <mark style="color:blue;">**Static 변수, Constant Pool**</mark>
* final class

#### Heap Area

* new 연산자를 통해 <mark style="color:purple;">**새로 생성되는 객체**</mark> (Method Area에 적재된 객체만 가능)
* 배열

#### Stack Area

* <mark style="color:blue;">**지역 변수, 파라미터, 리턴 값**</mark> 등이 생성된다.
* 메소드를 호출할 때마다 스택에 메소드와 관련된 1번 정보들이 저장된다.

#### PC Register

* Thread마다 하나씩 존재하는 레지스터로, 현재 스레드가 실행해야 하는 명령어와 주소를 저장한다.
