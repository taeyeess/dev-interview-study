# 네트워크

## HTTP 동작과정과 HTTP method, 상태코드

`HTTP`는 HTML 문서와 같은 자원을 가져오기 위해 사용되는 통신규약이다. 웹 브라우저(클라이언트)와 서버 사이의 HTTP 통신을 통해 사용자는 웹 문서에 접근/이용할 수 있다.

클라이언트와 서버는 개별적인 메세지(데이터 스트림)를 주고받으며 통신한다. 웹 브라우저(클라이언트)가 보내는 메세지를 `요청(request)`라고 하며, 이에 반응하여 서버가 전송하는 메세지를 `응답(response)`라고 한다. 

HTTP는 확장가능한 프로토콜이다. 이 확장가능성(extensibility)을 통해서 응용 계층 프로토콜(TCP 또는 TLS-encryped TCP연결)과 같은 다른 전송 프로토콜 또한 이용이 가능하다. 또한, 하이퍼텍스트 문서 뿐 만 아니라 이미지와 비디오 같은 컨텐츠도 서버와의 통신에서 송수신이 가능하다.

> `Tranport Layer Security` : Secure Socket Layer(SSL)으로도 알려진 이 프로토콜은 이메일, 웹 브라우징, 메세징 등 다른 프로토콜에서의 데이터 도청 및 변경으로 부터 보안을 약속한다.

> `Transmission Control Protocol` : TCP는 전송 제어 프로토콜로써, 두 host가 데이터 전송함에 있어 무결성을 보장한다.

### 웹 동작과정

<img src="https://github.com/93jpark/dev-interview-study/assets/image/network/network_http_workflow.jpeg" width="600" height="400">

##### 1. URL 검색
유저가 웹 브라우저의 검색창에 URL주소를 입력한다.

<img src="https://github.com/93jpark/dev-interview-study/assets/image/network/url_format.url" width="600" height="140">

URL은 위와 같은 형식으로 구성된다.
> 프로토콜 별 포트번호

| 프로토콜 | 포트번호 | 프로토콜 | 포트번호  |
| :-----: | :---: | :---: | :---:   |
| DHCP    | 67    | Telent| 23      |
| NBNS    | 137   | SMPT  | 25      |
| DNS     | 53    | HTTP  | 80      |
| SNTP    | 123   | HTTPS | 443     |
| SNMP    | 161   | FTP   | 21      |

<br>


##### 2. DNS서버와 IP주소

DNS서버에는 사용자가 적은 URL주소의 도메인 네임에 해당하는 IP 주소가 등록된다.

> dig 명령어를 통해 알아본 github.com의 DNS Lookup 결과
<img src="https://github.com/93jpark/dev-interview-study/assets/image/network/dig_dns_lookup.url" width="250" height="300">
github.com의 IP주소는 '20.200.245.247'으로 확인된다.

클라이언트는 DNS서버에 사용자가 요청한 도메인 주소에 대한 물리주소(IP주소)를 가져온다.

<br>

##### 3. 클라이언트-서버 TCP 연결

HTTP 요청 메시지를 전송하기 위해 클라이언트-서버 간 통신 채널을 만든다.
> 3-way-handshake
> 1. Clinet -> Server : 접속을 요청하는 SYN패킷 전송
> 2. Server -> Client : 접속 요청을 수락 후 접속 요청하는 쪽에 포트를 열어달라는 SYN, ACK 패킷 전송
> 3. Client -> Server : 수신이 정상적으로 이루어졌다는 ACK패킷 전송


<br>

##### 4. 클라이언트의 HTTP요청 메시지

클라이언트는 Header와 Body로 구성된 HTTP 요청 메시지를 전송한다.
`HTTP 메세지`는 ASCII 형식으로 인코딩된 텍스트 데이터이며, 클라이언트-서버 사이에서 어떻게 데이터를 교환할지 명세한다. 

###### HTTP Request(요청)

```
GET /hello.htm HTTP/1.1
User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
Host: www.tutorialspoint.com
Accept-Language: en-us
Accept-Encoding: gzip, deflate
Connection: Keep-Alive
```

`HTTP request`는 클라이언트에서 서버로 전송되는 메세지로, 어떠한 action을 요청하는지 명시한다. 
첫줄에는 HTTP method, 요청 타깃, HTTP 버전으로 구성된다.
- HTTP method - GET,PUT과 같은 서버를 통해 수행할 동작이 명시된다.
- Request target - HTTP method에 따라 URI 또는 '?'으로 시작하는 QueryString이 명시된다.
- HTTP version - HTTP 버전에 따라 나머지 부분의 구조가 달라진다.

<br>

###### HTTP Headers

```
Get /test/test.htm HTTP/1.1
Accept: */*
Accept-Language: ko
Accept-Encoding: gzip, deflate
If-Modified-Since: Fri, 21 Jul 2006 05:31:13 GMT
If-None-Match: "734237e186acc61:a1b"
User-Agent: Mozilla/4.0(compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322; InfoPath.1)
Host: localhost
Connection: Keep-Alive

HTTP/1.1 200 OK
Server: Microsoft-IIS/5.1
X-Powered-By: ASP.NET
Date: Fri, 21 Jul 2006 05:32:01 GMT
Content-Type: text/html
Accept-Ranges: bytes
Last-Modified: Fri, 21 Jul 2006 05:31:52 GMT
ETag: "689cb7f885acc61:a1b"
Content-Length: 101
```

