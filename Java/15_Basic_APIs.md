## **API** 클래스

- 프로그램 개발에 자주 사용되는 클래스 및 인터페이스 모음

<br>

### ***java.lang***

자바 프로그램의 기본적인 클래스를 담고 있는 패키지이기 때문에 `import` 없이 사용할 수 있다. 

<br>

### ***Object 클래스***

자바 최상위 클래스로 자바의 모든 클래스는 Object 클래스의 자식이거나 자손 클래스이다.

<br>

### equals()

- 두 객체가 동일한 객체면 `true` 그렇지 않으면 `false`를 리턴한다.
- 같은 객체이건 다른 객체이건 상관없이 객체가 저장하고 잇는 데이터가 동일하면 `true`

```java
Object object1 = new String("Object");
Object object2 = new String("Object");

System.out.println(object1.equals(object2));	// true
```

<br>

### hashCode()

- 객체의 메모리 번지를 이용해서 해시코드를 만들어 리턴
  - **객체 해시 코드** : 객체를 식별할 하나의 정수 값

<br>

### toString()

- 객체를 문자열로 표현한 값을 리턴
- 일반적으로 `toString()` 메소드는 "클래스명@16진수해시코드"로 구성된 문자 정보를 리턴

<br>

### clone()

- 원본 객체의 필드값과 동일한 값을 가지는 새로운 객체를 생성하는 것
- 원본 객체를 보호하기 위해 사용
- 객체를 복제하려면 원본 객체는 반드시 `java.lang.cloneable` 인터페이스를 구현하고 있어야 한다.
- `CloneNotSupportedException` 예외 처리가 필요한 메소드이기 때문에 `try-catch` 구문이 필요하다.

``` java
try {
    Object obj = clone();
} catch(CloneNotSupportedException e) {}
```



#### ***얕은 복제(thin clone)***

- 단순히 필드값을 복사해서 객체를 복제하는 것
- 복제 객체에서 참조 객체를 변경하면 원본 객체도 변경된 객체를 가지게 된다. (단점)

#### ***깊은 복제(deep clone)***

- 참조하고 있는 객체도 복제하는 것
- 깊은 복제를 하려면 `clone()` 메소드를 오버라이딩해서 참조 객체를 복제하는 코드를 직접 작성해야한다.

```java
public class Person implements Cloneable {
    public String name;
    public Profile profile;
    public String[] children;
    
    pubilc Person(String name, Profile profile, String[] children) {
        this.name = name;
        this.profile = profile;
        this.children = children;
    }
    
    @Override
    protected Object clone() throws CloneNotSupportedException {
        // 먼저 얕은 복사를 통해 name을 복제
        Member cloned = (Member) super.clone();
        
        // children[]을 깊은 복제
        cloned.children = Arrays.copyOf(this.children, this.children.length);
        
        // car를 깊은 복제
        cloned.profile = new Profile(this.profile.department);
        
        // 깊은 복제된 Member 객체를 리턴
        return cloned;
        
    }
}
```

<br>

### ***System 클래스***

- 운영체제의 일부 기능을 이용할 수 있다.
- System 클래스의 모든 필드와 메소드는 정적 필드와 정적 메소드로 구성되어 있다.

<br>

#### exit()

- 현재 실행하고 있는 프로세스를 강제 종료시킨다.
- 정상 종료 : 0, 비정상 종료 : 다른 값

```java
System.exit(0);
```

<br>

### ***Class 클래스***

- 클래스와 인터페이스의 메타 데이터를 관리
  - **메타 데이터** : 클래스의 이름, 생성자 정보, 필드 정보, 메소드 정보

<br>

#### getClass(), forName()

- Class 객체를 얻기 위해서 `getClass()` 메소드를 이용

```java
Class clazz = obj.getClass();
```

- `getClass()` 메소드는 해당 클래스로 객체를 생성했을 때만 사용할 수 있다.
- `forName()` 메소드는 클래스 전체 이름을 매개값으로 받고 Class 객체를 리턴한다.

```java
try {
    Class clazz = Class.forName(String className);
} catch (ClassNotFoundException e) {
}
```

