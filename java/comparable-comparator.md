# Comparable, Comparator

### **Comparable**

**TreeSet**과 **TreeMap**은 정렬을 위해 java.lang.Comparable을 구현한 객체를 요구한다. Integer, String 등은 모두 Comparable 인터페이스를 구현하고 있기 때문에 우리가 따로 구현해줘야 하는 부분이 없다. 따라서 사용자 정의 클래스도 Comparable 인터페이스의 compareTo() 메소드를 <mark style="background-color:yellow;">**Override**</mark>해주면 TreeSet, TreeMap에서 자동으로 정렬이 가능하게 된다.

```java
public class Sample implements Comaparable<Sample> {
    int year;
    int month;
    
    @Override
    public int compareTo(Sample sample) {
        // 년도가 같은 경우
        if(this.year == sample.year) {
            // 월 오름차순으로 정렬
            return (this.month - sample.month);
        }
        else {
            // 년도 오름차순으로 정렬
            return (this.year - sample.year);
        }
    }
}
```

주어진 객체의 비교할 값이 같으면 0, 작으면 음수, 크면 양수를 리턴하게되는데, 위 코드에서는 년도 오름차순을 기준으로 같은 년도에 대해서는 달 오름차순으로 정렬할 수 있다.



### **Comparator**

그렇다면, Comparable 인터페이스를 구현하지 않은 클래스 객체들에 대해서는 정렬이 불가능한 것인가? 그렇지 않다. 우리에게는 또 다른 인터페이스 Comparator가 존재하기 때문이다!

**Collections.sort()**와 **Arrays.sort()** 메소드의 오버로딩된 메소드들을 천천히 살펴보면 <mark style="color:blue;">**sort(T\[], Comparator\<? super T> c)**</mark>로 정의된 메소드들이 있을 것이다. 이 메소드들을 사용할 때, Comparator를 구현해 compare() 메소드를 오버라이드한 클래스를 전달 인자로 주면 된다! (혹은 익명 클래스로 작성해도 된다!)

```java
public class Sample {
    static class Student {
    	String name;
        int age;
        
        public Student(String name, int age) {
            this.name = name;
            this.age = age;
        }
    }
    
    public static void main(String[] args) {
        List<Student> studentList = new ArrayList<>();
        
        studentList.add(new Student("A", 10));
        studentList.add(new Student("B", 11));
        studentList.add(new Student("C", 9));
        
        Collections.sort(studentList, new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                // 나이 오름차순
                return o1.age - o2.age;
            }
        });
    }
}
```

자, 이렇게 오늘은 Comparable과 Comparator 인터페이스를 사용해 사용자 정의 클래스를 정렬하는 방법에 대해 알아보았다. 본인이 알고리즘을 공부하고 있다면 반드시 마주칠 수 있는 부분이니 잘 습득해놓자!
