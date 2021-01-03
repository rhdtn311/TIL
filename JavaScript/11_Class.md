# 클래스 (Class)

클래스는 객체를 생성하기 위한 탬플릿으로 연관있는 변수와 함수를 하나로 묶는 데 사용된다.

<br>

### *클래스 선언*

클래스는 다음과 같이 선언 가능하다. 일반적인 함수와는 다르게 호이스팅을 지원하지 않는다.

```javascript
class MyClass {
    constructor(parameter1, parameter2, ... ) {
        ...
    }
    method1() {...};
   	method2() {...};
    ...
}
```



#### constructor

constructor 메서드는 생성자로, 클래스로 생성된 객체를 초기화 하기 위한 메서드다.  "constructor" 이라는 이름을 가진 매서드는 클래스 안에 한 개만 존재할 수 있다.

```javascript
class People {
    constructor(name, age) {
        this.name = name
        this.age = age
    }
}

const Kong = new People('Kong',26);
console.log(Kong);	>>> People {name : "Kong", age : 26}
```

<br>

### *상속과 다형성*

자바스크립트에서 부모 클래스를 상속받아 부모 클래스에 정의된 매소드를 자식 클래스에서 사용할 수 있다.

```javascript
// Shape이라는 도형을 나타내는 클래스를 생성
class Shape {
    constructor(width, height, color) {
        this.width = width;
        this.height = height;
        this.color = color;
    }
    draw() {
        console.log(`I drawing this in ${this.color} color.`);
    }
    area() {
        return (this.width * this.height);
    }
}
```

extends 라는 명령어를 통해 클래스를 상속받을 수 있다.

```javascript
class Triangle extends Shape {}	// Triangle이라는 클래스는 Shape 클래스를 상속받음
```

Triangle은 Shape 클래스를 상속받았기 때문에 Shape 클래스에 정의된 메서드를 사용할 수 있다.

```javascript
const triangle = new Triangle(10,10,'red');

console.log(triangle.width);	>>> 10
console.log(triangle.draw());	>>> I drawing this in red color.

console.log(triangle.area());	>>> 100
```

Shape 클래스에서 도형의 넓이를 구하는 area 매서드는 너비 x 높이라는 사각형을 구하는 넓이 공식이 사용되었기 때문에 우리가 새로 생성한 triangle의 넓이를 구하는 공식과는 맞지 않다. 이럴 때 오버라이딩을 사용한다.

#### 오버라이딩

```javascript
class Triangle extends Shape {
    area() {
        return (this.height * this.width) / 2;	// 오버라이딩
    }
}

const triangle = new Triangle(10, 10, 'red');
console.log(triangle.area());	>>> 50
```

오버라이딩은 자식 클래스에 부모 클래스에서 오버라이딩 하고 싶은 매서드를 같은 이름으로 재정의한다. 만약 부모클래스에서 사용된 매서드를 다시 그대로 사용하고 싶다면 super.메서드명() 을 붙여주면된다.

<br>

### *instance of*

오브젝트가 특정 클래스의 인스턴스인지 확인해준다. 위에서 사용했던 예제를 그대로 사용한다.

```javascript
class Rectangle extends Shape {}
const rectangle =  new Rectangle(5,5,'blue');

console.log(rectangle instanceof Rectangle);	>>> true
console.log(rectangle instanceof Shape);	>>> true
console.log(rectangle instanceof Triangle);	>>> false
console.log(rectangle instanceof Object);	>>> true
// 모든 객체들은 Object를 상속하는 것이기 때문이다.
```

 <br>

<br>

___



참고 : [드림코딩 엘리](https://www.youtube.com/watch?v=_DLhUBWsRtw&t=1359s&ab_channel=%EB%93%9C%EB%A6%BC%EC%BD%94%EB%94%A9by%EC%97%98%EB%A6%AC)

