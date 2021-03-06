# 변수

- 변수 : 하나의 값을 저장할 수 있는 메모리 공간

### *변수의  선언*

```java
타입 변수이름; // syntax

int age; // 정수(int) 값을 저장할 수 있는 age 변수 선언
double value; // 실수(double) 값을 저장할 수 있는 value 변수 선언
```

- 타입은 변수에 저장되는 값의 종류와 범위를 결정짓는 요소기 때문에 어떤 값을 변수에 저장할지 충분히 생각한 다음 결정해야 한다.
- 변수는 콤마(,)를 사용하여 한꺼번에 선언할 수 있다.

```java
int x, y, z;
```

<br>

### *변수의 명명 규칙*

| 작성 규칙                                                    | 예                                                        |
| ------------------------------------------------------------ | --------------------------------------------------------- |
| 첫 글자는 문자이거나 '$', '_' 이어야 하고 숫자로 시작할 수 없다. (필수) | 가능 : age, $age, _name<br />불가능 : 10name, @price, @#! |
| 영어 대소문자가 구분된다. (필수)                             | myname과 myName은 다른 변수                               |
| 첫 문자는 영어 소문자로 시작하되, 다른 단어가 붙을 경우 첫 문자를 대문자로 한다. (관례) | maxSeeed, firstName                                       |
| 문자 수(길이)의 제한은 없다.                                 |                                                           |
| 자바 예약어는 사용할 수 없다. (필수)                         | int, private, new, void                                   |

<br>

### *변수 값 저장*

- 변수에 값을 저장할 때는 **대입 연산자(=)**를 사용한다.
- 변수를 선언하고 처음 값을 저장할 경우, 이 값을 **초기 값**이라고 한다.
- 변수에 초기값을 주는 행위를 **변수의 초기화**라고 한다.

```java
int age;	// 변수 선언
age = 26;	// 값 저장

int score = 100;	// 선언과 동시에 값 저장
```

리터럴 : 소스 코드 내에서 직접 입력된 값

**정수 리터럴** :

- 소수점이 없는 정수 리터럴은 10진수로 간주한다.

- 0으로 시작되는 리터럴은 8진수로 간주한다.

  ```java
  02, -04
  ```

- 0x 또는 0X로 시작하고 0~9 숫자나 A, B, C, D, E, F 또는 a, b, c, d, e, f로 구성된 리터럴은 16진수로 간주한다/

  ```java
  0x5, 0xA, 0xB3
  ```

- 정수 리터럴을 저장할 수 잇는 타입은 `byte, char, short, int, long`과 같이 5개가 있다.

<br>

**실수 리터럴** :

- 소수점이 있는 리터럴은 10진수 실수로 간주한다.

  ```java
  0.25, -10.12
  ```

- 대문자 E 또는 소문자 e가 있는 리터럴은 10진수 지수와 가수로 간주한다.

  ```java
  5E7	// 5 x 10^7
  0.12E-5	// 0.12 x 10^-5
  ```

- 실수 리터럴을 저장할 수 있는 타입은 `float, double`이 있다.

<br>

**문자 리터럴** :