`HTTP header`는 key:value형식으로 구성되며, 아래의 header들로 나뉘어진다.

- <strong>General Header</strong>
    요청 및 응답 메세지 모두에서 사용되는 일반 목적의 헤더 항목
    - Date, Connection, Cache-control, Pragma, Trailer

- <strong>Entity Header</strong>
    요청/응답 메세지에서 사용가능한 엔티티(콘텐츠, 본문, 리소스 등)에 대한 설명
    | 이름 | 설명 | 예시 |
    | :-----: | :---: | :--- |
    | Content-Type    | 해당 개체에 포함되는 미디어 타입 정보 | Content-Type: text/html; charset-latin-1 |
    | Content-Language    | 해당 개체와 호환되는 사용자 언어 | - |
    | Content-Encoding    | 해당 개체 데이터의 압축 방식    | Content-Encoding: gzip, defalte |
    | Content-Length      | 해당 개체의 바이트 길이        | - |
    | Content-Location    | 해당 개체의 실제 위치         | - |
    | Content-Disposition | 응답 Body를 브라우저에 표시하는 방법 | Content-Disposition : inline<br>Content-Disposition : attachment; filename='file_name.scv' |
    | Content-Security-Policy    | 다른 외부 파일을 로드할 경우, 차단할 소스와 불러올 소스 명식 | Content-Security-Policy: default-src https: |
    | Location            | 리소스가 리다이렉트된 때에 이동된 주소 | HTTP/1.1 302 Found Location: /|
    | Last-Modified       | 리소스를 마지막으로 갱신한 일시       | - |
    | Transfer-Encoding   | 동적으로 생성되어 Body의 길이를 모르는 경우 나누어 전송 | - |
    

-  <strong>Request Header</strong>
    HTTP 요청 메시지에서만 나타나며, 클라이언트와 관련된 데이터를 담고 있다.
    | 이름 | 설명 | 예시 |
    | :-----: | :---: | :--- |
    | Host    | 요청하는 호스트에 대한 이름 및 포트번호 | - |
    | User-Agent    | 클라이언트 소프트웨어 정보 | - |
    | From    | 클라이언트 사용자 메일 주소    | Content-Encoding: gzip, defalte |
    | Cookie      | 서버에 의해 Set-Cookie로 클라이언트에 설정된 쿠키 정보 | - |
    | Referer    | 바로 직전에 머물렀던 웹 링크 주소 | - |
    | If-Modified-since | 제시한 일시 이후 변경된 리소스를 취득 요청 | - |
    | Authorization | 인증토큰(JWT)을 서버로 보낼때 사용하는 헤더 | 토큰종류 + 실제 토큰문자 |
    | Origin | 서버로 POST요청 보낼때, 요청이 어느 주소에서 시작되었는지 명시 | - |
    



> Reference: 
https://gmlwjd9405.github.io/2019/01/28/http-header-types.html
https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages

<br>

##### 5. 클라이언트-서버 TCP 연결 해제


기존에 생성된 클라이언트-서버 통신 채널의 연결을 해제한다.

> 4-way-handshake
> 1. Clinet -> Server : 연결을 해제하기 위한 FIN패킷 전송
> 2. Server -> Client : 연결 종료를 확인했다는 ACK패킷 전송, 통신이 종료될때까지 대기
> 3. Server -> Client : 통신이 종료되었을 때, FIN패킷 전송
> 4. Client -> Server : 통신 해제를 확인했다는 ACK패킷 전송

<br>

##### 6. 서버의 응답 처리

HTTP Request 메시지에 따라 서버에서 필요한 비즈니스 로직을 수행하고 데이터를 가공하는 작업을 수행

<br>

##### 7. 클라이언트-서버 TCP 연결

앞서 HTTP Request를 전송하기 위해 만들었던 통신채널을 다시 클라이언트-서버 연결

##### 8. 서버의 HTTP응답 메시지 

HTTP Request 메시지에 따른 Response 메세지를 리소스/응답코드를 함께 전송

###### HTTP Response
```
HTTP/1.1 200 OK
Date: Mon, 27 Jul 2009 12:28:53 GMT
Server: Apache/2.2.14 (Win32)
Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
Content-Length: 88
Content-Type: text/html
Connection: Closed
```

`HTTP Response`메세지는 첫줄에 프로토콜의 버전, 상태코드, 상태 메세지로 구성된다. Header는 Request와 동일한 구조를 지니며, Body는 상태코드에 따라 달라진다.

<br>

##### 9. 클라이언트-서버 TCP 연결 해제

5의 TCP 연결 해제 작업을 반복한다. 

<br>

##### 10. 클라이언트의 응답메세지 출력

웹 브라우저를 통해 응답 받은 메시지의 Body 데이터를 나타낸다.

<br>



### HTTP Method

웹 브라우저에서 URL을 입력하면 해당 URL에 위치한 서버와 통신을 하게 된다. 브라우저는 서버로부터 웹문서를 받아서 렌더링하여 사용자에게 보여준다. 이 때, GET/POST와 같은 메소드를 통해 데이터를 수신하거나 입력한다. 

`HTTP Method`는 ..

### HTTP 상태코드

`HTTP 상태코드`는 ..

> reference : https://mangchhe.github.io/web/2021/02/19/HttpActionProcess/