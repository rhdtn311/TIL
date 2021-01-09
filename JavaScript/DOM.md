## DOM (Document Object Model)

문서 객체 모델이라고 불리는 **DOM (Document Object Model)**은 XML이나 HTML 문서에 접근하기 위한 인터페이스이다.  DOM은 다음과 같이 트리 객체로 구성된다.

![image](https://user-images.githubusercontent.com/68289543/104085048-cc84fa80-528f-11eb-8c70-0bb898ffefc7.png)



자바스크립트로   이 객체 모델을 이용하여 다음과 같은 작업을 할 수 있다.

- 자바스크립트는 새로운 **HTML요소나 속성을 추가**할 수 있다.
- 자바스크립트는 존재하는 **HTML 요소나 속성을 제거**할 수 있다.
- 자바스크립트는 HTML 문서의 **모든 HTML요소를 변경**할 수 있다.
- 자바스크립트는 HTML 문서의 **모든 HTML 속성을 변경**할 수 있다.
- 자바스크립트는 HTML 문서의 **모든 CSS 스타일을 변경**할 수 있다.
- 자바스크립트는 HTML 문서에 **새로운 HTML 이벤트를 추가**할 수 있다.
- 자바스크립트는 HTML문서의 **모든 HTML 이벤트에 반응** 할 수 있다.

<br>

### Document 객체

Document 객체는 웹 페이지 자체를 의미한다. 만약 HTML 페이지의 요소에 접근하길 원한다면 반드시 document 객체부터 시작해야 한다.

<br>

### Document 메소드

Document 객체는 HTML 요소와 관련된 작업을 도와주는 다양한 메소드를 제공한다.

- **HTML 요소를 선택**

  | 메소드                                       | 설명                                |
  | -------------------------------------------- | ----------------------------------- |
  | document.getElementById(id)                  | 요소의 id로 해당 요소를 선택        |
  | document.getElementsByTagName(태그 이름)     | 태그 이름으로 요소를 선택           |
  | document.getElementsByClassName(클래스 이름) | 해당 클래스에 속한 모든 요소를 선택 |

- **HTLM 요소를 변경**

  | 속성                               | 설명                            |
  | ---------------------------------- | ------------------------------- |
  | element.innerHTML = "content"      | 요소 내부의 HTML을 변경한다.    |
  | element.attribute = new value      | HTML 요소의 속성 값을 변경한다. |
  | element.style.property = new style | HTML 요소의 스타일을 변경한다.  |

- **HTML 요소를 생성**

  | 메소드                           | 설명                                           |
  | -------------------------------- | ---------------------------------------------- |
  | document.createElement(HTML요소) | 지정된 HTML 요소를 생성한다.                   |
  | document.write(text)             | HTML 출력 스트림을 이용하여 텍스트를 출력한다. |

  <br>

  <br>

  ___

  출처 : https://www.w3schools.com/js/js_htmldom.asp

  ​		   http://www.tcpschool.com/javascript/js_dom_concept
