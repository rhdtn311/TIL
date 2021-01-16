# 연산자

- **연산** : 프로그램에서 데이터를 처리하여 결과를 산출하는 것
- **연산자** : 연산에 사용되는 표시나 기호
- **피연산자** : 연산되는 데이터
- **연산식** : 연산자와 피연산자를 이용하여 연산의 과정을 기술한 것

다음은 자바에서 제공하는 연산자들이다.

| 연산자 종류 | 연산자                                             | 피연산자 수 | 산출값        | 기능 설명                             |
| ----------- | -------------------------------------------------- | ----------- | ------------- | ------------------------------------- |
| 산술        | +, -, *, /, %                                      | 이항        | 숫자          | 사칙연산 및 나머지 계산               |
| 부호        | +, -                                               | 단항        | 숫자          | 음수와 양수의 부호                    |
| 문자열      | +                                                  | 이항        | 문자열        | 두 문자열을 연결                      |
| 대입        | =, +=, -=, *=, /=, %=<br />.&=, ^=, <<=, >>=, >>>= | 이항        | 다양          | 우변의 값을 좌변의 변수에 대입        |
| 증감        | ++, --                                             | 단항        | 숫자          | 1만큼 증가/감소                       |
| 비교        | ==, !=, >, <, >=, <=,<br />instance if             | 이항        | boolean       | 값을 비교                             |
| 논리        | !, &, \|, &&, \|\|                                 | 단항, 이항  | boolean       | 논리적 NOT, AND, OR 연산              |
| 조건        | (조건식) ? A : B                                   | 삼항        | 다양          | 조건식에 따라 A 또는 B 중 하나를 선택 |
| 비트        | ~, &, \|, ^                                        | 단항, 이항  | 숫자, boolean | 비트 NOT, AND, OR, XOR 연산           |
| 쉬프트      | >>, <<, >>>                                        | 이항        | 숫자          | 비트를 좌측/우측으로 밀어서 이동      |

- 연산식은 반드시 하나의 값을 산출하기 때문에 하나의 값이 올 수 있는 곳이면 어디든지 값 대신에 연산식을 사용할 수 있다.

<br>

## *연산의 방향과 우선순위*

- 연산자에 따라 우선순위가 정해져 있다.
- 같은 우선순위의 연산자의 경우에는 연산식의 왼쪽부터 오른쪽으로 연산을 한다.
- 단항 연산자(++, --, ~, !), 부호 연산자(+, -), 대입 연산자(=, +=, -=, ...)는 오른쪽에서 왼쪽으로 연산된다.

```java
a = b = c = 5;
// 연산식은 c = 5, b = c, a = b 순서로 실행	
```

