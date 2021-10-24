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

getBoardInfo() 메서드 실행 시, boardNo에 해당하는 정보가 없는 경우, NPE가 발생하게 된다. 이 경우, ExceptionHandler 메서드를 통해 예외가 발생했을 때 직접 처리 로직을 구현할 수 있다. Exception 타입을 지정하게 되면 해당 타입을 포함한 하위 타입까지 처리할 수 있다.

### 2. @ControllerAdvice, @RestControllerAdvice

### 3. @ResponseStatus