<br>

### ***String 클래스***

문자열을 생성, 추출, 비교, 찾기, 분리 등의 메소드

<br>

#### String 생성자

```java
// 배열 전체를 String 객체로 생성
String str = new String(byte[] bytes);

// 지정한 문자 셋으로 디코딩
String str = new String(byte[] bytes, String charsetName);

// 배열의 offset 인덱스 위치부터 length만큼 String 객체로 생성
String str = new String(byte[] bytes, int offset, int length);

// 지정한 문자셋으로 디코딩
String str = new String(byte[] bytes, int offset, int length, String charsetName)
```

<br>

#### String 메소드

#### ***charAt()***

- 매개값으로 주어진 인덱스의 문자를 리턴

```java
String str = "가나다라마바사";
char c = str.charAt(3);

System.out.println(c);	// 라
```

<br>

#### ***equals()***

- 문자열을 비교함

```java
String str1 = new String("안녕");
String str2 = new String("안녕");

System.out.println(str1 == str2);	// false
System.out.println(str1.equals(str2));	// true
```

<br>

#### ***getBytes()***

- 문자열을 바이트 배열로 변환

```java
byte[] bytes1 = "ABCDEFG".getBytes();

System.out.println(Arrays.toString(bytes1));	// [65, 66, 67, 68, 69, 70, 71]
```

<br>

#### ***indexOf()***

- 매개값으로 주어진 문자열이 시작되는 인덱스를 리턴 (없으면 -1 리턴)

```java
String str = "abcdef";
int i = str.indexOf("c");
int notValue = str.indexof("없는 값");

System.out.println(i);	// 2
System.out.println(notValue);	// -1
```

<br>

#### ***length()***

- 문자열의 길이를 리턴

```java
String str = "apple";
int strLength = str.length();

System.out.println(strLength);	// 5
```

<br>

#### ***replace()***

- 첫 번째 매개값인 문자열을 찾아 두 번째 매개값인 문자열로 대치한 새로운 문자열을 생성하고 리턴

```java
String oldStr = "롤 하고싶다.";
String newStr = oldStr.replace("롤", "공부");

System.out.println(newStr);	// "공부 하고싶다."
```

<br>

#### ***substring()***

- 주어진 인덱스에서 문자열을 추출한다.

```java
substring(int beginIndex);	// beginIndex부터 끝까지
substring(int beginIndex, int endIndex);	// beginIndex부터 endIndex까지
```

```java
String str = "0123456789";
String subStr1 = str.substring(5);
String subStr2 = str.substring(5,9);

System.out.println(subStr1);	//	56789
System.out.println(subStr2);	//	5678
```

<br>

#### ***toLowerCase(), toUpperCase()***

- `toLowerCase()` : 문자열을 모두 소문자로 바꾼 새로운 문자열을 생성한 후 리턴
- `toUpperCase()` : 문자열을 모두 대문자로 바꾼 새로운 문자열을 생성한 후 리턴

```java
String lowerAlpha = "abcdefg";
String upperAlpha = "HIJKLMN";

String lowerToUpper = lowerAlpha.toUpperCase();
String upperToLower = upperAlpha.toLowerCase();

System.out.println(lowerToUpper);	// ABCDEFG
System.out.println(upperToLower);	// hijklmn
```

<br>

#### ***trim()***

- 문자열 앞뒤 공백을 제거한 새로운 문자열을 생성하고 리턴

```java
String oldStr = "      안녕하세용      ";
String newStr = oldStr.trim();

System.out.println(newStr);	// "안녕하세용"
```

<br>

#### ***valueOf()***

- 기본 타입의 값을 문자열로 변환

```java
int i = 10;
double d = 10.0;
char c = 'a';
boolean b = true;

String intToString = String.valueOf(i);
String doubleToString = String.valueOf(d);
String charToString = String.valueOf(c);
String booleanToString = String.valueOf(b);

System.out.println(intToString.getClass());		// class java.lang.String
System.out.println(doubleToString.getClass());	// class java.lang.String
System.out.println(charToString.getClass());	// class java.lang.String
System.out.println(booleanToString.getClass());	// class java.lang.String
```

