TCP(Transmission Control Protocol: 전송 컨트롤 프로토콜)

TCP는 네트워크 계층 중 전송 계층에서 사용하는 프로토콜로, 장치들 사이에 논리적인 접속의 신뢰성을 보장하는 연결지향형 서비스이다.

애플리케이션에게 신뢰적이고 연결지향성 서비스를 제공하는 가상 회선 방식이다. 

일반적으로 TCP와 IP는 함께 사용되며 IP는 데이터를 메시지 형태(단위: segment)로 배달하고, TCP는 패킷의 추적 및 관리를 한다.

신뢰적인 전송을 보장하기에 handshaking(주고받기)하고 데이터의 흐름제어와 혼잡제어, 오류제어를 수행한다.

UDP보다 속도는 느리다.

데이터를 송신하는 곳과 수신하는 곳의 처리 속도를 조절하여 수신자의 buffer overflow(버퍼가 흘러 넘쳐 지정된 메모리 바깥쪽에 저장하는 것)를 방지한다.

파일전송에 주로 사용

정보의 소통량이 과다하면 패킷을 조금만 전송하여 혼잡 붕괴 현상이 일어나는 것을 막는다.

3-way handshaking과정을 통해 연결을 설정하고 4-way handshaking을 통해 해제한다.

높은 신뢰성을 보장한다.

전이중(Full-Duplex), 점대점(Point to Point) 방식.

전이중

전송이 양방향으로 동시에 일어날 수 있다.

점대점

각 연결이 정확히 2개의 종단점을 가지고 있다.

멀티캐스팅이나 브로드캐스팅을 지원하지 않는다.

연속성보다 신뢰성있는 전송이 중요할 때에 사용된다.


Client -> Server ​

상태

설명

CLOSED

연결 수립을 시작하기 전의 기본 상태 (포트가 닫힌 상태)

LISTEN

포트가 열린 상태로 연결 요청 대기 중

SYN-SENT

SYN 요청을 한 상태

SYN-RECEIVED

SYN(SYNcronize) 요청을 받고 상대방의 응답을 기다리는 중

ESTABLISEHD

포트 연결 상태, 서로 데이터를 교환할 수 있다.

Server -> Client

상태

설명

CLOSE

연결 수립을 시작하기 전의 기본 상태 (연결 없음)

ESTABLISHED

연결의 수립이 완료된 상태, 서로 데이터를 교환할 수 있다.

CLOSE-WAIT

상대방의 FIN(종료 요청)을 받은 상태. 상대방 FIN에 대한 ACK를 보내고 애플리케이션에 종료를 알린다.

LAST-ACK

CLOSE-WAIT 상태를 처리 후 자신의 FIN요청을 보낸 후 FIN에 대한 ACK를 기다리는 상태.

FIN-WAIT-1

자신이 보낸 첫 FIN에 대한 ACK를 기다리고 있다.

FIN-WAIT-2

자신이 보낸 첫 FIN에 대한 ACK를 받았고 상대방의 FIN을 기다린다.

CLOSING

상대방의 FIN에 ACK를 보냈지만 자신의 FIN에 대한 ACK를 못받은 상태

TIME-WAIT

모든 FIN에 대한 ACK를 받고 연결 종료가 완료된 상태. 새 연결과 겹치지 않도록 일정 시간 동안 기다린 후 CLOSED로 전이한다.

​

​

 TCP 3-way Handshake

TCP 3 Way Handshake는 TCP/IP 프로토콜을 이용해서 통신을 하는 응용 프로그램이 데이터를 전송하기 전 정확한 전송을 보장하기 위한 연결 확인 방식으로,  상대방 컴퓨터와 사전에 세션을 수립하는 3번의 과정을 의미한다.

• 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 실제 데이터 전달을 시작하기전에 한쪽이 다른 쪽이 준비되었다는 것을 알 수 있게 한다.


​

Client -> Server : SYN

Server -> Client : SYN + ACK

Client -> Server : ACK

​

​

TCP 3-way Handshake 과정


1

클라이언트는 서버에 접속을 요청하는 SYN 패킷을 보낸다. 이때 클라이언트는 이전의 connection으로부터 오는 패킷으로 인식할 수 있는 문제 발생 가능성을 줄이기 위해 SYN에 무작위의 Sequence Number를 보내고 SYN/ACK 응답을 기다리는SYN_SENT 상태가 되는 것이다.

 SYN 플래그 비트를 1로 설정한 세그먼트를 전송한다.

PORT 상태 - 서버: LISTEN, 클라이언트: CLOSED

 

