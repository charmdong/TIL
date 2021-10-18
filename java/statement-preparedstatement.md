# Statement, PreparedStatement

### 실행 과정

> 1. SQL 문장 분석
>    * 문법 검사
>    * 의미 검사
>    * 권한 검사
> 2. 컴파일
> 3. 실행

Statement를 사용하는 경우, SQL을 실행할 때마다 1 \~ 3단계를 모두 거치게 된다. 반면, PreparedStatement를 사용하는 경우에는 처음 실행하는 경우에만 3단계를 거치고 캐시에 올려둔다. 이후에는 캐시에 올라가 있는 것을 재사용한다.



### Statement

```
Connection connection = DBConnection.getConnection();

String query = "SELECT name FROM member WHERE id = " + param;
Statement stmt = connection.createStatement();

ResultSet result = stmt.executeQuery(query);
```

* 실행될 SQL을 한 눈에 파악할 수 있다.
* SQL을 실행할 때마다 위에서 언급한 3단계의 과정을 모두 거치기 때문에 성능상 이슈가 존재한다.
* 파라미터 바인딩 시, SQL Injection 공격에 취약하다.
* 위 예시에서 param의 값으로 id' or '1'='1 가 온다면 member 테이블의 모든 사용자의 데이터를 조회할 수 있다.



### PreparedStatement

```
Connection connection = DBConnection.getConnection();

String query = "SELECT name FROM member WHERE id = ?"

// 1. PreparedStatement 생성
PreparedStatement pstmt = connection.preparedStatement(query);

// 2. 파라미터 바인딩
pstmt.setString(1, userId);

// 3. 쿼리 실행
ResultSet result = pstmt.executeQuery();
```

* 한 번 실행하면 컴파일되어 캐시에 올라가기 때문에 재사용이 가능하다.
* placeHolder를 이용해 SQL 문장에 인자가 위치할 곳을 명시한다.
* 파라미터 부분을 set메서드로 설정하기 때문에, 외부의 입력이 query문의 구조를 변경하는 것을 방지할 수 있다.
