# HTTP

**Hyper Text Transfer Protocol**의 약자로 인터넷에서 데이터를 주고받을 수 있는 포로토콜이다. HTTP는 웹에서 이루어지는 모든 데이터 교환의 기초이며, 클라이언트-서버 프로토콜이다. 클라이언트-서버 프로토콜이란, 보통 웹브라우저인 수신자 측에 의해 요청이 초기화되는 프로토콜을 의미한다. 

클라이언트와 서버들은 개별적인 메세지 교환에 의해 통신한다. 보통 브라우저인 **클라이언트에 의해 전송되는 메세지를 요청(request)**라고 부르며, 그에 대한 **서버에서의 응답으로 전송되는 메세지를 응답(responses)**이라고 부른다.

<br>

### HTTP 기반 시스템의 구성요소

HTTP는 클라이언트-서버 프로토콜로, **요청(request)**은 하나의 개체, 사용자 에이전트에 의해 전송된다. 일반적으로 사용자 에이전트는 브라우저지만, 웹을 돌아다니는 로봇이 될 수도 있다.

각각의 개별적인 요청들은 서버로 보내지고, 서버는 요청을 처리하고 그에대한 **응답(request)**을 한다. 

<br>

### HTTP 헤더

HTTP 헤더는 클라이언트와 서버가 요청 또는 응답으로 부가적인 정보를 전송할 수 있도록 해준다. HTTP 헤더는 대소문자를 구분하지 않는 이름과 콜론(:) 다음에 오는 값으로 이루어져있다. 헤더는 다음과 같이 구분된다.

- **General header** : 요청과 응답 모두에게 적용되지만 body에서 최종적으로 전송되는 데이터와는 관련이 없는 헤더
- **Request header** : 웹 브라우저가 웹 서버에게 요청한 데이터
- **Response header** : 응답에 대한 부가적인 정보를 갖는 헤더

우리는 웹 브라우저의 개발자도구를 이용하여 웹 브라우저와 웹 서버가 서로 주고받은 데이터인 HTTP Message를 볼 수 있다.

<br>

#### *HTTP headers*

- **Request Header**

  ![image](https://user-images.githubusercontent.com/68289543/104690893-98568180-5748-11eb-9ee1-72b320c5d214.png)

  

  - **-Request Line** : 데이터 처리 방식 (HTTP Request Method)과 요청하는 정보, 프로토콜 버전으로 구성되어 있다.
    - HTTP Request Method : 클라이언트는 Request Method들 중 하나를 사용하여 서버에게 요청 메세지를 보낼 수 있다.
      - GET : URL 형식으로 웹서버측 데이터를 요청
      - POST : 클라이언트에서 서버로 어떤 정보를 제출한다. (HTTP 바디에 담아서)
      - HEAD : GET과 비슷하지만 실제 문서를 요청하는 것이 아니라, 문서의 정보를 요청한다. (HTTP 헤더)
      - DELETE : 웹 리소스를 제거한다

  - **Host** : 인터넷에 연결되어 있는 컴퓨터를 식별하는 이름. 반드시 하나가 존재해야한다.
  - **User-Agent** : 웹 브라우저의 다른 표현으로 사용자의 웹 브라우저 정보가 포함되어 있다.
  - **Accept-Encoding** : 응답하는 데이터의 양이 많을 때 압축해서 전송하는데, 압축 방식과 같은 정보를 담고있다.
  - **Accept** : 요청을 보낼 때 서버에 이런 타입의 데이터(MIME)를 보내줬으면 좋겠다고 명시할 때 사용

<br>

- **Response Header**

  ![image](https://user-images.githubusercontent.com/68289543/104693016-4b74aa00-574c-11eb-8515-69ba92b25699.png)

  - **Status Line** : 버전, 응답결과(Status Code), 응답 결과를 문자로 표현
    - **Status Code** : 응답 결과를 숫자로 표현해줌
      - 1xx : informational
      - 2xx: 성공
      - 3xx : redirection
      - 4xx: 클라이언트 오류 
      - 5xx : 서버 오류
  - **Content-Type** : 응답해야 하는 타입
  - **Content-Length** : 응답하는 content의 전체 크기(byte)
  - **Content-Encoding** : 압축되어 있는 방식을 정의

<br>

<br>

___

참고 : [MDN](https://developer.mozilla.org/ko/docs/Web/HTTP)

https://developer.mozilla.org/ko/docs/Web/HTTP

https://www.zerocho.com/category/HTTP/post/5b344f3af94472001b17f2da
