# 참조 타입

## *데이터 타입 분류*

- 자바의 데이터 타입은 크게 **기본 타입(primitive type)** 과 **참조 타입(reference type)** 으로 분류된다.
  - 기본 타입 : 정수, 실수, 문자, 논리 리터럴
  - 참조 타입 : 객체(Object)의 번지를 참조하는 타입 (배열, 열거, 클래스, 인터페이스 타입)
- **기본 타입을 이용해서 선언된 변수는 실제 값을 변수 안에 저장**하지만 **참조 타입을 이용해서 선언된 변수를 메모리의 번지를 값으로 갖는다.**

- **변수는 스택 영역**에 생성되고 **객체는 힙 영역**에 생성된다.

<br>

## *메모리 사용 영역*

JVM은 운영체제에서 할당받은 메모리 영역(Runtime Data Area)을 다음과 같이 세부 영역으로 구분해서 사용한다.

![image](https://user-images.githubusercontent.com/68289543/104838445-52dbb500-58fe-11eb-8826-ff41827377f3.png)

<br>

### 메소드(Method) 영역

메소드 영역에는 코드에서 사용되는 클래스(~.class)들을 클래스 로더로 읽어 클래스별로 **런타임 상수풀(runtime constant pool), 필드(field) 데이터, 메소드(method) 데이터, 메소드 코드, 생성자(constructor) 코드** 등을 분류해서 저장한다. 메소드 영역은 JVM이 시작할 때 생성되고 모든 스레드가 공유하는 영역이다.

<br>

### 힙(Heap)영역

힙 영역은 **객체**와 **배열**이 생성되는 영역이다. 힙 영역에 생성된 객체와 배열은 **JVM 스택 영역의 변수나 다른 객체의 필드에서 참조**한다. 참조하는 변수나 필드가 없다면 의미 없는 객체가 되기 때문에 이것을 쓰레기 수집기(Garbage Collector)를 실행시켜 쓰레기 객체를 힙 영역에서 자동으로 제거한다. 

<br>

### JVM 스택 (Stack)영역

JVM 스택 영역은 각 스레드마다 하나씩 존재하며 스레드가 시작될 때 할당된다. 자바 프로그램에서 추가적으로 스레드를 생성하지 않았다면 `main` 스레드만 존재하므로 JVM 스택도 하나이다. JVM 스택은 메소드를 호출할 때마다 프레임(Frame)을 추가(push)하고 메소드가 종료되면 해당 프레임을 제거(pop)하는 동작을 수행한다. 예외 발생 시 `printStackTrace()` 메소드를 보여주는 `Stack Trace`의 각 라인은 하나의 프레임을 표현한다. 

프레임 내부에는 로컬 변수 스택이 있는데, 기본 타입 변수와 참조 타입 변수가 추가(push)되거나 제거(pop)된다. 변수가 이 영역에 생성되는 시점은 초기화가 될 때, 즉 최초로 변수에 값이 저장될 때이다. 변수는 선언된 블록 안에서만 스택에 존재하고 블록을 벗어나면 스택에서 제거된다.

```java
char c1 = 'A';	// 스택 영역 [c1:'A']

if (c1 == 'A') {	// 스택 영역 [d1 : 1.23, v1 : 10, c1 : 'A']
    int v1 = 10;
    double d1 = 1.23;
}	// 블록을 빠져나가면 스택에서 제거(v1, d1)

boolean b1 = false;	// 스택 영역 [b1 : false, c1 : 'A']
```

기본 타입 변수는 스택 영역에 직접 값을 가지고 있지만, 참조 타입 변수는 값이 아니라 **힙 영역이나 메소드 영역의 객체 주소를 가진다.**  다음과 같이 배열 변수인 `scores`는 스택 영역에 생성되지만 실제 10, 20, 30을 갖는 배열은 힙 영역에 생성된다. 배열 변수 `scores`에는 배열의 **힙 영역의 주소가 저장**된다. 자바에서 배열은 객체로 취급된다.

```java
int[] scores = {10, 20, 30};

// 스택 영역 [scores : 5번지(주소)]
// 힙 영역 (5번지)[10, 20, 30]
```

<br>

## *참조 변수의 ==, != 연산*

- 참조 타입 변수들 간의 `==`,`!=` 연산은 동일한 객체를 참조하는지, 다른 객체를 참조하는지 알아볼 때 사용된다.
  - 참조 타입 변수의 값은 힙 영역의 객체 주소이므로 결국 주소 값을 비교하는 것이 된다.

<br>

## *null과 NullPointerException*

- 참조 타입 변수는 힙 영역의 객체를 참조하지 않는다는 뜻으로 `null` 값을 가질 수 있다. `null`로 초기화된 참조 변수는 스택 영역에 생성된다.
- 프로그램 실행 도중 `NullPointerException`이 발생하면, 예외가 발생된 곳에서 객체를 참조하지 않은 상태로 참조 타입 변수를 사용하고 있는 것이다.

<br>

## *String 타입*

문자열은 `String` 객체로 생성되고 변수는 `String` 객체를 참조한다.

```java
String name = "김철수";
String hobby = "자바";
```

위 코드에서  `name`과 `hobby`변수는 스택 영역에 생성되고, '김철수'와 '자바'는 힙 영역에 `String` 객체로 생성된다. 그리고 변수 `name`과 `hobby`에는 `String`객체의 주소 값이 저장되어 있다.

자바는 문자열 리터럴이 동일하다면 `String`객체를 공유하도록 되어 있다. 

```java
String name1 = "김철수";
String name2 = "김철수";

// name1과 name2는 같은 String 객체의 주소를 저장한다.
```

 일반적으로 변수에 문자열을 저장할 경우에는 문자열 리터럴을 사용하지만 다음과 같이 `new` 연산자를 사용해서 직접 `String`객체를 생성할 수 있다.

```java
String name1 = new String("김철수");
String name2 = new String("김철수");
```

단, 이 경우에는 `name1`과 `name1`가 다른 `String`객체를 참조한다.

```java
String name = "김철수";
name = null;
```

위 경우에는 변수 `name`은 `String`객체를 참조하고 있다가 변수에 `null`값이 들어옴으로써 더이상 객체를 참조하지 않게 되었다. 이 때 힙 영역에 있는 `String`객체는 쓰레기 객체가 되어 쓰레기 수집기(Gabage Collector)에 의해 메모리에서 자동 삭제된다.

<br>

## *배열 타입*

배열이란 같은 타입의 데이터를 연속된 공간에 나열시키고, 각 데이터에 인덱스(Index)를 부여해 놓은 자료구조이다.

```java
배열이름[인덱스]
```

배열의 인덱스는 위와 같이 표기하며, 인덱스는 배열의 각 항목의 데이터를 읽거나, 저장하는데 사용된다.

- 배열은 같은 타입의 데이터만 저장할 수 있다. (`int`배열은 `int` 값만, `String` 배열은 문자열만)
  - 만약 다른 타입의 값을 저장하려고 하면 타입 불일치(Type mismatch) 컴파일 오류가 발생한다.
- 한 번 생성된 배열은 길이를 늘리거나 줄일 수 없다.

<br>

## *배열 선언*

배열을 선언하는 방법은 다음과 같이 두 가지가 존재한다.

```java
타입[] 변수;	// 방법1
타입 변수[];	// 방법2
```

```java
// 방법1
int[] intArray;
double[] doubleArray;	

// 방법2
int intArray[];
double doubleArray[];
```

배열 변수는 참조 변수에 속한다. 배열도 객체이므로 힙 영역에 생성되고 배열 변수는 힙 영역의 배열 객체를 참조하게 된다.

<br>

## *값 목록으로 배열 생성*

배열 항목에 저장될 값의 목록이 있다면 다음과 같이 간단하게 배열 객체를 만들 수 있다.

```java
데이터타입[] 변수 = { 값0, 값1, 값2, ... };
```

중괄호{}는 주어진 값들을 항목으로 가지는 배열 객체를 힙에 생성하고, 배열 객체의 번지를 리턴한다.  예를 들어 다음과 같이 배열을 생성할 수 있다.

```java
String hobby [] = {"축구","야구","농구","테니스"};
```

그리고 "축구" 는 `hobby[0]`, 야구는 `hobby[1]`, 농구는 `hobby[2]`, 테니스는 `hobby[3]` 로 표현할 수 있고, 다음과 같이 대입 연산자를 사용하여 값을 변경할 수 있다.

```java
hobby[0] = "게임";
System.out.println(hobby[0]);	// 게임
```

단, 배열 변수를 이미 선언한 후에 다른 실행문에서 줄광호를 사용한 배열을 생성되지 않는다.

```java
int array[];
array = {1,2,3,4,5};	// 컴파일 에러
```

만약, 배열 변수를 미리 선언한 후, 값들이 나중에 결정되는 상황이라면 `new`연산자를 사용해서 값 목록을 지정해주면 된다.

```java
int array[];
array = new int[] {1,2,3,4,5};
```

<br>

## *new 연산자로 배열 생성*

값의 목록을 가지고 있지 않지만, 향후 값들을 저장할 배열을 미리 만들고 싶다면 `new` 연산자로 다음과 같이 배열 객체를 생성할 수 있다.

```java
타입[] 변수 = new 타입[길이];

// 예시
int[] array = new int[5];
```

길이는 배열이 저장할 수 있는 값의 수를 말한다. `new` 연산자로 배열을 생성할 경우, 이미 배열 변수가 선언된 후에도 가능하다.

```java
타입[] 변수 = null;
변수 = new 타입[길이];

// 예시 
int[] array = null;
array = new int[5];	// int array[] = {0, 0, 0, 0, 0}
```

`new` 연산자로 배열을 처음 생성할 경우 값들은 기본값인 0으로 초기화된다. (`String` 객체로 배열을 생성할 경우 `null`로 초기화된다.)

<br>

## *배열 길이*

- 배열의 길이란 배열에 저장할 수 있는 전체 항목 수를 말한다. 

- 코드에서 배열의 길이를 얻으려면 다음과 같이 배열 객체의 `length` 필드를 읽으면 된다.
  - 필드는 객체 내부의 데이터를 말한다.
  - `length` 필드는 읽기 전용 필드라 값을 변경할 수 없다.

```java
배열변수.length;
```

<br>

## *커맨드 라인 입력*

`main()` 메소드의 매개값인 `String[] args`는 무엇일까 ?

```java
public static void main(String[] args) { ... }
// Stringp[] args = { }; 
```

"java 클래스"로 프로그램을 실행하면 JVM은 길이가 0인 `String` 배열 을 먼저 생성하고 `main()` 메소드를 호출할 때 매개값으로 전달한다.

만약 다음과 같이 "java 클래스" 뒤에 공백으로 구분된 문자열 목록을 주고 실행하면, 문자열 목록으로 구성된 `String[]` 배열이 생성되고 `main()` 메소드를 호출할 때 매개값으로 전달된다.

```java
java 클래스 문자열0 문자열1 문자열2 . . . 문자열n-1
    
// 다음과 같다. String[] args = {문자열0, 문자열1, 문자열2, ... , 문자열n-1};
// 위 문자열들을 main() 메소드의 매개변수로 삽입한다.
```

<br>

## *다차원 배열*

- 행과 열로 구성된 배열을 2차원 배열이라고 한다.
- 자바는 2차원 배열을 중첩 방식으로 구현한다.

```java
int[][] scores = new int[2][3];	// 행이 2이고 열이 3인 2차원 배열
```

이 코드는 메모리에 다음과 같이 세 개의 배열 객체를 생성한다.

![image](https://user-images.githubusercontent.com/68289543/104846650-eae99680-591e-11eb-968f-94b898188969.png)

배열 변수인 `score`는 길이 2인 배열 A를 참조한다. 배열 A의 `scores[0]`은 다시 길이 3인 배열 B를 참조하고, `scores[1]`은 길이 3인 배열C를 참조한다. `score[0]`과 `score[1]` 모두 배열을 참조하는 변수 역할을 한다. 따라서 각 배열의 길이는 다음과 같다.

```java
scores.length;	// 2
scores[0].length;	// 3
scores[1].length;	// 3

// 파이썬으로 나타내면 scores = [[값1,값2,값3],[값1,값2,값3]] 과 마찬가지다.
```

```java
int score[][] = new int[2][];	// int타입의 2차원 배열 score은 2개의 값이 들어간다.
score[0] = new int[2];	// 배열 score의 0번째 인덱스에는 길이가 2인 int타입 배열이 들어간다.
score[1] = new int[3];	// 배열 score의 1번ㅉ 인덱스에는 길이가 3인 int타입 배열이 들어간다.

// 파이썬으로 나타내면 scores = [[값1, 값2],[값1, 값2, 값3]]
```

만약 그룹화된 값 목록을 가지고 있다면 다음과 같이 중괄호 안에 다시 중괄호를 사용해서 값 목록을 나열하면 된다.

```java
int[][] array = {{1,2},{3,4,5}};

int[0][0];	// 1
int[1][2];	// 5
```

<br>

## *객체를 참조하는 배열*

`String[]` 배열은 각 항목에 문자열이 아니라, `String` 객체의 주소를 가지고있다. 즉 `String` 객체를 참조하게 된다.

```java
String[] strArray = new String[3];
strArray[0] = "Java";
strArray[1] = "C+";
strArray[2] = "C#";
```

 따라서 `String[]` 배열의 항목 간에 문자열 비교는 `==` 연산자 대신 `equals()` 메소드를 사용해야한다.

```java
String array[] = new String[3];
array[0] = "Kim";
array[1] = "Kim";
array[2] = new String("Kim");

System.out.println(array[0] == array[1]);	// true
System.out.println(array[0] == array[2]);	// false

System.out.println(array[0].equals(array[1]));	// true
System.out.println(array[0].equals(array[2]));	// true
```

<br>

## *배열 복사*

배열은 한 번 생성하면 크기를 변경할 수 없기 때문에 더 큰 배열이 필요해진다면 새로운 큰 배열을 만들고 이전 배열로부터 값들을 복사해야 한다. 배열 간의 항목 값들을 복사하려면  `for문`을 사용하거나 `System.arraycopy()` 메소드를 사용한다.

```java
// for문을 이용

int oldArray[] = {1,2,3};
int newArray[] = new int[5];

for(int i = 0; i < oldArray.length; i++) {
    newArray[i] = oldArray[i];
	}
```

`System.arraycopy()` 메소드를 호출하는 방법은 다음과 같다.

```java
System.arraycopy(Object src, int srcPos, Object dest, int destPos, int length);
```

- `src` : 원본 배열
- `srcPos` : 원본 배열에서 복사할 항목의 시작 인덱스
- `dest` : 새 배열
- `destPos` : 새 배열에서 붙여넣을 시작 인덱스
- `length` : 복사할 개수

```java
// array1의 모든 배열을 array2에 복사
System.arraycopy(array1,0,array2,0,array1.length)
```

`String[]`과 같은 객체를 복사할 때는 원래 항목이 참조하는 객체와 복사한 항목이 참조하는 객체가 같아진다. 이것을 **얕은 복사(shallow copy)**라고 하고, 반대로 참조하는 객체도 별도로 생성하는 것을 **깊은 복사(deep copy)**라고 한다.

<br>

## *향상된 for문*

배열 및 컬렉션 객체를 좀 더 쉽게 처리할 목적으로 카운터 변수와 증감식을 사용하지 않는 향상된 `for문`을 사용한다.

```java
for (타입 변수 : 배열) {
    실행문;
}
```

`for 문`이 처음 실행될 때 배열에서 가져욜 첫 번째 값이 존재하는지 평가하고 가져올 값이 존재하면 해당 값을 변수에 저장하고 실행문을 실행한다. 실행문이 모두 실행되면 다시 루프를 돌아 배열에서 가져올 다음 값이 존재하는지 평가한다. 가져올 항목이 없다면 `for문`이 종료된다.

```java
int array[] = {1,2,3};
    for (int item : array) {
        System.out.print(item + " ");	// 1 2 3 
    }
```

<br>

## *열거 타입*

데이터 중에는 몇 가지로 한정된 값만을 갖는 경우가 있다. 예를 들어 요일과 같이 7개의 값만 같은 데이터들이 그러하다.  이와 같이 한정된 값만을 갖는 데이터 타입이 **열거 타입(enumeration type)**이다. 열거 타입은 몇 개의 **열거 상수(enumeration constant)** 중에서 하나의 상수를 저장하는 데이터 타입이다.

<br>

### 열거 타입 선언

- 먼저 열거 타입의 이름을 정하고 열거 타입 이름으로 소스파일(.java)을 생성해야한다.
- 열거 타입의 이름은 관례적으로 첫 문자는 대문자로하고 나머지는 소문자로 구성한다.
- `public enum` 키워드는 열거 타입을 선언하기 위한 키워드이다. 반드시 소문자로 작성해야한다.

```java
public enum 열거타입이름 { ... }
```

- 열거 타입을 선언했다면 열거 상수를 선언한다. (열거 상수는 관례적으로 대문자로 작성한다.)

```java
public enum Week { MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATERDAY, SUNDAY }
```

- 열거 상수가 여러 단어로 구성될 경우에는 단어 사이에 밑줄(_)을 입력하는 것이 관례적이다.

```java
public enum Name { FIRST_NAME, LAST_NAME }
```

<br>

### 열거 타입 변수

열거 타입도 하나의 데이터 타입이므로 변수를 선언하고 사용해야 한다. 

```java
열거타입 변수;

// ex
Week today;
Week reservationDay;
```

열거 타입 변수를 선언했다면 다음과 같이 열거 상수를 저장할 수 있다. 

```java
열거타입 변수 = 열거타입.상수;

// ex
Week today = Week.SUNDAY;
System.out.println(today);	// SUNDAY
```

열거 타입도 참조 타입이다. 그리고 열거 상수는 열거 객체로 생성된다. 예를들어 열거 타입 `Week`의 경우 `MONDAY` 부터 `SUNDAY`까지 총 7개의 `Week` 객체로 생성된다. 그리고 메소드 영역에 생성된 열거 상수가 해당 `Week`객체를 각각 참조하게 된다.

![image](https://user-images.githubusercontent.com/68289543/104868612-3768bc80-5987-11eb-9be9-a942edeb117e.png)

그렇다면 다음 코드는 어떻게 이해하면 좋을까?

```java
Week today = Week.SUNDAY;
```

열거 타입 변수 `today`는 스택 영역에 생성된다. `today`에 저장되는 값은 `Week.SUNDAY` 열거 상수가 참조하는 객체의 번지이다. 따라서 열거 상수 `Week.SUNDAY`와 `today` 변수는 서로 같은 `Week` 객체를 참조하게 된다.

![image](https://user-images.githubusercontent.com/68289543/104868674-6aab4b80-5987-11eb-8c89-9297be0b5072.png)

<br>

### 열거 객체의 메소드

열거 객체는 열거 상수의 문자열을 내부 데이터로 가지고 있다. 다음은 열거 객체가 가지는 데이터 및 메소드이다.

| 리턴 타입 | 메소드               | 설명                                  |
| --------- | -------------------- | ------------------------------------- |
| String    | name()               | 열거 객체의 문자열을 리턴             |
| int       | ordinal()            | 열거 객체의 순번(0부터)을 리턴        |
| int       | compareTo()          | 열거 객체를 비교해서 순번 차이를 리턴 |
| 열거 타입 | valueOf(String name) | 주어진 문자열의 열거 객체를 리턴      |
| 열거 배열 | values()             | 모든 열거 객체들을 배열로 리턴        |

<br>

#### name()

`name()`메소드는 열거 객체가 가지고 있는 문자열을 리턴한다. 리턴되는 문자열은 열거 타입을 정의할 때 사용한 상수 이름과 동일하다.

```java
Week today = Week.SUNDAY;
String name = today.name();	// SUNDAY
```

위 코드는 `todya`가 참조하는 열거 객체에서 `name()` 메소드를 호출하여 문자열을 얻어낸다. 

<br>

#### ordinal()

`ordinal()` 메소드는 전체 열거 객체 중 몇 번째 열거 객체인지 알려준다.

```java
Week today = Week.SATURDAY;
int dayNum = today.ordinal();	// 5
```

<br>

#### compareTo()

`compareTo()` 메소드는 매개값으로 주어진 열거 객체를 기준으로 전후로 몇 번째 위치하는지를 비교한다. 만약 열거 객체가 매개값의 열거 객체보다 순번이 빠르다면 음수가, 순번이 늦다면 양수가 리턴된다. 

```java
Week sun = Week.SUNDAY;
Week tues = Week.TUESDAY;

int result = sun.compareTo(tues);
System.out.println(result);	// 5
```

<br>

#### valueOf()

`valueOf() `메소드는 매개값으로 주어지는 문자열과 동일한 문자열을 가지는 열거 객체를 리턴한다.

```java
Week weekDay = Week.valueOf("MONDAY");

// weekDay 변수는 Week.MONDAY 열거 객체를 참조하게 된다.
```

<br>

#### values()

`values()` 메소드는 열거 타입의 모든 열거 객체들을 배열로 만들어 리턴한다.

```java
Week days[] = Week.values();
for(Week day : days) {
    System.out.println(day);
}
```

`Week` 배열은 다음과 같이 생성된다. 배열의 인덱스는 열거 객체의 순번과 같고 각 인덱스의 값은 해당 순번의 열거 객체 번지이다.

```java
// 스택 영역 days ---------> 힙 영역 [ , , , , , , ] ---------> 힙 영역 MONDAY,TUESDAY, ... , SUNDAY
```

즉, 스택 영역의 `days` 변수는 힙 영역의 각 인덱스 별로 Week 열거 객체의 번지를 가지고 있는 배열을 가리키고, 배열의 각 인덱스는 힙 영역의 순번에 맞는 열거 객체를 가르킨다. 

<br>

<br>

<br>

___

출처 : 한빛 미디어 <이것이 자바다> 신용권

그림 참조 : https://kephilab.tistory.com/41, https://programmer-seva.tistory.com/74

















