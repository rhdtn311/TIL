# DML (Data Manipulation Language)

- 데이터 조작어(DML)에는 다음과 같이 4가지 조작어가 있다.
  - `SELECT` : 검색
  - `INSERT` : 등록
  - `UPDATE` : 수정
  - `DELETE` : 삭제

<br>

``` MYSQL
SELECT *
FROM EMPLOYEE;

# EMPLOYEE 테이블
+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | name   | job       | boss | hiredate   | salary  | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
```

<br>

## *SELECT*

```mysql
SELECT(DISTINCT) 컬럼명(ALIAS)
FROMT 테이블명;
```

- `SELECT` : 검색하고자 하는 데이터(컬럼)을 나열
- `DISTINCT` : 중복행을 제거
- `ALIAS` : 나타날 컬럼에 대한 이름을 부여
- `FROM` : 선택한 컬럼이 있는 테이블을 명시

```mysql
SELECT *	# *는 모든 컬럼을 나타냄
FROM EMPLOYEE;

+-------+--------+-----------+------+------------+---------+---------+--------+
| empno | name   | job       | boss | hiredate   | salary  | comm    | deptno |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+

SELECT NAME, JOB
FROM EMPLOYEE;
+--------+-----------+
| NAME   | JOB       |
+--------+-----------+
| SMITH  | CLERK     |
| ALLEN  | SALESMAN  |
| WARD   | SALESMAN  |
| JONES  | MANAGER   |
| MARTIN | SALESMAN  |
| BLAKE  | MANAGER   |
| CLARK  | MANAGER   |
| SCOTT  | ANALYST   |
| KING   | PRESIDENT |
| TURNER | SALESMAN  |
| ADAMS  | CLERK     |
| JAMES  | CLERK     |
| FORD   | ANALYST   |
| MILLER | CLERK     |
+--------+-----------+

# AS : 별칭 
SELECT NAME AS 이름, JOB AS 직업
FROM EMPLOYEE;
+--------+-----------+
| 이름   | 직업      |
+--------+-----------+
| SMITH  | CLERK     |
| ALLEN  | SALESMAN  |
| WARD   | SALESMAN  |
| JONES  | MANAGER   |
| MARTIN | SALESMAN  |
| BLAKE  | MANAGER   |
| CLARK  | MANAGER   |
| SCOTT  | ANALYST   |
| KING   | PRESIDENT |
| TURNER | SALESMAN  |
| ADAMS  | CLERK     |
| JAMES  | CLERK     |
| FORD   | ANALYST   |
| MILLER | CLERK     |
+--------+-----------+

# DISTINCT : 중복 제거
SELECT DISTINCT EMPNO
FROM EMPLOYEE;
+--------+
| deptno |
+--------+
|     10 |
|     20 |
|     30 |
+--------+
```

<br>

### concat

- 두 컬럼을 하나로 결합하여 출력한다.

```MYSQL
SELECT CONCAT(컬럼1,'-',컬럼2) ...;
```

<br>

> 예시

```MYSQL
SELECT CONCAT(EMPNO,'-',NAME) AS '사번-이름'
FROM EMPLOYEE;

+-------------+
| 사번-이름   |
+-------------+
| 7369-SMITH  |
| 7499-ALLEN  |
| 7521-WARD   |
| 7566-JONES  |
| 7654-MARTIN |
| 7698-BLAKE  |
| 7782-CLARK  |
| 7788-SCOTT  |
| 7839-KING   |
| 7844-TURNER |
| 7876-ADAMS  |
| 7900-JAMES  |
| 7902-FORD   |
| 7934-MILLER |
+-------------+
```

<br>

### UCASE, UPPER

- 소문자를 대문자로 바꿔서 출력해줌

```MYSQL
SELECT * 
FROM ROLE;
+---------+-----------------+
| role_id | description     |
+---------+-----------------+
|     100 | Developer       |
|     101 | Researcher      |
|     102 | Project manager |
+---------+-----------------+

SELECT UPPER(description)	# UPPER 대신 UCASE 사용 가능 
FROM ROLE;
+--------------------+
| UPPER(DESCRIPTION) |
+--------------------+
| DEVELOPER          |
| RESEARCHER         |
| PROJECT MANAGER    |
+--------------------+


```

<br>

### LOWER, LCASE

- 대문자를 소문자로 만들어줌

```MYSQL
SELECT LOWER(NAME)	# LOWER 대신 LCASE 사용 가능
FROM EMPLOYEE;
ORDER BY NAME;
+-------------+
| LCASE(NAME) |
+-------------+
| adams       |
| allen       |
| blake       |
| clark       |
| ford        |
| james       |
| jones       |
| king        |
| martin      |
| miller      |
| scott       |
| smith       |
| turner      |
| ward        |
+-------------+
```

<br>

### SUBSTRING

- 문자열을 끊어서 출력

```mysql
# SUBSTRING(문자열(칼럼),N 번째 글자 부터(시작), N+M 번째 글자 까지(끝))

SELECT SUBSTRING('MySQL',3,3);	# FROM문이 빠지면 테이블을 출력하는 것이 아니다.
+------------------------+
| SUBSTRING('MySQL',3,3) |
+------------------------+
| SQL                    |
+------------------------+
```

<br>

### LPAD, RPAD

- 공백을 원하는 문자로 채워준다.

```mysql
# LPAD(RPAD) (문자열(칼럼), 총N글자를 만듦, 공백을 채울 문자)

SELECT LPAD('lpad',6,'%');
+--------------------+
| LPAD('lpad',6,'%') |
+--------------------+
| %%lpad             |
+--------------------+

SELECT RPAD('rpad',10,'@');
+---------------------+
| RPAD('rpad',10,'@') |
+---------------------+
| rpad@@@@@@          |
+---------------------+
```

