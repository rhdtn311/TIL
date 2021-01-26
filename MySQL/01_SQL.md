# SQL (Structured Query Language)

- SQL은 데이터를 보다 쉽게 검색하고 추가, 삭제, 수정과 같은 조작을 할 수 있도록 고안된 컴퓨터 언어이다.
- 관계형 데이터베이스에서 데이터를 조작하고 쿼리하는 표준 수단이다.
- 조작 언어
  - **DML (Data Manipulation Language)** : 데이터를 조작하기 위해 사용하는 언어로 `INSERT`, `UPDATE`, `DELETE`, `SELECT` 가 여기에 해당된다.
  - **DDL (Data Definition Language)** : 데이터베이스의 스키마를 정의 하거나 조작하기 위해 사용하는 언어로, `CREATE`, `DROP`, `ALTER` 등이 여기에 해당된다.
  - **DCL (Data Control Language)** : 데이터를 제어하는 언어로,권한을 관리하고, 데이터의 보안, 무결성 등을 정의하는 언어. `GRANT`, `REVOKE`가 여기에 해당된다.

<br>

## *데이터베이스 생성하기*

`consol`에 다음과 같이 입력하여 데이터베이스에 접속한다.

```mysql
# 데이터 베이스 접속
mysql -uroot -p	
# user is root, password
```

- 데이터베이스 생성 

  ``` sql
  create database DB이름;
  ```

- 생성한 데이터베이스를 사용하는 계정을 생성하고, 해당 계정이 데이터베이스를 **이용할 수 있는 권한**을 줘야 한다. 

  ```mysql
  grant all privileges on db이름.* to 계정이름@'클라이언트 이름' identified by '암호';
  flush privileges
  
  # *은 모든 권한을 의미하고, 클라이언트 이름에 %가 온다면 어떤 클라이언트에서든 접근이 가능하다는 의미이고, flush privileges는 DBMS에게 적용을 하라는 의미이다. 
  ```

<br>

## *데이터베이스에 접속하기*

데이터베이스를 생성하고 계정을 만들었다면 해당 데이터베이스에 접속할 수 있다.

```mysql
mysql -h호스트명 -uDB계정명 -p 데이터베이스이름;
```

<br>

## *데이터베이스 연결 끊기*

```mysql
quit
```

<br>

## *Mysql 구문 특징*

- 키워드는 대소문자를 구분하지 않는다.
- 여러 문장을 한 줄에 연속으로 붙여서 실행 가능하다. (`;`) 으로 구분
- 하나의 SQL은 여러 줄로 입력 가능하다. (`;`) 으로 구분
- SQL을 입력하는 도중 취소 가능하다. `Ctrl + C` 혹은 `\c` 입력
- DBMS에 조재하는 데이터베이스 확인 명령어 : `show databases`
- 사용중인 데이터베이스 전환 명령어 : `use` db이름
  - 데이터베이스를 전환하려면, 이미 데이터베이스가 존재해야 하며, 현재 접속 중인 계정이 해당 데이터베이스를 사용할 수 있는 권한이 있어야 한다.

<br>

### 실습

```mysql
mysql -uroot -p	# MySQL 관리자 계정인 root로 DBMS에 접속하겠다.

# 데이터베이스 생성
create database newDB;

# 데이터베이스 사용자 생성과 권한주기
grant all privileges on newDB.* to newDBuser@'%' identified by '123';
# 권한 줄 DB이름 : newDB
# 사용자 계정 : newDBuser, @'%' 모든 클라이언트(컴퓨터)에서 접근 가능
# 비밀번호 : 123
flush privileges;	# 적용

# MySQL과 접속 끊기 (root 계정에서 나감)
quit	

# 생성한 데이터베이스에 접속하기(root 계정에서 나간 후 newDBuser로 접속)
mysql -h127.0.0.1 -unewDBuser -p newDB
Enter password : 123
```

만약 `user` 라는 계정이 있고 그 계정에 `mydb`라는 데이터베이스가 있을 때, `newDBuser` 라는 계정의 `newDB`를 `user`에게 접근 가능하도록 하려면 다음과 같이 하면된다.

```mysql
# 우선 관리자 계정인 root로 접속한다.
mysql -uroot -p

# user라는 계정에 newDB라는 데이터베이스의 사용 권한을 준다.
grant all privileges on newDB.* to user@'%' identified by '123';

# 관리자 계정에서 나간다.
quit

# 다시 user에 접속한다.
mysql -uuser -123;

# database를 확인해본다.
show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mydb               |
| newdb              |
+--------------------+
```

<br>

## *테이블*

**RDBMS**의 기본적 저장구조로 한 개 이상의 **column**과 0개 이상의 **row**로 구성되어있다.

![image](https://user-images.githubusercontent.com/68289543/105808852-e6db0a00-5feb-11eb-96f6-3b1780c515e6.png)

- **열(column)** : 테이블 상에서의 단일 종류의 데이터를 나타낸다. 특정 데이터 타입 및 크기를 가지고 있다.
- **행(Row)** : 열들의 값의 조합. 레코드라고 불리며 **기본키(PK)**에 의해 구분된다. 
- **필드(Field)** : 행과 열의 교차점으로 필드는 데이터를 포함할 수 있고 없을 때는 `NULL` 값을 가지고있다.

<br>

### 현재 데이터베이스의 테이블 확인하기

```mysql
show tables;
```

실습을 위해 테이블이 있는 데이터베이스를 다운 받아 MySQL에 연결

```mysql
mysql -uuser -p mydb < examples.sql	# examples.sql이 데이터베이스 파일이다.
Enter password : 123

show tables;
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

### 특정 테이블의 구조 확인

```sql
desc 테이블이름;
```

```mysql
desc employee;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| empno    | int(11)      | NO   | PRI | NULL    |       |
| name     | varchar(10)  | YES  |     | NULL    |       |
| job      | varchar(9)   | YES  |     | NULL    |       |
| boss     | int(11)      | YES  | MUL | NULL    |       |
| hiredate | varchar(12)  | YES  |     | NULL    |       |
| salary   | decimal(7,2) | YES  |     | NULL    |       |
| comm     | decimal(7,2) | YES  |     | NULL    |       |
| deptno   | int(11)      | YES  | MUL | NULL    |       |
+----------+--------------+------+-----+---------+-------+
```

<br>
<br>
<br>

___
참고 : https://www.boostcourse.org/web326/lecture/258481