- 작은 따옴표(')로 묶은 텍스는 하나의 문자 리터럴로 간주한다.

  ```java
  'A', '김', '1', '\t'
  ```

- 역슬래쉬(\\)가 붙은 문자 리터럴은 이스케이프(escape) 문자라고도 하는데 특수한 용도로 사용된다.

  - `\t` : 수평 탭, `\n` : 줄바꿈, `\r` : 리턴

- 문자 리터럴을 저장할 수 있는 타입은 `char`이다.

<br>

**문자열 리터럴** :

- 큰따옴표(")로 묶는 텍스트는 문자열 리터럴로 간주한다. 큰따옴표 안에는 텍스트가 없어도 문자열 리터럴로 간주된다.

  ```java
  "Hello World !"
  "한줄 내려 쓰기 \n 합니다."
  ```

-  문자열 리터럴을 저장할 수 있는 타입은 `String`이다.

<br>

**논리 리터럴** :

- true와 false는 논리 리터럴로 간주한다.

  ```java
  true, false
  ```

- 논리 리터럴을 저장할 수 있는 타입은 `boolean`이다.

<br>

### *변수의 사용 범위*

- 변수는 중괄호 {} 블록 내에서 선언되고 사용된다, 중괄호 블록을 사용하는 곳은 **클래스, 생성자, 메소드**이다. 메소드 블록 내에서 선언된 변수를 **로컬 변수(local variable)**라고 한다. 로컬 변수는 메소드 실행이 끝나면 메모리에서 자동으로 없어진다. 

  ```java
  // main 메소드에서 변수 선언
  
  public class VariableExample {
      public static void main(String[] args) {
          int value = 10;	// 변수 선언 및 초기값 저장
          int sum = value + 20;
          System.out.println(sum);
      }
  }
  ```

  - 변수는 선언된 블록 내에서만 사용이 가능하다.
    - `for`, `if`, `while` 과 같은 제어문 블록에서 선언된 변수는 해당 제어문 블록 내에서만 사용이 가능하고 블록 밖에서는 사용할 수 없다. 

<br>

### *데이터 타입*

- 모든 변수에는 타입이 있으며 타입에 따라 저장할 수 있는 값의 종류와 범위가 달라진다. 
- 변수를 선언할 때 주어진 타입은 변수를 사용하는 도중에 변경할 수 없다.

<br>

#### **정수 타입** 

| 정수 타입 | byte | char | short | int  | long |
| --------- | ---- | ---- | ----- | ---- | ---- |
| 바이트 수 | 1    | 2    | 2     | 4    | 8    |

- 자바는 기본적으로 정수 연산을 `int`타입으로 수행한다. 그렇기 때문에 저장하려는 값이 정수 리터럴이라면 특별한 이유가 없는 한 `int`타입 변수에 저장한다.

- `byte` 타입 : 정수 타입 중에서 가장 작은 범위의 수를 저장

- `char` 타입 : 하나의 유니코드를 저장하기 위해 2byte 크기인 `char` 타입을 제공한다. 

  - 유니코드엔 음수가 없기 때문에  `char`타입에는 음수를 저장할 수 없다.
  - `char` 타입의 변수에 어떤 문자를 대입하지 않고 단순히 초기화할 목적이라면 공백 하나를 포함해서 초기화 해야한다. ex) \' \'

- `short` 타입 : `short` 타입은 2byte로 표현되는 정수 값을 저장할 수 있는 데이터 타입이다.

- `int` 타입 : `int` 타입은 4byte로 표현되는 정수값을 저장할 수 있는 데이터 타입이다.

  - 자바에서 정수 연산을 하기 위한 기본 타입이다. ( `byte` 타입 변수 + `short` 타입 변수 = `int` 타입으로 변환 후 연산 수행)

- `long` 타입 : `long` 타입은 8byte로 표현되는 정수값을 저장할 수 있는 데이터 타입으로 수치가 큰 데이터를 다루는 프로그램에서 필수적으로 사용된다.

  - `long`타입의 변수를 초기화할 때는 정수값 뒤에 소문자 'l' 이나 대문자 'L'을 붙일 수 있다. 만약 초기화 하는 정수가 `int`타입의 크기를 넘어간다면 꼭 'L'를 붙여줘야한다. 그렇지 않으면 컴파일 에러가 난다.

  ```java
  public class LongExample {
      public static void main(String[] args) {
          long var1 = 10;
          long var2 = 20L;
          long var3 = 1000000000000;	// 컴파일 에러
          long var4 = 1000000000000L;
      }
  }
  ```

  **<br>**

  #### **실수 타입**

  - 소수점이 있는 실수 데이터를 저장할 수 있는 타입

    | 실수 타입 | float | double |
    | --------- | ----- | ------ |
    | 바이트 수 | 4     | 8      |

  - `float`과 `double` 의 메모리 사용 크기는 각각 `int`와 `long`의 크기와 같지만, 정수 타입과는 다른 저장 방식 때문에 정수 타입보다 훨씬 더 큰 범위의 값을 저장할 수 있다. ( 부동소수점 방식 )
  - `double`이 `float`보다 더 정밀한 값을 저장할 수 있기 때문에 높은 정밀도를 요구하는 계산에서는 `double`을 사용해야 한다.
  - 자바에서는 실수 리터럴의 기본 타입을 `double`로 간주한다.
  - 실수 리터럴을 `float` 타입 변수에 저장하려면 리터럴 뒤에 소문자 'f'나 대문자 'F'를 붙여야 한다.

  ```java
  double var1 = 0.123;
  float var2 = 0.123;	// 컴파일 에러
  float var3 = 0.123F;
  ```

  <br>

  #### **논리 타입(boolean)**

  - `boolean ` 타입은 1byte로 표현되는 논리값 (true/ false)을 저장할 수 있는 데이터 타입이다.
  - 상태값에 따라 조건문과 제어문의 실행 흐름을 변경하는데 주로 이용

<br>

### *타입 변환*

- 데이터 타입을 다른 데이터 타입으로 변환하는 것
- 타입 변환에는 **자동(묵시적) 타입 변환**과 **강제(명시적) 타입 변환**이 있다.

<br>

#### 자동 타입 변환

- 프로그램 실행 도중 자동적으로 타입 변환이 일어나는 것
- 작은 크기를 가지는 타입이 큰 크기를 가지는 타입에 저장될 때 발생

``` java
byte(1) < short(2) < int(4) < long(8) < float(4) < double(8)	// 타입의 크기 비교
// 표현할 수 있는 값의 범위가 long보다 float이 더 크다.
```

```java
byte byteValue = 10;
int intValue = byteValue;	// 자동 타입 변환 
```

위 예에서 `byteValue`는 `byte`타입이므로 1byte 크기를 가지고 `intValue`는 `int` 타입이기 때문에 4byte의 크기를 가진다. 따라서 `byteValue`는 `int`타입 `intValue`로 자동 타입 변환된다.

- 자동 타입 변환이 되면 작은 그릇의 물을 큰 그릇의 물에 옮긴 것처럼 값은 동일하다.
- 정수 타입이 실수 타입으로 변환하는 것은 무조건 자동 타입 변환이 된다.
- `char`타입의 경우 `int`타입으로 자동 변환되면 유니코드 값이 `int`타입에 저장된다.

```java
int intValue = 10;
double doubleValue = intValue;	// 10.0

char charValue = 'A';
int intValue = charValue;	// 65
```

<br>

#### 강제 타입 변환

- 강제적으로 큰 데이터 타입을 작은 데이터 타입으로 쪼개어서 저장하는 것 (= **캐스팅 : Casting**)

```java
int intValue = 10;
byte byteValue = (byte) intValue;	// 10
```

위 코드를 보면 `intValue`는 4byte의 `int` 타입이지만 `(byte)` 캐스팅 연산자를 사용해서 `int` 타입을 1byte씩 4 부분으로 쪼개서 맨 뒤에 있는 부분 1byte만 `byte`타입인 `byteValue`에 저장하였다.  끝에있는 1byte만 저장하므로 만약 `intValue`가 1byte 만으로 표현하지 못한다면, `byte`타입으로 변환했을 때 값이 보존되지 못한다. 하지만 위와 같이 1byte만으로 표현 가능하다면 값이 보존된다.

- 실수 타입을 정수 타입으로 강제 타입 변환 시 소수점 이하 부분은 사라지고 정수 부분만 저장된다.

```java
double doubleValue = 2.1592;
int intValue = (int) doubleValue;	// 2
```

- 강제 타입 변환 시 값이 손실 되지 않도록 주의해야한다. 따라서 다음과 같이 사용한다.

```java
public class Hello {
	public static void main(String[] args) {
		int intValue = 127;
		byte byteValue = 0;
		if ((Byte.MIN_VALUE <= intValue) && (Byte.MAX_VALUE >= intValue)) {
			System.out.println(byteValue = (byte) intValue);}
		else {
			System.out.println("변환할 수 없습니다.");
		}
    }
}
```

- `int` 타입을 실수타입으로 강제 타입 변환하기 위해선 근사치로 변환되는 것을 막기 위해 더 정밀한 `double`을 이용한다.

<br>

#### 연산식에서의 자동 타입 변환

- 연산은 기본적으로 같은 타입의 피연산자 간에만 수행되기 때문에 서로 다른 타입의 피 연산자가 있을 경우 두 피연산자 중 크기가 큰 타입으로 자동 변환된 후 연산을 수행한다.

```java
int intValue = 10;
double doubleValue = 10.5;
double result = intValue + doubleValue;	// intValue가 double타입으로 자동 변환 후 연산 수행 => 20.5
```

- 자바의 경우 정수 끼리 연산할 때 `int` 타입을 기본으로 한다. 그 이유는 피연산자를 4byte 단위로 저장하기 때문이다. 따라서 `int` 타입보다 작은 타입끼리의 연산도 `int` 타입으로 변환한 후 연산하여 `int` 타입의 결과를 반환한다.

```java 
byte value1 = 5;
byte value2 = 10;
byte value3 = value1 + value2;	// 컴파일 에러
int value4 = value1 + value2;	// 15
```

- `char` 타입 끼리의 연산 후 문자로 출력하고 싶으면 `char` 타입으로 강제 타입 변환을 해줘야한다.

```java
char value1 = 1;
char value2 = 'A';
int intResult = value1 + value2;	// 66
char charResult = (char)(value1 + value2);	// B
```

- 피연산자 중 하나가 `long` 타입이라면 다른 피연산자도 `long` 타입으로 자동 타입 변환되고 연산의 결과는 `long` 타입이 된다.
- 피연산자 중에 실수 리터럴이나 `double` 타입이 있다면 다른 피연산자도 `double` 타입으로 자동 타입 변환되어 연산되므로 결과는 `double` 타입으로 산출된다.

```java
int intValue1 = 10;
int intResult = intValue1/4;	// 2
int intResult2 = intValue1/4.0;	// 컴파일 에러 ( 4.0은 실수 리터럴임)
double doubleResult = intValue1/4.0;	// 2.5
```

<br>

<br>

<br>

___

출처 : 한빛미디어 <이것이 자바다> 저자 : 신용권

