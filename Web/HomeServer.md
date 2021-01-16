# Home Server

인터넷에 연결되어 있는 모든 컴퓨터들은 통신을 위해서 자신만의 IP 주소를 가지고있어야 한다. 하지만 IPv4 체계로는 많이 부족하다. 그래서 등장한 것이 IPv6지만 체계를 완전히 바꾸는 것은 비용이 막대하기 때문에 우선 IPv4 체계의 주소를 아껴써야 한다. 그래서 등장한 것이 공유기이다.

<br>

## *공유기(Router)*

**공인 IP 주소(Public IP Address)** 는 인터넷을 사용하기 위해 인터넷에 가입해서 부여받는 IP 주소를 말하고, **사설 IP 주소(Private IP Address)** 는 공유기가 하나의 공인 IP 주소를 가지고 만들어 낸 사설 네트워크에서 각 장치에게 부여하는 IP 주소를 말한다. 공인 IP 주소는 전세계의 장치들이 서로 통신하기 위해 사용하는 주소이고 사설 IP 주소는 해당 사설 네트워크 내에 존재하는 장치들끼리만 유효한 주소이다. 그래서 사설 IP 주소는 동일한 사설 네트워크 내에서는 중복되면 안 되지만, 서로 다른 사설 네트워크에 존재하는 장치들의 사설 IP 주소는 같아도 된다.

공유기에는 WAN 포트, LAN 포트가 있다. **WAN(Wide Area Network)** 은 전세계의 장치들이 서로 통신하기 위한 거대한 규모의 네트워크인 인터넷을 의미한다. 따라서 공유기를 이용하려면 집으로 들어오는 인터넷을 유선으로 WAN 포트에 연결해야 하며, 인터넷을 이용하려는 각 장치들은 공유기에 유선(LAN 포트) 또는 무선(공유기의 안테나)으로 연결해야 한다.

공유기는 자신을 포함하여 연결된 각 장치들에게 사설 IP 주소를 부여함으로써 사설 네트워크를 형성한다. 공유기 자체에 부여되는 사설 IP 주소를 **게이트웨이 주소(Gateway Address)** 혹은 **라우터 주소(Router Address)** 라고 부르며, 이 주소에 접속하면 해당 공유기의 설정을 확인하거나 바꾸는 것이 가능하다.

아래 범위에 있는 IP 주소는 사설 IP주소로만 사용한다고 전세계적으로 약속 되어 있다. 그렇지 않은 주소는 공인 IP 주소이다.

| 주소 범위                     | 주소 개수    | 특징                   |
| ----------------------------- | ------------ | ---------------------- |
| 10.0.0.0 ~ 10.255.255.255     | 16,777,216개 | 큰 규모의 LAN에 사용   |
| 172.16.0.0 ~ 172.31.255.255   | 1,048,576개  | 중간 규모의 LAN에 사용 |
| 192.168.0.0 ~ 192.168.255.255 | 65,536개     | 작은 규모의 LAN에 사용 |

<br>

## *NAT (Network Address Translation)*

**NAT(Network Address Translation)** 는 공유기에 연결된 각 장치들이 외부 네트워크에 있는 다른 장치들과 통신하도록 해준다. 만약 사설 IP 주소가 192.168.02인 장치 A가 페이스북에 접속하려는 상황을 가정해보자면 다음과 같은 과정이 진행된다.

1. 장치 A가 공유기에게 페이스북에 접속하고 싶음을 알린다.

2. **공유기는 192.168.0.2에 해당하는 장치가 페이스북에 접속하려 한다는 정보를 공유기 내부에 기록한다.**

3. **송신자 IP주소를 공인 IP 주소로 바꿔서 페이스북에 접속을 시도한다.**

4. 페이스북 서버는 공유기에게 응답한다.

   . . . 

여기서 2,3 과정에 해당하는 것이 NAT 기술이다. 사설 네트워크에 존재하는 특정 장치가 외부 네트워크의 장치와 통신하기 위해서는 공유기를 반드시 매개해야 하는데, 그 때 공유기가 중간에서 수행하는 역할이 바로 NAT 기술인 것이다.

<br>

## *포트(Port), 포트 포워딩(Port Forwarding)*

한 개의 컴퓨터에 부여된 공인 IP의 주소는 한 개지만, 컴퓨터는 여러 서버를 운영할 수 있다. 이때 필요한 것이 바로 **포트(Port)** 이다. 

