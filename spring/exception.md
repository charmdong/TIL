# Exception

### 1. @ExceptionHandler

Controller에서 @RequestMapping 메서드를 실행하는 과정에서 예외가 발생했을 때, 해당 예외를 직접 처리하고자 할 때 @ExceptionHandler 를 사용한다.

```java
@Controller
public class SampleController {
	
    @RequestMapping("/board")
    public String getBoardInfo(Model model, @RequestParam("boardNo") int boardNo) {
    	Board board = BoardService.getBoardInfo(boardNo);
        
        // boardNo에 해당하는 데이터가 없는 경우, NullPointerException 발생
        model.setAttribute("boardInfo", board);
        
        return "board/detail";
    }
    
    @ExceptionHandler(NullPointerException.class)
    public String handleException() {
    	return "error/exception";
    }
    
    // 또는 전달인자로 처리할 예외 클래스를 받아 정의, 위의 메서드와 동일한 예외 클래스에 대한 처리
    @ExceptionHandler
    public String handleException(NullPointerException exception) {
    	// exception에 직접 접근 가능
        return "error/excpetion";
    }
}
```

getBoardInfo() 메서드 실행 시, boardNo에 해당하는 정보가 없는 경우, NPE가 발생하게 된다. 이 경우, **ExceptionHandler 메서드를 통해 **<mark style="color:blue;">**예외가 발생했을 때 직접 처리 로직을 구현**</mark>**할 수 있다.** <mark style="color:blue;">**Exception 타입을 지정**</mark>**하게 되면 해당 타입을 포함한 하위 타입까지 처리**할 수 있다.

기본적으로 **ExceptionHandler 메서드를 통해 예외를 처리하게 되면** <mark style="background-color:purple;">**응답 코드가 200**</mark>으로 날아간다. 따라서, **다른 응답 코드를 전송**하고 싶다면 <mark style="background-color:purple;">**HttpServletResponse를 이용해 전송하고자 하는 응답 코드를 지정**</mark>하면 된다.

```java
@ExceptionHandler(NullPointerException.class)
public String handleException(HttpServletResponse response) {
    // 원하는 응답 코드 설정
    response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR);
    return "error/exception";
}
```

#### ExceptionHandler 처리는 누가 하는가?

Spring은 **Controller에서 예외가 발생하면 **<mark style="color:blue;">**HandlerExceptionResolver에게 처리를 위임**</mark>한다. MVC 설정인 \<mvc:annotation-driven>이나 @EnableWebMvc 어노테이션을 사용할 경우, 내부적으로 <mark style="color:orange;">**ExceptionHandlerExceptionResolver**</mark>를 등록한다. 이는 <mark style="background-color:purple;">**@ExceptionHandler 어노테이션이 적용된 메서드를 이용해 예외를 처리하는 기능을 제공**</mark>한다.

#### 처리 과정

> 1. <mark style="color:blue;">**ExceptionHandlerExceptionResolver**</mark>가 **발생한 예외와 매핑되는 **<mark style="color:blue;">**ExceptionHandler 메서드를 통해 예외를 처리**</mark>한다.
> 2. DefaultHandlerExceptionResolver가 Spring이 발생시키는 예외에 대한 처리를 한다.
> 3. 예외 타입에 **@ResponseStatus 어노테이션이 적용되어 있는 경우, **<mark style="color:blue;">**ResponseStatusExceptionResolver **</mark>**해당 어노테이션 값을 이용해 응답 코드를 전송**한다.



### 2. @ControllerAdvice, @RestControllerAdvice

@ExceptionHandler를 이용하면 해당 컨트롤러에서 발생한 예외만 처리할 수 있다. 만약 모든 컨트롤러에서 공통으로 발생하는 예외를 처리하고자 한다면, @ControllerAdvice, @RestControllerAdvice를 이용하면 된다.

```java
@ControllerAdvice("com.donggun.springMaster.controller")
public class CommonExceptionHandler {
    
    @ExceptionHandler(RuntimeException.class)
    public String handleRuntimeException() {
        return "error/runtimeException";
    }
}
```

@ControllerAdvice 어노테이션을 이용하면 적용할 컨트롤러의 범위를 지정해 해당 컨트롤러들에 대해 공통으로 예외를 처리할 수 있게 해준다.&#x20;

> @ControllerAdvice의 @ExceptionHandler 메서드와 컨트롤러의 @ExceptionHandler 중에서는 후자가 높은 우선순위를 갖는다.

###

### 3. @ResponseStatus

원하는 응답 코드를 보다 쉽게 설정하기 위해 예외 클래스에 붙여 사용한다. 이 어노테이션을 통해 응답 코드를 설정하면 해당 예외가 발생했을 때 해당 예외 응답 코드가 반환된다.

```java
@ResponseStatus(Http.NOT_FOUND)
public class SampleException extends Exception {

    ...
}
```

