# DDL(Data definition language)

- 데이터 정의어(DDL)은 테이블과 같은 데이터의 구조를 정의하는데 사용한다.

<br>

## *CREATE*

- 테이블을 생성하는 구문

```mysql
CREATE TABLE 테이블명(
필드명1 타입 [NULL|NOT NULL][DEFAULT][AUTO_INCREMENT],
필드명2 타입 [NULL|NOT NULL][DEFAULT][AUTO_INCREMENT],
필드명3 타입 [NULL|NOT NULL][DEFAULT][AUTO_INCREMENT],
......
PRIMARY KEY(필드명)
);
```

- `NULL` : 속성값의 빈 값
- `NOT NULL` : 빈 값을 허용하지 않는다.
- `DEFAULT` : 기본값을 지정해준다.
- `AUTO_INCREMENT` : 입력하지 않고 자동으로 1씩 증가한다.

```MYSQL
CREATE TABLE EMPLOYEE2(
empno INTEGER NOT NULL PRIMARY KEY,
name VARCHAR(10),
job VARCHAR(9),
boss INTEGER,
hiredate VARCHAR(12),
salary DECIMAL(7, 2),
comm DECIMAL(7, 2),
deptno INTEGER
);

DESC EMPLOYEE2;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| empno    | int(11)      | NO   | PRI | NULL    |       |
| name     | varchar(10)  | YES  |     | NULL    |       |
| job      | varchar(9)   | YES  |     | NULL    |       |
| boss     | int(11)      | YES  |     | NULL    |       |
| hiredate | varchar(12)  | YES  |     | NULL    |       |
| salary   | decimal(7,2) | YES  |     | NULL    |       |
| comm     | decimal(7,2) | YES  |     | NULL    |       |
| deptno   | int(11)      | YES  |     | NULL    |       |
+----------+--------------+------+-----+---------+-------+
```

<br>

## *ALTER*

- 테이블을 수정하는 구문
  - `ADD` : 필드 추가
  - `DROP` : 필드 삭제
  - `CHANGE` : 컬럼을 새롭게 재정의
  - `RENAME` : 테이블의 이름 변경

```mysql
# ADD
ALTER TABLE 테이블명
ADD 필드명 타입 [NULL|NOT NULL][DEFAULT][AUTO_INCREMENT];

# DROP
ALTER TALBE 테이블명
DROP 필드명;

# CHAGNE
ALTER TABLE 테이블명
CHANGE 필드명 새필드명 타입[NULL|NOT NULL][DEFAULT][AUTO_INCREMENT];

# RENAME
ALTER TABLE 테이블명 RENAME 변경이름
```

```MYSQL
# EMPLOYEE2 테이블에 VARCHAR(12) 타입의 birthdate 필드 추가
ALTER TABLE EMPLOYEE2
ADD birthdate VARCHAR(12);
+-----------+--------------+------+-----+---------+-------+
| Field     | Type         | Null | Key | Default | Extra |
+-----------+--------------+------+-----+---------+-------+
| empno     | int(11)      | NO   | PRI | NULL    |       |
| name      | varchar(10)  | YES  |     | NULL    |       |
| job       | varchar(9)   | YES  |     | NULL    |       |
| boss      | int(11)      | YES  |     | NULL    |       |
| hiredate  | varchar(12)  | YES  |     | NULL    |       |
| salary    | decimal(7,2) | YES  |     | NULL    |       |
| comm      | decimal(7,2) | YES  |     | NULL    |       |
| deptno    | int(11)      | YES  |     | NULL    |       |
| birthdate | varchar(12)  | YES  |     | NULL    |       |
+-----------+--------------+------+-----+---------+-------+

# EMPLOYEE2 테이블에서 birthdate 필드 제거
ALTER TABLE EMPLOYEE2
DROP birthdate;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| empno    | int(11)      | NO   | PRI | NULL    |       |
| name     | varchar(10)  | YES  |     | NULL    |       |
| job      | varchar(9)   | YES  |     | NULL    |       |
| boss     | int(11)      | YES  |     | NULL    |       |
| hiredate | varchar(12)  | YES  |     | NULL    |       |
| salary   | decimal(7,2) | YES  |     | NULL    |       |
| comm     | decimal(7,2) | YES  |     | NULL    |       |
| deptno   | int(11)      | YES  |     | NULL    |       |
+----------+--------------+------+-----+---------+-------+

# EMPLOYEE2 테이블의 `deptno` 컬럼을 `dept_no`로 변경, NULL 허용을 NOT NULL로 변경
ALTER TABLE EMPLOYEE2
CHANGE deptno dept_no int(11) NOT NULL;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| empno    | int(11)      | NO   | PRI | NULL    |       |
| name     | varchar(10)  | YES  |     | NULL    |       |
| job      | varchar(9)   | YES  |     | NULL    |       |
| boss     | int(11)      | YES  |     | NULL    |       |
| hiredate | varchar(12)  | YES  |     | NULL    |       |
| salary   | decimal(7,2) | YES  |     | NULL    |       |
| comm     | decimal(7,2) | YES  |     | NULL    |       |
| dept_no  | int(11)      | NO   |     | NULL    |       |
+----------+--------------+------+-----+---------+-------+

# EMPLOYEE2 테이블 이름을 NEW_EMPLOYEE로 변경
ALTER TABLE EMPLOYEE2 RENAME NEW_EMPLOYEE;
+-----------------------+
| Tables_in_mydb        |
+-----------------------+
| bonus                 |
| department            |
| employee              |
| new_employee          |
| project               |
| project_participation |
| role                  |
| salarygrade           |
+-----------------------+
```

<br>

## *DROP*

- 테이블을 삭제한다.
- 제약 조건이 있을 경우에는 `DROP TABLE` 명령으로 삭제가 되지 않을 수 있다. 이럴 경우 테이블을 생성한 반대 순서로 삭제 해야한다.

```MYSQL
DROP TABLE 테이블이름;
```

```mysql
DROP TABLE NEW_EMPLOYEE;

+-----------------------+
| Tables_in_mydb        |
+-----------------------+
| bonus                 |
| department            |
| employee              |
| project               |
| project_participation |
| role                  |
| salarygrade           |
+-----------------------+
```

<br>

<br>

<br>

___

참고 : https://www.boostcourse.org/web326/joinLectures/28762