**포트는 해당 컴퓨터의 어떤 서버에 접속할지를 명시해주는 기능을 수행** 한다. 포트는 총 65,536개 까지 명시할 수 있다. 이 중 0부터 1023까지는 이미 상용화된 프로토콜을 위해 예약이 되어 있는 Well-known 포트로, 우리가 함부로 사용할 수 없는 포트이다. 예를들어 HTTP 프로토콜의 경우에는 80번으로 약속이 되어 있다. 그래서 브라우저를 통해 웹 서버에 접속할 때는 기본적으로 80번 포트에 접속하는 것이 된다. 직접 지정해서 사용하고 싶은 경우에는 1024번 이상의 포트를 사용한다. 또 다른 웹 서버를 열고 싶은 경우에는 8000번이나 8080번을 사용하는 것이 관습이다. 

**포트 포워딩(Port Frowarding)** 은 만약 사설 네트워크 내에 장치가 A, B, C 세 개가 존재하고 C에서 80번 포트로 열려 있는 웹 서버에 외부 장치가 접속하고 싶을 때 필요한 기능이다. 공유기 자체도 자신이 형성한 사설 네트워크 내에서 하나의 사설 IP 주소를 가지고 있다. 우리는 그 주소에 접속함으로써 해당 공유기의 설정을 확인하거나 바꿀 수 있다. 포트 포워딩 관련 설정도 그 곳에서 가능한데, 포트 포워딩은 외부 포트, 내부 IP, 내부 포트를 지정해줌으로써 설정이 가능하다. 즉 외부에서 어떤 포트로 접속했을 때 사설 네트워크 내 어떤 장치의 어떤 포트로 접속을 연결해줄지 설정해주면 된다.

<br>

## *유동/ 고정 IP 주소 (Dynamic/Static IP Address)*

공인 IP주소는 대부분 고정적이지 않다. 인터넷에 가입하여 받은 공인 IP 주소를 부여받은 컴퓨터가 오랜 시간 꺼져 있으면, 지금 새로 인터넷에 가입하는 사람에게 그 주소를 부여해줄 수도 있기 때문이다. 그러다가 컴퓨터가 다시 켜지면 IST(Internet Service Provider)는 새로운 공인 IP 주소를 부여해준다. 이처럼 고정적이지 않은 IP 주소를 **유동 IP 주소(Dynamic IP Address)** 라고 부르고, 인터넷 가입시 추가 금액을 지불하면 변하지 않은 공인 IP 주소를 부여받을 수 있는데, 이를 **고정 IP 주소(Static IP Address)** 라고 한다.

<br>

## *DHCP(Dynamic Host Configuration Protocol)*

공유기와 연결된 각 장치들은 자신이 사용할 사설 IP 주소를 직접 설정하는 것이 가능하지만, 관련된 어려운 지식들을 많이 알고있어야 하므로 쉽지 않다. 그래서 대부분의 경우 공유기가 **DHCP(Dynamic Host Configuration Protocol)** 라는 원리를 통해 각 장치에게 자동적으로 사설 IP 주소를 부여하게 된다. DHCP의 동작 원리는 다음과 같다.

장치 A가 공유기에 연결되는 순간, 다음과 같은 과정이 진행되어 공유기로부터 사설 IP 주소를 할당 받는다. 참고로 MAC 주소란 각 장치의 고유한 제조 번호로, 전세계의 모든 장치들은 각자 자신만의 고유한 MAC 주소를 가지고 있다. 또한 공유기와 장치 간 DHCP 통신을 위해서, 기본적으로 공유기에는 DHCP 서버가 깔려 있고 장치에는 DHCP 클라이언트가 깔려있다.

1. 장치 A는 공유기의 DHCP 서버에 자신의 MAC 주소를 전달하며 사설 IP 할당을 요청한다.
2. 현재 연결된 다른 장치들의 사설 IP 주소와 겹치지 않게 사설 IP 주소를 장치 A에 일정 시간 부여한다.
3. 장치 A에 해당 사설 IP 주소를 일정 시간만큼 부여했다는 정보를 내부에 기록한다.

<br>

<br>

___

참고 : https://it-eldorado.tistory.com/22, [생활코딩](https://opentutorials.org/course/3265/20039)
