# Exception

**예외란?**

사용자의 잘못된 조작 또는 개발자의 잘못된 코딩으로 발생하는 프로그램 오류를 말한다.



**예외의 종류**

|                                                                                                                                                               |                                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| **일반 예외 (Exception)**                                                                                                                                         | **실행 예외 (RuntimeException)**                                                                                                           |
| - 자바 소스를 **컴파일하는 과정**에서 예외 처리 코드가 필요한지 검사하기 때문에 컴파일러 체크 예외라고도 한다. - 예외 처리 코드가 없다면, **컴파일 오류**가 발생한다. - Exception 클래스를 상속받지만 RuntimeException을 상속받지 않는 클래스들이다. | - 컴파일하는 과정에서 예외 처리 코드를 검사하지 않는 예외를 말한다. - RuntimeException을 상속받은 클래스들이다. - 자바 컴파일러가 체크를 하지 않기 때문에, 개발자의 경험에 의해서 **예외 처리 코드**를 삽입해야 한다. |
| # ClassNotFoundException # InterruptedException                                                                                                               | # NullPointerException # ArrayIndexOutOfBoundsException # NumberFormatException # ClassCastException                                   |

****

**예외 처리**

실행 예외의 경우 컴파일러가 체크해주지 않기 때문에 예외 처리 코드를 개발자의 경험을 바탕으로 작성해야 한다.

try-catch-finally 블록을 이용한다. 

```
try {
	// 예외가 발생할 수 있는 코드
} catch (예외클래스 e) {
	// 예외 발생시 실행될 코드
} finally {
	// 예외 발생 여부와 관계 없이 반드시 실행될 코드
}
```

****

**다중 catch**

try 블록 내부에서는 다양한 종류의 예외가 발생할 수 있다. 따라서 각각의 예외가 발생할 때마다 실행해줄 코드를 작성하기 위해서는 각각의 예외를 catch하도록 다중 catch 블록을 구현해주면 된다. 하지만, try 블록에서는 동시다발적으로 예외가 발생하는 것이 아니기 때문에 하나의 예외가 발생하고 그에 맞는 catch 블록이 실행된다.

```
try {
	// NullPointerException 혹은 NumberFormatException이 발생할 수 있는 코드
} catch (NullPointerException ne) {
	// NullPointerException 발생 시 실행될 코드
} catch (NumberFormatException ne) {
	// NumberFormatException 발생 시 실행될 코드
}
```

****

**catch 순서**

\- 다중 catch 블록을 작성할 때는 **상위 예외 클래스**가 **하위 예외 클래스**보다 아래쪽에 위치해야 한다. 

\- try 블록에서 예외가 발생했을 때, 예외를 처리해줄 catch 블록은 **위에서부터 차례대로 검색**된다.

\- 만약 상위 예외 클래스의 catch 블록이 위에 있다면, 하위 예외 클래스의 catch 블록은 실행되지 않는다.

****

**멀티 catch**

자바 7부터 catch 블록에 여러 개의 예외를 처리할 수 있도록 멀티 catch 기능을 추가했다. ' | ' 로 연결해준다.

```
try {

} catch (ArrayIndexOutOfBoundsException | NumberFormatException e) {
	
}
```

****

**자동 리소스 닫기**

자바 7에서 새로 추가된 **try-with-resources** 를 사용하면 예외 발생 여부와 상관없이 사용했던 리소스 객체의 close() 메소드를 호출해 안전하게 리소스를 close해준다. 리소스란, 데이터를 읽고 쓰는 객체라고 생각하면 된다.

```
FileInputStream fis = null;
try {
	fis = new FileInputStream("file.txt");
	...
} catch (IOException e) {
	...
} finally {
	if(fis != null) {
    	try {
        	fis.close();
        } catch (Exception e) { }
    }
}

// try-with-resources
// try 블록에서 예외가 발생하면 우선 close()로 리소스를 닫고 catch 블록을 실행한다.
try(
    FileInputStream fis = new FileInputStream("file.txt");
    FileOutputStream fos = new FileOutputStream("file2.txt")
) {
	...
} catch (IOException e) {
	...
}
```

여기서 사용되는 리소스는 **java.lang.AutoClosable 인터페이스를 구현**하고 있어야 한다.