<br>

### TRIM, LTRIM, RTRIM

- 공백을 없애준다.
  - `TRIM` : 양쪽 공백 제거
  - `LTRIM` : 왼쪽 공백 제거
  - `RTRIM` : 으론쪽 공백 제거

```mysql
SELECT TRIM("   TRIM   ");
+--------------------+
| TRIM("   TRIM   ") |
+--------------------+
| TRIM               |
+--------------------+

SELECT LTRIM("   TRIM   ");
+---------------------+
| LTRIM("   TRIM   ") |
+---------------------+
| TRIM                |
+---------------------+

SELECT RTRIM("   TRIM   ");
+---------------------+
| RTRIM("   TRIM   ") |
+---------------------+
|    TRIM             |
+---------------------+
```



### ORDER BY

- 특정 컬럼을 기준으로 오름차순으로 정렬해준다.
- `DESC` 를 입력하여 내림차순으로 변경할 수 있다.

```MYSQL
SELECT EMPNO, NAME 
FROM EMPLOYEE ORDER BY EMPNO;	# 오름차순
+-------+--------+
| EMPNO | NAME   |
+-------+--------+
|  7369 | SMITH  |
|  7499 | ALLEN  |
|  7521 | WARD   |
|  7566 | JONES  |
|  7654 | MARTIN |
|  7698 | BLAKE  |
|  7782 | CLARK  |
|  7788 | SCOTT  |
|  7839 | KING   |
|  7844 | TURNER |
|  7876 | ADAMS  |
|  7900 | JAMES  |
|  7902 | FORD   |
|  7934 | MILLER |
+-------+--------+

SELECT EMPNO, NAME
FROM EMPLOYEE ORDER BY EMPNO DESC;	# 내림차순
+-------+--------+
| EMPNO | NAME   |
+-------+--------+
|  7934 | MILLER |
|  7902 | FORD   |
|  7900 | JAMES  |
|  7876 | ADAMS  |
|  7844 | TURNER |
|  7839 | KING   |
|  7788 | SCOTT  |
|  7782 | CLARK  |
|  7698 | BLAKE  |
|  7654 | MARTIN |
|  7566 | JONES  |
|  7521 | WARD   |
|  7499 | ALLEN  |
|  7369 | SMITH  |
+-------+--------+

# 컬럼명 대신 N번째 컬럼으로 지정할 수 있다.
SELECT EMPNO, NAME
FROM EMPLOYEE ORDER BY 2;	# 2번째 열은 NAME
+-------+--------+
| EMPNO | NAME   |
+-------+--------+
|  7876 | ADAMS  |
|  7499 | ALLEN  |
|  7698 | BLAKE  |
|  7782 | CLARK  |
|  7902 | FORD   |
|  7900 | JAMES  |
|  7566 | JONES  |
|  7839 | KING   |
|  7654 | MARTIN |
|  7934 | MILLER |
|  7788 | SCOTT  |
|  7369 | SMITH  |
|  7844 | TURNER |
|  7521 | WARD   |
+-------+--------+
```

<br>

## *WHERE*

- 검색 조건을 설정할 수 있다.

```mysql
SELECT 컬럼명
FROM 테이블명
WHERE 조건식
ORDER BY 칼럼 또는 표현식 (ASC, DESC)
```

- `WHERE`절에 올 수 있는 연산자들
  - 비교 연산자 (=, <, >, <=, >=, != , <>)
  - 논리 연산자 (AND, OR, NOT)
  - 범위 (BETWEEN A AND B)
  - 집합 (IN)
  - 패턴 (LIKE)
    - `%` : 0개이상의 문자열을 나타낸다.
    - `_` : 단 하나의 문자를 나타낸다.

```MYSQL
# 비교 연산자
SELECT NAME, DEPTNO
FROM EMPLOYEE
WHERE DEPTNO >= 20
ORDER BY DEPTNO ASC;
+--------+--------+
| NAME   | DEPTNO |
+--------+--------+
| SMITH  |     20 |
| JONES  |     20 |
| SCOTT  |     20 |
| ADAMS  |     20 |
| FORD   |     20 |
| ALLEN  |     30 |
| WARD   |     30 |
| MARTIN |     30 |
| BLAKE  |     30 |
| TURNER |     30 |
| JAMES  |     30 |
+--------+--------+

# 논리 연산자
SELECT NAME, DEPTNO, COMM
FROM EMPLOYEE
WHERE (DEPTNO = 30) AND NOT(COMM = 'NULL');
+--------+--------+---------+
| NAME   | DEPTNO | COMM    |
+--------+--------+---------+
| ALLEN  |     30 |  300.00 |
| WARD   |     30 |  500.00 |
| MARTIN |     30 | 1400.00 |
+--------+--------+---------+

# 범위
SELECT NAME
FROM EMPLOYEE
WHERE NAME BETWEEN 'A' AND 'D'
ORDER BY NAME ASC;
+-------+
| NAME  |
+-------+
| ADAMS |
| ALLEN |
| BLAKE |
| CLARK |
+-------+

# 집합
SELECT NAME, BOSS
FROM EMPLOYEE
WHERE BOSS IN (7902, 7698)
ORDER BY BOSS ASC;
+--------+------+
| NAME   | BOSS |
+--------+------+
| ALLEN  | 7698 |
| WARD   | 7698 |
| MARTIN | 7698 |
| TURNER | 7698 |
| JAMES  | 7698 |
| SMITH  | 7902 |
+--------+------+

# 패턴
SELECT NAME
FROM EMPLOYEE
WHERE NAME LIKE "A%"
ORDER BY NAME ASC;
+-------+
| NAME  |
+-------+
| ADAMS |
| ALLEN |
+-------+
```

<br>

<br>