| 연산자                                     | 연산 방향                                                    | 우선순위 |
| ------------------------------------------ | ------------------------------------------------------------ | -------- |
| 증감(++, --), 부호(+, -), 비트(~), 논리(!) | ![image](https://user-images.githubusercontent.com/68289543/104811448-d9c95880-583e-11eb-8361-d0dc3b2d99f4.png) | 높음     |
| 산술(*, /, %)                              | ![image](https://user-images.githubusercontent.com/68289543/104811475-1b5a0380-583f-11eb-8fa8-bcd174da45c2.png) |          |
| 산술(+, -)                                 | ![image](https://user-images.githubusercontent.com/68289543/104811475-1b5a0380-583f-11eb-8fa8-bcd174da45c2.png) |          |
| 쉬프트(<<, >>, >>>)                        | ![image](https://user-images.githubusercontent.com/68289543/104811475-1b5a0380-583f-11eb-8fa8-bcd174da45c2.png) |          |
| 비교(<, >, <=, >=,instance of )            | ![image](https://user-images.githubusercontent.com/68289543/104811475-1b5a0380-583f-11eb-8fa8-bcd174da45c2.png) |          |
| 비교( ==, !=)                              | ![image](https://user-images.githubusercontent.com/68289543/104811475-1b5a0380-583f-11eb-8fa8-bcd174da45c2.png) |          |
| 논리(&)                                    | ![image](https://user-images.githubusercontent.com/68289543/104811475-1b5a0380-583f-11eb-8fa8-bcd174da45c2.png) | 중간     |
| 논리(^)                                    | ![image](https://user-images.githubusercontent.com/68289543/104811475-1b5a0380-583f-11eb-8fa8-bcd174da45c2.png) |          |
| 논리(\|)                                   | ![image](https://user-images.githubusercontent.com/68289543/104811475-1b5a0380-583f-11eb-8fa8-bcd174da45c2.png) |          |
| 논리(&&)                                   | ![image](https://user-images.githubusercontent.com/68289543/104811475-1b5a0380-583f-11eb-8fa8-bcd174da45c2.png) |          |
| 논리(\|\|)                                 | ![image](https://user-images.githubusercontent.com/68289543/104811475-1b5a0380-583f-11eb-8fa8-bcd174da45c2.png) |          |
| 조건(?:)                                   | ![image](https://user-images.githubusercontent.com/68289543/104811475-1b5a0380-583f-11eb-8fa8-bcd174da45c2.png) |          |
| 대입(=, +=, -= , ... )                     | ![image](https://user-images.githubusercontent.com/68289543/104811448-d9c95880-583e-11eb-8361-d0dc3b2d99f4.png) | 낮음     |

- 괄호() 를 사용하면 최우선순위가 된다.

<br>

## *단항 연산자*

단항 연산자는 피연산자가 하나뿐인 연산자를 말하며, **부호 연산자, 증감 연산자, 논리 부정 연산자, 비트 반전 연산자**가 있다.

<br>

#### **부호 연산자** (+, -)

부호 연산자는 양수 및 음수를 표시하는 +,-를 말한다. `boolean`타입과  `char` 타입을 제외한 나머지 기본 타입에 사용할 수 있다.

| 연산자 | 설명                 |
| ------ | -------------------- |
| +      | 피연산자의 부호 유지 |
| -      | 피연산자의 부호 변경 |

```java
int plusNumber = +10;
int minusNumer = -20;
```

- 변수 앞에 붙을 때는 부호를 유지하거나 바꾸기 위해 사용된다.

```java
int number = 10;
int result1 = +number;	// 10
int result2 = -number;	// -10
```

- **부호 연산자의 산출 타입은 `int`타입이다.**

```java
short number = 10;
short result = -number;	// 컴파일 에러

// 다음과 같이 변경 되어야 한다.
short number = 10;
int result = -number;	// -10
```

<br>

#### **증감 연산자(++, --)**

- 증감 연산자는 변수의 값을 1 증가(++)시키거나 1 감소(--)시키는 연산자를 말한다. `boolean` 타입을 제외한 모든 기본 타입의 피연산자에 사용할 수 있다.

| 연산식      | 설명                                                 |
| ----------- | ---------------------------------------------------- |
| ++피연산자  | 다른 연산을 수행하기 전에 피연산자의 값을 1 증가시킴 |
| -- 피연산자 | 다른 연산을 수행하기 전에 피연산자의 값을 1 감소시킴 |
| 피연산자++  | 다른 연산을 수행한 우헤 피연산자의 값을 1 증가시킴   |
| 피연산자--  | 다른 연산을 수행한 후에 피연산자의 값을 1 증가시킴   |

- 증감 연산자는 피연산자에 앞에 올 때와 뒤에 올 때의 연산식의 결과가 다르다.

```java
int x = 1;
int y = 1;
int result1 = ++x +10;	// x의 값이 1증가한 후 10과 더해줌 => 12
int result2 = y++ + 10;	// y가 10과 더하기(+) 연산을 마치고 1증가함 => 11
```

<br>

#### **논리 부정 연산자(!)**

- 논리 부정 연산자는 `true`를 `false`로, `false`를 `true`로 변경하기 때문에 `boolean` 타입에서만 사용할 수 있다.

| 연산식    | 설명                                                         |
| --------- | ------------------------------------------------------------ |
| !피연산자 | 피연산자가 true면 false<br />피연산자가 false면 true 값을 산출 |

<br>

#### **비트 반전 연산자(~)**

- 비트 반전 연산자는 정수 타입(`byte`, `short`, `int`, `long`)의 피연산자에만 사용되며, 피연산자를 2진수로 표현했을 때 비트값인 0을 1로, 1을 0으로 반전한다. 연산 후 부호 비트인 최상위 비트를 포함하여 모든 비트가 반전되기 때문에 부호가 반대인 새로운 값이 산출된다.

| 연산식             | 설명                        |
| ------------------ | --------------------------- |
| ~10 (00 ... 01010) | 산출 결과 : -11(11...10101) |

- 비트 반전 연산자의 산출 타입은 `int`타입이다.
- 비트 반전 연산자의 결과를 이용하면 부호가 반대인 정수를 구할 수도 있다. ( 비트 반전 연산자의 산출값 + 1)

```java
byte number = 30;
int minusNumber = ~number + 1;	// -30
```

- `integer.toBinayrString()` 메소드는 정수값을 총 32비트의 이진 문자열로 리턴해준다.

```java
int num = 10;
int num2 = ~10;
String binaryNum = Integer.toBinaryString(num);
String binaryNum2 = Integer.toBinaryString(num2);
while(binaryNum.length() < 32) {
			binaryNum = "0" + binaryNum;
		}
System.out.println(binaryNum);	// 00000000000000000000000000001010
System.out.println(binaryNum2);	// 11111111111111111111111111110101
```

<br>

## *이항 연산자*

- 이항 연산자는 피연산자가 두 개인 연산자를 말하며 **산술 연산자, 문자열 연산자, 대입 연산자, 비교 연산자, 논리 연산자**가 있다.

<BR>

#### **산술 연산자(+, -, *, /, %)**

- 일반적으로 말하는 사칙연산(+, -, *, /)과 나머지를 구하는 연산자(%)를 포함하여 5개이다.`boolean` 타입을 제외한 모든 기본 타입에 사용할 수 있다.

| 연산식              | 설명                                        |
| ------------------- | ------------------------------------------- |
| 피연산자 + 피연산자 | 덧셈                                        |
| 피연산자 - 피연산자 | 뺄셈                                        |
| 피연산자 * 피연산자 | 곱셈                                        |
| 피연산자 / 피연산자 | 좌측 피연산자를 우측 피연산자로 나눗셈 (몫) |
| 피연산자 % 피연산자 | 좌측 피연산자를 우측 피연산자로 나눈 나머지 |

- 산술 연산자는 피연산자들의 타입이 동일하지 않을 경우 다음과 같은 규칙을 사용해서 피연산자들의 타입을 일치시킨다.
  1. 피연산자들이 모두 정수타입이고, `int` 타입(4byte) 보다 크기가 작은 타입일 경우 모두 `int`타입으로 변환하여 연산 수행, 산출도 `int`
  2. 피연산자들이 모두 정수타입이고, `long` 타입이 있을 경우 모두 `long`타입으로 변환 후 연산을 수행, 산출도 `long`
  3. 피연산자 중 실수 타입이 있을 경우, 크기가 큰 실수 타입으로 변환 후 연산을 수행한다. 산출도 실수타입

```java
		int intValue1 = 10;
		int intValue2 = 4;
		
		int result1 = intValue1/intValue2;	// 정수/정수 연산이므로 정수를 반환하기 때문에 2를 산출
		double result2 = intValue1/intValue2;	// 정수/정수 연산이므로 정수를 반환하지만 반환 타입이 double이므로 2.0을 산출
		
		double result3 = (double)intValue1/intValue2;	// intValue1이 double이기 때문에 intValue2는 double로 변환 후 연산 => 2.5 산출
		double result3 = (intValue1*1.0) / intValue2;	// intValue1에 1.0이라는 실수 리터럴을 곱해 intValue1이 실수이므로 intValue2도 실수 타입으로 변환하여 연산 -> 2.5 산출
		}
```

- `char` 타입도 정수 타입이므로 산술 연산이 가능한데, `char`타입도 `int`타입으로 변환되므로 산출타입은 `int`이다.

```java
int i = 65;	// 65
char c1 = 'A' + 1;	// 유니코드 65 + 1 (리터럴 간의 연산은 타입 변환 없이 해당 타입으로 계산)
char c2 = (char)i+1;	// char 타입과 1이 더해지므로 char 타입이 int 타입으로 변환되어 char 타입인 c2에 담기지 못하고 컴파일 오류 발생
int i2 = 'A' + 1;	// int 타입인 i2에도 'A'의 유니코드 값인 65 + 1 = 66이 저장
```

<br>

#### ***산술 연산 시 주의사항***

1. **오버플로우 탐지**

   산술 연산을 할 때 연산 후의 산출값이 산출 타입으로 충분히 표현 가능한지 살펴봐야한다. 산출 타입으로 표현할 수 없는 값이 산출되었을 경우, 오버플로우가 발생하고 쓰레기값을 얻을 수 있기 때문이다.

   ```java
   int x = 1000000;
   int y = 1000000;
   int z = x * y; // z의 값이 int 범위를 초과하게 되어 -727379968을 산출한다.
   ```

   <br>

2. **정확한 계산은 정수 사용**

   정확하게 계산해야 할 때는 실수 타입을 사용하지 않는 것이 좋다. 

   ```java
   int a = 1;
   double doubleValue = 0.1;
   int b = 7;
   
   // 원하는 결과값은 3
   double result = a - b * doubleValue;	// 부동소수점 타입은 0.1을 정확히 표현할 수 없어 근사치를 처리 하기 때문에 0.29999999999999993
   ```

   위 예제를 다음과 같이 변경한다.

   ```java
   int a = 1;
   int aTen = 1 * 10;
   int b = 7;
   int temp = aTen - b;
   
   double result = temp/10.0;	// 3
   ```

   <br>

3. **NaN과 Infinity 연산**

   `/` 또는 `%` 연산자를 사용할 때 좌측 피연산자가 정수 타입인 경우 우측 피연산자는 0이 올 수 없다. 만약 0으로 나눈다면 컴파일은 정상적으로 되지만, 실행 시 `ArithmeticException`(예외)가 발생한다.

   ```java 
   5 / 0;	// ArithmeticException 예외발생
   5 % 0;	// ArithmeticException 예외발생
   ```

   자바는 프로그램 실행 도중 예외가 발생하면 실행 즉시 멈추고 프로그램은 종료된다. 그래서 예외가 발생하였을 경우 예외 처리를 해야한다.

   ```java
   5 / 0.0;	// Infinity
   5 % 0.0;	// NaN
   ```

   실수 타입인 0.0 또는 0.0f로 나누면 `ArithmeticException`가 발생하지 않고, `/` 연산의 결과는 `infinity` 값을 가지며, `%` 연산의 결과는 `NaN`을 가진다. 하지만 `Infinity`와 `NaN`이 결과로 나와도 다음 연산을 수행하면 안된다. 이 값과 산술 연산을 하면 어떤 수와 연산하더라도 `Infinity`와 `NaN`이 산출되기 때문이다.

   `Double.isInfinite()`, `Double.isNaN()` 메소드를 사용하여 `/`와 `%`의 결과가 `Infinity` 또는 `NaN`인지 확인할 수 있다.

   ```java
   double infinity = 5 / 0.0;
   double nan = 5 % 0.0;
   		
   System.out.println(Double.isInfinite(infinity));	//true
   System.out.println(Double.isNaN(nan));	//true
   ```

   <br>

4. **입력값의 NaN 검사**

   실수(부동소수점)를 입력받을 때는 반드시 `NaN` 검사를 해야한다. 

   ```java
   String userInput = "NaN";	// 사용자 입력값이 문자열 "NaN"
   double val = Double.valueOf(userInput);	// 입력값 문자열 "NaN"을 Double로 타입을 변환함 => double 타입의 NaN이 됌
   
   double number = 10000.0;	
   number += val;	// NaN + double = NaN
   ```

   위 결과는 원래 값(`number`)이 사라지고 `NaN`이 출력되기 때문에 문자열을 입력 받을 때는 반드시 `NaN`인지 검사해야한다.

   ```java
   String userInput = "NaN";
   double val = Double.valueOf(userInput);
   
   double number = 10000.0;
   
   if(Double.isNaN(val)) {	// == 연산자를 사용하면 안된다.
       System.out.println("NaN이 입력되어 처리할 수 없음");
       val = 0.0
   }
   
   number += val;	// NaN이 입력되어 처리할 수 없음
   				// 10000.0
   ```

   주의 해야 할 점은 `NaN`인지 조사할 때 `==` 연산자를 사용하면 안된다. `NaN` 은 `!=` 연산자를 제외한 모든 비교 연산자를 사용할 경우 `false` 값을 리턴하기 때문이다.

   <br>

   <br>

   <br>

   ___

   출처 : 한빛미디어 < 이것이 자바다 > 신용권























