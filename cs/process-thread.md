# Process, Thread

### Process

* 프로그램이 실행된 상태를 말한다.
* 프로그램을 실행하기 위해서는 필요한 메모리를 할당 받는다. (Code, Data, Heap, Stack 영역)
* <mark style="background-color:orange;">각 프로세스는 자원을 공유하지 않는다.</mark>
* Context Switching 비용이 크다.



### Thread

* <mark style="background-color:blue;">하나의 프로세스 내에서 나뉘어진 하나 이상의 실행 단위이다.</mark>
* <mark style="background-color:orange;">부모 프로세스의 자원을 공유</mark>한다. (Code, Data, Heap)
* 따라서, Context Switching이 일어날 때 캐시 적중률이 올라가고, 비용이 적게 든다. 



### Multi-Process

* 하나의 어플리케이션의 처리 방식 중 하나.
* 여러 사용자가 로그인을 요청하는 경우, 부모 프로세스가 fork를 통해 자식 프로세스를 생성해 일을 처리하도록 한다. 
* 이 경우, <mark style="background-color:orange;">자식 프로세스는 부모 프로세스와 별개의 메모리 영역</mark>을 가진다.
* Context Switching 비용이 크다.
* 동기화 작업이 필요하지 않다.
* 구글 크롬은 탭마다 별개의 프로세스이다. 그렇기 때문에 메모리를 많이 점유하게 되지만, 공유하는 자원이 없기 때문에 하나의 탭에서 문제가 발생하더라도 나머지 탭에는 영향을 주지 않는다.



### Multi-Thread

* 하나의 어플리케이션의 처리 방식 중 하나.
* 인텔리제이 사용 시, 테스트를 돌리면서 코드를 수정할 수 있는 이유가 바로 이것.
* <mark style="background-color:orange;">한 어플리케이션의 작업 단위가 나누어지는 것</mark>.
* 공유된 자원으로 메모리를 효율적으로 사용할 수 있다.
* Context Switching 비용이 적다.
* 공유 자원 관리가 필요하다.
* 인터넷 익스플로러에서 탭을 하나의 스레드로 보면 된다. 따라서 하나의 탭에서 문제가 발생하면 나머지 탭에도 영향을 주게 된다. (스레드는 자원을 공유하기 때문에)



### Context Switching

* 현재 진행하고 있는 Task(Process, Thread)의 상태를 저장하고 다음 진행할 Task의 상태 값을 읽어 적용하는 과정을 말한다.
* 여러 개의 Task가 동시에 실행되는 것처럼 보이게 하기 위해서는, <mark style="background-color:blue;">빠른 속도로 Task를 바꿔 가면 실행</mark>해야 한다.
* CPU가 Task를 바꿔 가며 실행하기 위해 필요한 기술이다.
* 과정
  1. Task의 대부분의 정보는 Register에 저장되고, <mark style="color:orange;">PCB</mark>(Process Control Block)에 의해서 관리된다.
  2. 현재 실행하고 있는 Task의 PCB 정보를 메모리에 적재한다.
  3. 다음 실행할 Task의 PCB 정보를 메모리에 적재하고 CPU가 이전에 진행했던 과정을 연속적으로 수행 가능.
