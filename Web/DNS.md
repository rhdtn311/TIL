# DNS(Domain Name System)

두 대의 컴퓨터가 인터넷을 통해서 통신을 하기 위해서 반드시 필요한 것이 있다. 그것은 바로 **IP 주소**이다.

![image](https://user-images.githubusercontent.com/68289543/104828832-ae7f5180-58b0-11eb-9e5a-6f2ea0b77783.png)

만약 왼쪽에 있는 컴퓨터가 클라이언트라고 하고,  왼쪽의 컴퓨터에서 오른쪽에 있는 컴퓨터를 서버로 접속하고자 한다면,  웹브라우저에 93.184.216.34를 입력해야 한다. 즉, 클라이언트가 서버에 접속하기 위해서는 서버의 IP를 알아야한다. 그 후에 서버는 어떠한 정보를 생성한 다음에 클라이언트에게 제공한다.그러기 위해서 서버 컴퓨터는 클라이언트 컴퓨터의 IP를 알아야한다. 즉, 인터넷에 참여하는 모든 컴퓨터들은 각자 IP주소를 가지고 있어야한다. 이 때, 인터넷에 연결되어 있는 장치들은 컴퓨터 뿐만 아니라 여러가지 것들이 있다. 우리는 포괄적으로 인터넷에 연결되어있는 각각의 장치(컴퓨터)들을 **호스트(host)**라고 한다.

다시 돌아가서 우리가 만약 93.184.216.34라는 IP 주소를 가진 컴퓨터에 접속을 하려 한다면, IP 주소는 기억하기 힘들기 때문에 어려움을 겪을 수 있다. 이러한 불편함을 없애기 위해서 사용할 수 있는 방법이 있다. 

모든 운영체제에는 hosts라는 파일이 존재한다. 그리고 우리가 만약 *"그 hosts파일에 example.com의 ip주소는 93.184.216.34이다."* 라고 적어놓으면 example.com에 접속했을 때 hosts파일에 있는 내용을 읽어서 컴퓨터는 93.184.216.34에 접속하게된다. 이것이 hosts라는 파일의 역할이고 이것을 통해서 우리는 DNS(Domain Name Service)를 통하지 않고도 우리가 자주 사용하는 사이트나 우리만의 사이트에 도메인 주소와 같은 host의 이름을 부여할 수 있다.

<br>

## *DNS의 등장 배경*

만약 내가 특정 사이트에 간편하게 접속하기 위해 내 hosts파일을 변경하여 이름을 설정하여 접속한다면, 그것은 나에게만 해당되는 것이다. 그래서 서버쪽에서는 *'만약 내 서버에 접속하기 위해서는 어려운 IP 주소가 아닌, 이름으로 접속할 수 있으면 얼마나 좋을까?'* 라는 생각을 하게된다. 그렇게 된다면 IP 주소가 바뀌어도 등록해놓은 이름은 바뀌지 않기 때문에 유연함을 유지할 수도 있다. 이 방법을 사용하기 위해서 전 세계에 hosts파일을 관리하는 Stanford Reserch Institute라는 단체를 필요로 했다. 서버쪽 컴퓨터에서 Stanford Reserch Institute에게 *"93.184.216.34는 example.com으로 해주세요."* 라는 요청을 하게되고  Stanford Reserch Institute는 자신들이 관리하는 hosts파일을 갱신하여 일을 처리하였다. 

하지만 인터넷이 커짐으로써 이 방법에 여러가지 문제가 제기되기 시작하였다. 클라이언트가  Stanford Reserch Institute로부터 갱신된 hosts파일을 받기 전까지는 IP 주소로 접속을 해야했거나,  Stanford Reserch Institute에서는 host 파일을 일일이 수작업으로 갱신해줘야 했다. 이 과정에서 많은 시간과 많은 비용이 들었다. 또한 한 hosts 파일에서 모든 인터넷의 주소를 관리하는 것은 당연히 한계에 봉착할 수 밖에 없었다. 이러한 한계를 극복하기 위해서 등장한 것이 **DNS(Domain Name System)이다.**

<br>

## *DNS란 ?*

![image](https://user-images.githubusercontent.com/68289543/104829685-74667d80-58b9-11eb-8db7-6b0cf8fe8da9.png)

서버쪽에서 자신의 IP에 이름을 설정하고 싶다면 DNS Server에게 요청을 한다. 그러면 DNS Server에서 해당 IP 주소와 요청한 이름을 DNS Server에 저장한다. 만약 우리가 컴퓨터에 인터넷을 연결하게 된다면 어떠한 메커니즘에 의해 우리 컴퓨터에는 DNS Server의 IP 주소가 자동으로 세팅이된다. 그래서 만약 우리가 특정 사이트에 접속하기 위해 `www.example.com` 을 입력하게 된다면 첫 번째로 우리의 hosts 파일을 탐색한다. 만약 hosts 파일에 맞는 정보가 없으면 그 다음에 DNS Server에 접속해서 `www.example.com`의 IP 주소를 요청하고 DNS Server에서 그에 맞는 IP 주소를 응답해주게된다. 그렇게 우리는 해당 IP 주소를 가진 컴퓨터에 연결하게된다. 이처럼 DNS Server를 이용하는 모든 컴퓨터들은 서버의 IP 주소가 바뀌어도 문제 없이 서버에 접속할 수 있게된다. 

<br>

## *Public DNS*

컴퓨터가 원하는 도메인 이름의 IP 주소를 알아낼 수 있는 이유는 컴퓨터에 연결된 **local DNS Server** 덕분이다. 이 local DNS Server는 우리가 인터넷을 연결할 때 이용한 통신사에서 자동으로 설정을 해주지만, 어떠한 이유로 이것을 다른 서비스로 변경할 수 있다.

<br>

## *DNS 원리*

DNS Server가 하는 일은 크게 두 가지가 있다. 하나는 서버로 사용할 컴퓨터가 자신의 이름과  IP를 제출하면 그것을 서버에 등록하는 것이고 다른 하나는  클라이언트로 사용되는 컴퓨터가 이름을 물어보면 응답해주는 것이다. 

우선 도메인의 이름은 다음과 같은 구조로 이루어져있다.

![image](https://user-images.githubusercontent.com/68289543/104831029-20af6080-58c8-11eb-9708-992fb1650ce9.png)

- 이 도메인에 있는 각각의 부분들은 **(sub, Second-level, Top-level, Root)** 이 각각의 부분들을 관리해주는 독자적인 서버 컴퓨터가 존재한다. 
- 도메인은 ".(dot)" 또는 Root라고 불리는 도메인 아래에 계층적인 구조로 구성되어 있다.

예시를 통해 도메인의 원리를 보면 다음과 같다.

![image](https://user-images.githubusercontent.com/68289543/104831472-8a316e00-58cc-11eb-9022-a2f67fc0c3f1.png)



1. 웹 브라우저에 `www.naver.com`을 입력하면 먼저 Local DNS에게 `"www.naver.com"`이라는 hostname에 대한 IP 주소를 요청한다.
2. Local DNS에 `"www.naver.com"`의 IP 주소가 있다면 Local DNS가 바로 PC에게 IP 주소를 주고 끝나지만 Local DNS에 `"www.naver.com"`의 IP 주소가 없다면 다음과 같이 진행한다.
3. Local DNS는 `"www.naver.com"`의 IP 주소를 찾아내기 위해 다른 DNS 서버들과 통신을 한다. Local DNS는 Root DNS 서버에게 `"www.naver.com"`의 IP 주소를 요청한다. (Local DNS는 반드시 Root DNS의 IP 주소를 알고있어야한다.) 이 Root DNS 서버는 전 세계에 13대 구축되어있다.
4. Root DNS 서버 `"www.naver.com"`의 IP 주소를 모르기 때문에 Root DNS 서버가 대신 "com 도메인"을 관리하는 Top-level의 IP 주소를 알려준다. 
5. 이제 Local DNS 서버는 "com 도메인"을 관리하는 Top-level DNS 서버에 `"www.naver.com"`의 IP 주소를 요청한다.
6. 그러면 Top-level DNS 서버는 "naver.com 도메인"을 관리하는 Second-level의 IP 주소를 알려준다.
7. "naver.com 도메인"을 관리 하는 Second-level의 DNS 서버에는 `"www.naver.com"`에 대한 IP 주소가 있으므로 IP 주소를 Local DNS 서버에게 응답해준다.



이와 같이 Local DNS 서버가 여러 DNS 서버를 차례대로 물어봐서 그 답을 찾는 과정을 **Recursive Query**라고 부른다.

<br>

<br>

<br>

___

참고 : [생활코딩](https://opentutorials.org/course/3276/20303), https://www.netmanias.com/ko/post/blog/5353/dns/dns-basic-operation
