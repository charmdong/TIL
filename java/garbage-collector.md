# Garbage Collector

### Garbage Collector

> 1. Heap 메모리 영역에서 활동하므로, Heap 영역에 생성되는 배열과 객체들 중 자주 사용되지 않는 객체를 제거하는 역할을 한다.
> 2. 메모리 공간은 한정적이기 때문에 오랜 기간동안 사용되지 않는 객체들은 메모리 공간을 차지하기만 할뿐, 프로그램을 실행하는 데 역할을 하지 못한다. 
> 3. 프로그램 내에서 해당 객체를 호출하거나 참조하지 않는다면, 제거 대상이 된다.



### 용어 정리

![\[출처: https://bscnote.tistory.com/96\]](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2\&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmxWdJ%2FbtqxpApS248%2FUurzeevh040qhMrtk238g0%2Fimg.jpg)

#### 0. Stop the world

* 각 GC가 실행될 때, GC가 실행되는 스레드를 제외한 나머지 스레드들은 실행을 중단하게 되는 현상을 말한다.

#### 1. Minor GC

* Eden: 객체가 새로 생성되면 위치하는 공간.
* 이 공간이 가득 차게 되면 발생하는 GC를 말한다.
* 이 과정을 거치게 되면 객체들이 Survivor 영역으로 이동하게 된다.
* Minor GC가 발생하면 Survivor0 -> Survivor1, Survivor1 -> Survivor0으로 살아남은 객체들이 이동한다.

#### 2. Promotion

* Minor GC를 통해서 살아남은 객체들은 age라는 살아남은 횟수를 나타내는 정보를 지니는데, 이 age가 특정 값에 도달하면 해당 객체가 Old 영역으로 이동하게 되는 현상을 말한다.
* Survivor 영역보다 큰 객체는 바로 Old 영역으로 이동하기도 한다.

#### 3. Major GC

* Old 영역이 가득 차게 되면 실행되는 GC이다.

#### 4. Mark & Sweep & Compaction

* Mark: 사용되지 않는 객체를 식별하는 작업.
* Sweep: 사용되지 않는 객체를 제거하는 작업.
* Compaction: Sweep을 통해 파편화된 메모리 영역을 앞에서부터 채워나가는 작업.

![\[출처: https://mirinae312.github.io/develop/2018/06/04/jvm_gc.html\]](https://mirinae312.github.io/img/jvm_gc/MarkSweepCompaction.png)



### GC 종류

#### 1. Serial GC (-XX:+UserSerialGC)

> * 가장 단순한 방식으로, Single Thread로 동작한다.
> * Single Thread로 동작하기 때문에 Stop the world 시간이 가장 길다.
> * MSC 알고리즘을 사용한다.

#### 2. Parallel GC (-XX:+UserParallelGC)

> * Young 영역에 대해 **멀티 스레드**로 동작한다.
> * Serial GC에 비해 Stop the world 시간이 적게 걸린다.
> * Java 8의 기본 GC이다.

#### 3. Parallel Old GC (-XX:+UserParallelOldGC, -XX:+ParallelGCThreads=n)

> * Young, Old 영역에서 **멀티 스레드**로 동작한다.
> * 멀티 스레드의 개수를 지정할 수 있다.
> * Mark - Summary - Compact 알고리즘을 사용한다.
> * **Summary**: <mark style="background-color:orange;">이미 GC가 실행된 영역에서 살아남은 객체를 식별</mark>하는 작업.

#### 4. CMS GC (Concurrent Mark Sweep GC)

> * STW 시간을 최소화하기 위한 GC이다.
> * GC 대상을 자세하게 파악한 후, STW 시간을 줄이고자 한다.
> * GC 대상을 파악하는 과정이 복잡하다.
> * Initial Mark -> Concurrent Mark -> Remark -> Concurrent Sweep 과정을 거친다.
> * Initial Mark
>   * GC Root가 참조하는 객체를 식별한다. (STW 발생)
> * Concurrent Mark
>   * 참조하는 객체를 따라가며 Mark (STW 발생 X)
> * Remark
>   * CM 과정에서 변경 사항이 없는 지 확인. (STW 발생)
> * Concurrent Sweep
>   * 접근할 수 없는 객체를 제거 (STW 발생 X)
> * Compaction 작업은 필요한 경우에만 실행한다. 연속적인 메모리 할당이 어여루 정도로 메모리 단편화가 심한 경우에만 

#### 5. G1 GC (Garbage First GC, -XX:+UseG1GC)

![\[출처: https://mirinae312.github.io/develop/2018/06/04/jvm_gc.html\]](https://mirinae312.github.io/img/jvm_gc/G1Heap.png)

> * 기존 GC들과 다르게 Heap 메모리 영역을 Region이라는 범위로 나누어 관리한다.
> * 짧은 GC 시간을 보장하는 게 목적이다.
> * Region의 상태에 따라 역할(Eden, Survivor, Old)이 동적으로 부여된다.
> * **Humongous**: Region 크기의 50%를 초과하는 객체를 저장하기 위한 공간이다.
> * **Available/Unused**: 아직 사용되지 않은 Region이다.
