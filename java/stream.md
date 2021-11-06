# Stream

### **1. 반복자**

```java
// 자바 7 이전까지 컬렉션 요소 iterator를 활용한 순차적 처리
List<String> nameList = Arrays.asList("A", "B", "C");
Iterator<String> iter = list.iterator();

while(iterator.hasNext()) {
	String name = iterator.next();
    System.out.println(name);
}

// 자바 8 이후 Stream을 이용한 순차적 처리
List<String> nameList = Arrays.asList("A", "B", "C");
Stream<String> stream = list.stream();
stream.forEach(name -> System.out.println(name));
```

&#x20;

### **2. 특징**

iterator와 비슷한 역할을 하는 반복자이지만, 람다식으로 요소 처리 코드를 제공하는 점과 내부 반복자를 사용함으로써 병렬 처리가 쉽다는 점, 중간 및 최종 처리 작업을 수행할 수 있다는 점에서 여러 차이를 지닌다.

> **1. 람다식을 사용한 요소 처리**\
> Stream이 제공하는 요소 처리 메소드는 대부분 함수적 인터페이스 매개 타입을 가지므로 람다식 혹은 메소드 참조를 이용하여 요소 처리 내용을 매개값으로 전달할 수 있다.\
> \
> **2. 내부 반복자의 사용을 통해 병렬 처리가 쉽다.**\
> 외부 반복자란, 개발자가 코드로 직접 컬렉션의 요소를 반복해서 가져오는 코드 패턴을 말한다. index를 이요한 for문, iterator를 이용한 while문 등이 해당된다. \
> \
> 내부 반복자란, 컬렉션 내부에서 요소들을 반복시키고, 개발자는 요소마다 처리해야 하는 코드만 제공하는 코드 패턴을 말한다.\
> \
> 내부 반복자를 사용하게 되면, 외부 반복자를 사용할 때에 비해 개발자는 온전히 요소 처리 코드에만 집중할 수 있게 된다. 또한, 요소들의 반복 순서를 변경하거나, 병렬 작업을 할 수 있게 도와줘 효율적으로 요소 반복을 수행할 수 있다.\
>
>
> ```java
> public class ParallelSample {
>     public static void main(String[] args) {
>     	List<String> nameList = Arrays.asList("A", "B", "C");
>         
>         Stream<String> parallelStream = nameList.parallelStream();
>         parallelStream.forEach(ParallelSample::printThreadName);
>         
>         /*
> 		출력 결과
>             
> 		B : main
> 		C : ForkJoinPool.commonPool-worker-2
> 		A : ForkJoinPool.commonPool-worker-1
>         */
>     }
>     
>     public static void printThreadName(String str) {
>     	System.out.println(str + " : " + Thread.currentThread().getName());
>     }
> }​
> ```
>
> \
> \
> **3. 중간 처리와 최종 처리가 가능하다.**\
>