<br>

#### ***split()***

- 정규 표현식을 구분자로 해서 문자열을 분리한 후, 배열에 저장하고 리턴

```java
String[] result = "문자열".split("정규표현식");
```

```java
String str = "김땡땡&박망망,이댕댕_공공공";
String[] result = str.split("&|,|_");

System.out.println(Arrays.toString(result));	// [김땡땡, 박망망, 이댕댕, 공공공]
```

<br>

### StringTokenizer 클래스

- 문자열이 한 종류의 구분자로 연결되어 있을 경우, 문자열을 손쉽게 분리할 수 있다.

```java
StringTokenizer st = new StringTokenizer("문자열", "구분자")	// 구분자를 생략하면 공백이 기본 구분자가 된다.
```

<br>

```java
String text = " 김땡땡/박망망/이댕댕/공공공";
StringTokenizer st = new StringTokenizer(text, "/");
```

위와 같이 `StringTokenizer`을 이용하여 문자열을 분리한 후 다음 메소드들을 이용하여 토큰을 사용할 수 있다.

- `countTokens()` : 꺼내지 않고 남아 있는 토큰의 수 
- `hasMoreTokens()` : 남아 있는 토큰이 있는지 여부
- `nextToken()` : 토큰을 하나씩 꺼내옴
  - 토큰을 하나 꺼내오면 `StringTokenizer` 객체에는 해당 토큰이 없어진다.

```java
int countToken = st.countTokens();
for (int i = 0; i < countToken; i++ ) {
    String getToken = st.nextToken();

    System.out.println(getToken);
}
/*
김땡땡
박망망
이댕댕
공공공
*/

while(st.hasMoreTokens()) {
    String getToken = st.nextToken();
    
    System.out.println(getToken);
}
/*
김땡땡
박망망
이댕댕
공공공
*/
```

<br>

### StringBuffer, StringBuilder 클래스

- 문자열을 변경하는 작업이 많을 경우에는 `StringBuffer` 또는 `StringBuilder` 클래스를 이용한다.
-  내부 버퍼에 문자열을 저장해 두고, 그 안에서 추가, 수정, 삭제 작업을 할 수 있도록 설계되어있다.

<br>

#### ***StringBuilder***

- 기본 생성자는 16개의 문자열을 저장할 수 있는 초기 버퍼를 만든다.
- `StringBuilder(int capacity)` 는 `capacity`의 수 만큼 문자들을 저장할 수 있는 초기 버퍼를 만든다.
  - 버퍼가 부족할 경우 자동으로 버퍼 크기를 늘리기 때문에 초기 버퍼의 용량은 중요하지 않다.

- 객체 생성 후 버퍼 내에서 문자 추가, 삽입, 삭제 등의 작업을 할 수 있다.
  - `append(...)` : 문자열 끝에 주어진 매개값을 추가
  - `insert(int offset, ...)` : 문자열 중간에 주어진 매개값을 추가
  - `delete(int start, int end)` : 문자열의 일부분을 삭제
  - `deleteCharAt(int index)` : 문자열에서 주어진 index의 문자를 삭제
  - `replace(int start, int end, String str)` : 문자열의 일부분을 다른 문자열로 대치
  - `StringBuilder reverse()` : 문자열의 순서를 뒤바꿈
  - `setCharAt(int index, char ch)` : 문자열에서 주어진 index의 문자를 다른 문자로 대치

```java
StringBuilder stringBuilder = new StringBuilder();

stringBuilder.append("게임");
stringBuilder.append(" 하고싶다.");
System.out.println(stringBuilder);	// 게임 하고싶다.

stringBuilder.insert(3," 안");
System.out.println(stringBuilder); // 게임 안하고싶다.

stringBuilder.delete(4,5);
System.out.println(stringBuilder);	//  게임 하고싶다.

stringBuilder.replace(0,2,"공부");
System.out.println(stringBuilder);	// 공부 하고싶다.

stringBuilder.setCharAt(1,'연');
System.out.println(stringBuilder);	// 공연 하고싶다.

stringBuilder.reverse();
System.out.println(stringBiulder);	// .다싶고하  연공
```