2

서버는 SYN요청을 받고 클라이언트에게 요청을 수락한다는 ACK 와 SYN flag 가 설정된 패킷을 발송하고 클라이언트가 다시 ACK으로 응답하기를 기다린다. 이때 서버는 SYN_RECEIVED 상태가 된다.

SYN과 ACK 플래그 비트를 1로 설정한 세그먼트를 전송한다.

PORT 상태 - 서버: SYN_RCV, 클라이언트: CLOSED

 

3

클라이언트는 서버에게 ACK을 보내고 이후로부터는 연결이 이루어지고 데이터가 오가게 되는것이다. 이때의 서버 상태가 ESTABLISHED 이다.

만약 수신자가 데이터 유닛(segment)이 손상된것을 확인하면(Error Detection에 사용되는 transport layer의 checksum을 활용), 해당 segment를 없앤다. 그러면 서버는 PAR(Positive Acknowledgement with Re-transmission)이라고 하는 메커니즘을 통해 신뢰적인 통신을 제공하여 ack을 받을 때까지 데이터 유닛을 재전송한다.

PORT 상태 - 서버: ESTABLISHED, 클라이언트: ESTABLISHED

​

 TCP 4-way Handshake

3 way handshake와 반대로 가상 회선 연결을 해제할 때 주고 받는 확인작업이다. 이 역시 4번의 확인과정을 거친다고 하여 4 way handshake라고 부른다.

TCP 4-way Handshake 과정

​


​

1

클라이언트가 연결을 종료하겠다는 FIN(FINish)플래그를 전송한다.

서버가 FIN 플래그로 응답하기 전까지 연결을 계속 유지한다.

​

2

서버는 일단 확인메시지를 보내고 자신의 통신이 끝날때까지 기다리는데 이 상태가 TIME_WAIT(Client에서 뒤늦게 도착하여 패킷이 Drop되고 데이터는 유실될 경우에 대비한 잉여 패킷을 기다리는 과정)상태다. ACK 플래그 비트를 1로 설정한 세그먼트를 전송한다.

전송할 데이터가 남아 있으면 계속 전송한다. 

​

3

서버가 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN플래그를 전송한다.

 

4

클라이언트는 확인했다는 메시지를 보낸다.

​

​

3-Way Handshake와 4-Way Handshake

참고 TCP Header 안의 플래그 정보

TCP Header에는 CONTROL BIT(플래그 비트, 6bit)가 존재하며, 각각의 bit는 "URG-ACK-PSH-RST-SYN-FIN"의 의미를 가진다.

해당 위치의 bit가 1이면 해당 패킷이 어떠한 내용을 담고 있는 패킷인지를 나타낸다.

SYN(SYnchronize) "000010"

연결 설정

Sequence Number를 랜덤으로 설정하여 세션을 연결하는 데 사용하며, 초기에 Sequence Number를 전송한다.

ACK(Acknowledgement) "010000"

응답 확인

Acknowledgement Number 필드가 유효한지를 나타낸다.

SYN 세그먼트 전송 이후(TCP 연결 시작후) 모든 세그먼트의 ACK 비트는 1로 지정된다.

FIN(Finish) "000001"

연결 해제

세션 연결을 종료시킬 때 사용되며, 더 이상 전송할 데이터가 없음을 의미한다.

 

 

References

http://needjarvis.tistory.com/157

http://hyeonstorage.tistory.com/286

https://gmlwjd9405.github.io/2018/09/19/tcp-connection.html

[Network] TCP 3-way handshaking과 4-way handshaking - Heee's Development Blog (gmlwjd9405.github.io)

[네트워크] TCP 3-way & 4-way handshake란? — 조무래기 코딩 (tistory.com)

https://blog.naver.com/kenzo28/220238548338

https://ko.wikipedia.org/wiki/전송_계층

https://ko.wikipedia.org/wiki/OSI_모형

https://mangkyu.tistory.com/15

https://beenii.tistory.com/127

https://needjarvis.tistory.com/157

https://www.geeksforgeeks.org/tcp-3-way-handshake-process/

https://gyoogle.dev/blog/computer-science/network/TCP 3 way handshake & 4 way handshake.html

https://www.geeksforgeeks.org/tcp-connection-termination/

webstylez.egloos.com  

blazebyte.blogspot.kr 

[ 네트워크 쉽게 이해하기 22편 ] TCP 3 Way-Handshake & 4 Way-Handshake (tistory.com)

[네트워크] TCP/UDP와 3 -Way Handshake & 4 -Way Handshake (velog.io)