# JDBC

- 자바를 이용한 데이터베이스의 접속과 SQL 문장의 실행, 그리고 실행 결과로 얻어진 데이터의 핸들링을 제공하는 방법과 절차에 관한 규약
- 자바 프로그램 내에서 SQL문을 실행하기 위한 자바 API
- SQL과 프로그래밍 언어의 통합 접근 중 한 형태

<br>

### JDBC를 이용한 프로그래밍 방법

1. `import java.sql.*;`
2. 드라이버 로드
3. `Connection` 객체를 생성
4. `Statement` 객체를 생성 및 질의 수행
5. SQL문에 결과물이 있다면 `ResultSet` 객체를 생성
6. 모든 객체를 뒤에서부터 차례로 닫는다.

<br>

### JDBC 사용

1. ***import***

   `import java.sql.*;`

2. ***드라이버 로드***

   `Class.forName("com.mysql.jdbc.Driver");`

3. ***Connection 얻기***

   `String dburl = "jdbc:mysql://localhost/dbName";`

   `Connection com = DriverManager.getConnection(dburl,ID,PWD);`

4. ***Statement 생성***

   `Statement stmt = con.createStatement();`

5. ***질의 수행***

   `ResultSet rs = stmt.executeQuery("select no from user");`

6. ***ResultSet으로 결과 받기***

   `ResultSet rs = stmt.executeQuery("select no from user");`

   `while (rs.next())`

   ​	`System.out.println(rs.getInt("no"));`

7. ***Close***

   `re.close();`

   `stmt.close();`

   `con.close();`

<br>

<br>

<br>

___

참고 : https://www.boostcourse.org/web326/lecture/58939