<br>

### Arrays 클래스

- 배열 조작 기능을 가지고 있다.
- `binarySearch(배열, 찾는 값)` : 전체 배열 항목에서 찾는 값이 있는 인덱스를 리턴
- `copyOf(원본배열, 복사할 길이)`  : 원본 배열의 0번 인덱스에서 복사할 길이만큼 복사한 배열 리턴, 복사할 길이는 원본 배열의 길이보다 커도 되며, 리턴 배열의 길이가 된다.
- `copyOfRange(원본배열, 시작 인덱스, 끝 인덱스)` : 원본 배열의 시작 인덱스에서 끝 인덱스까지 복사한 배열 리턴
- `deepEquals(배열, 배열)` : 두 배열의 깊은 비교
- `equals(배열, 배열)` : 두 배열의 얕은 비교 
- `fill(배열, 값)` : 전체 배열 항목에 동일한 값을 저장
- `fill(배열, 시작인덱스, 끝인덱스, 값)` : 시작 인덱스부터 끝 인덱스까지의 항목에만 동일한 값을 저장
- `sort(배열)` : 배열의 전체 항목을 오름차순으로 정렬
  - 사용자 정의 클래스 타입일 경우에는 클래스가 `Comparable` 인터페이스를 구현하고 있어야 정렬이 된다.
- `toString(배열)` : 배열을 문자열로 리턴

<br>

### Wrapper 클래스

- 기본 타입의 값을 갖는 객체를 생성할 수 있는 클래스
- 포장 객체의 특징은 포장하고 있는 기본 타입은 외부에서 변경할 수 없다.

<br>

#### ***박싱, 언박싱***

- 박싱 : 기본 타입의 값을 포장 객체로 만드는 과정
- 언박싱 : 포장 객체에서 기본 타입의 값을 얻어내는 과정

```java
// 박싱
Byte object = new Byte(10);
Byte object = new Byte("10");
Byte object = Byte.valueOf(10);
Byte object = Byte.vlaueOf("10");

Integer object = new Integer(10);
Integer ojbect = new Integer("10");
Integer object = Integer.valueOf(10);
Integer object = Integer.valueOf("10");

Boolean object = new Boolean(true);
Boolean object = new Boolean("true");
Boolean object = Boolean.valueOf(true);
Boolean object = Boolean.valueOf("true");

// 언 박싱 (기본타입명 + Value() 메소드를 이용)
byte obj = object.byteValue();
int obj = object.intValue();
boolean obj = object.booleanValue();
```

<br>

#### ***자동 박싱, 언박싱***

- 자동 박싱 : 포장 클래스 타입에 기본값이 대입될 경우 발생

```java
Integer boxingObject = 100;	// 자동 박싱 ( 힙 영역에 생성)
int unboxingObject = boxingObject;	// 자동 언박싱
```

<br>

#### ***문자열을 기본 타입 값으로 변환***

```java
byte num = Byte.parseByte("10");
short num = Short.parseShort("10");
int num = Integer.parseInt("10");
long num = Long.parseLong("10");
float num = Float.parseFloat("10.5F");
double num = Double.parseDouble("10.5");
boolean bool = Boolean.parseBoolean("true");
```

<br>

#### ***포장 값 비교***

- `==`와 `!=` 는 내부의 값을 비교하는 것이 아닌 포장 객체의 참조를 비교하기 때문에 사용할 수 없다.
- `equals()` 또는 언박싱을 해서 비교한다.

<br>

### Math, Random 클래스

#### ***Math 클래스***

- 수학 계산에 사용할 수 있는 메소드
- 모두 정적 메소드이기 때문에 Math 클래스로 바로 사용 가능하다.
- `abs()` : 절댓값
- `ceil()` : 올림
- `floor()` : 버림
- `max()` : 최대값
- `min()` : 최소값
- `random()` : 랜덤값 ( 0 이상 1 미만의 소수를 리턴)
- `rint()` : 가까운 정수의 실수값
- `round()` : 반올림값

<br>

<br>

<br>

____

















































































