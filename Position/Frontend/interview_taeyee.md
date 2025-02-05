## 프론트엔드 면접 예상 질문 리스트

중요도 <span style="color:#FEDA3E">★★★★★</span>


### 브라우저 렌더링 과정 (홈페이지가 사용자에게 보여지는 순서)

##### 1. DOM, CSSOM을 생성
- 서버로 부터 받은 HTML, CSS을 다운받는다. (HTML은 DOM으로, CSS는 CSSOM으로 만들어진다.)
- HTML이 파싱된다. 
- DOM Tree와 CSSOM Tree가 만들어진다. 

##### 2.   Style (Render Tree를 생성)
- DOM Tree와 CSSOM Tree를 이용하여 Render Tree를 생성한다. 
- Render Tree에는 스타일 정보가 설정되어 있고, 실제 화면에 표현되는 노드들로 구성된다. 

##### 3.   Layout 단계 (render tree 배치)
- 브라우저의 뷰포트(Viewport)내에서 각 노드들의 정확한 위치와 크기를 계산한다. 
- 생성된 render tree노드들이 가지고 있는 스타일과 속성에 따라서 브라우저 화면의 어느 위치에 어떤 크기로 출력될 지 계산하는 단계이다.
- 레이아웃 단계에서 %, vh, vw와 같이 상대적인 위치, 크기의 속성은 실제화면에 (viewport) 그려지는 픽셀 단위로 변환된다.

#### 4.   Paint (render tree 그리기)
- 레이아웃 계산이 완료되면 요소들을 실제화면에 그리게 된다.
- 처리해야하는 스타일이 복잡할수록 paint단계에 소요되는 시간이 길다. 

> `Reflow` : Layout 이후 과정을 다시 수행. 레이아웃 계산을 다시하는 것
> `Repaint` : 재결합된 렌더트리를 기반으로 다시 페인트 하는 것

 ‣ HTML 문서가파싱되어 DOM을 생성할 때 css를 로드하는 link혹은 style태그를 만나면 DOM생성을 중지한다. 
‣ 만약 script태그를 만나면, css와 동일하게 JS코드를 실행하기 위해 파싱을 중단한다. 
- async, defer를 이용해 해결

‣ 이후 JS엔진을 실행하고 JS코드를 파싱한다. 
자바스크립트가 DOM, CSSOM을 변경하는 경우 리렌더링을 하게 된다. 

### 브라우저의 동작원리? 주소창에 www.google.com을 입력하면 일어나는 일.

#### 브라우저의 동작원리
- 브라우저의 주요 기능은 사용자가 자원을 서버에 요청하고, 요청한 자원 서버에서 응답하여 브라우저에 제공하여 표시하는 것이다.
- 웹 브라우저에 URL을 입력하면 웹 서버라 불리는 프로그램이 웹 브라우저에 웹 페이지를 제공한다.
- 웹 브라우저가 웹 서버에 연결하려면, 웹 서버가 실행중인 컴퓨터의 주소를 알아야 하는데 이 주소를 IP주소 라고 한다.
- 각 컴퓨터는 IP주소를 가지고 있고, 이 IP주소는 193.394.0.1과 같은 숫자들로 구성되어 있어 그 대신 기억하기 좋은 도메인 이름을 사용한다.
- 웹 브라우저와 웹 서버는 IP주소를 이용하여 연결하기 때문에 도메인 이름을 IP 주소로 변환할 필요가 있는데, 이 때 사용하는 것이 DNS(Domain Name Server)이다. 
- 웹 브라우저에서 URL을 입력하면 웹 브라우저는 도메인 이름에 해당하는 IP주소를 찾기 위해 DNS에 요청을 보내고, DNS는 IP주소를 응답으로 제공한다.   
- DNS로 부터 받은 IP주소를 통해 웹 서버에 연결한 뒤 URL에 해당하는 웹 페이지를 요청하고, 웹 페이지를 응답받는다.

#### 주소창에 www.google.com을 입력하면 일어나는 일
	Step 1. 주소창에 입력한 텍스트 정보 확인
		- 대부분의 인터넷 브라우저는 자사의 주소창을 검색창과 동일하게 사용하기 때문에,
		   사용자가 주소창에 입력한 것이 ‘검색어’인지 ‘URL’인지 확인하고
		   ‘검색어’ -> 검색 엔진의 URL에 검색어를 포함한 주소로 페이지 이동
		   ‘URL’ -> 브라우저 엔진에서 (네트워크 스레드를 통해) 네트워크 호출을 수행한다.
	Step 2. 네트워크 호출 (브라우저의 동작원리)
		- 웹 브라우저가 웹 서버와의 네트워크 통신을 통해 데이터들을 가져오기 위해 호출 		
		- 웹 브라우저 (클라이언트)는 TCP소켓을 열고 이를 통해 서버에 데이터를 요청하는 
		  HTTP Request를 보낸다. 
		- HTTP Request를 받은 서버는 클라이언트가 요청한 문서를 찾아 일고 이를 
		  byte형태로 변환한 후, 클라이언트로 HTTP Reply(HTTP Response)를 보낸다.
	Step 3. 렌더링 작업 (브라우저 렌더링)

### 웹사이트 성능 최적화에는 어떤 방법이 있는지

- Style은 상단, js(script)는 하단에서 불러온다
- 웹팩 (Webapack) 사용
- JS 공백 줄이기
- Html 작성시 불필요한 div제거
- CSS 최적화
- 리플로우, 리페인트를 고려한 스타일 작성
- 사용하지 않는 css제거
- 이미지 최적화
- Picture, img 지연로딩 활용하기
- 스프라이트 이미지 사용
- 핵심적인 웹 지표 (LCP, FID, CLS) 최적화
- 애니메이션은 js보다는 css로 사용한다
- SEO (검색엔진최적화)
- CDN 사용 (서버를 하나만 두는 것이 아닌 각 지역에 분산)
- 라이브러리 의존도 낮추기
…


### 브라우저 저장소의 차이점 (localStorage, SessionStorage, Cookie)

- 브라우저 저장소의 종류는 Cookie, WebStorage 두가지로 나뉘고 WebStorage는 LocalStorage와 SessionStorage로 이루어져 있다. 
- WebStorage는 Html5에 포함되어 있는 스펙으로 웹의 데이터를 클라이언트에 저장할 수 있는 새로운 자료구조이다. 기존의 저장소로 사용되었던 Cookie의 몇가지 단점을 개선하기 위해 만들어짐.
- WebStorage는 key-value쌍의 구조로 데이터를 저장하고 key를 기반으로 데이터를 조회할 수 있다. 
- Web storage는 용량의 제한이 cookie보다 크다. 
- 웹사이트에서 cookie를 설정하면 이후 모든 요청은 쿠키정보를 포함하여 서버로 전송된다. 이는 불필요한 트래픽을 발생시킨다. 반대로 web storage는 데이터가 클라이언트단에 저장만 되고 서버로의 전송은 이루어지지 않는다. 

#### LocalStrorage
- 로컬 스토리지는 저장한 데이터를 지우지 않는 이상 영구적으로 보관이 가능하다. 
	 (도메인마다 별도로 로컬 스토리지가 생성됨. 도메인이 같으면 공유가 가능하다.)
- 사용예시: 자동 로그인
#### SessionStrorage
- 세션 종료 시 (브라우저를 닫을 경우) 클라이언트에 대한 정보가 삭제된다.
	 (도메인이 같아도 브라우저가 다르거나, 탭이 다르면 다른 저장소이다. 즉 서로 침범할 수 없다. )      
- 사용예시: 입력 폼 정보, 비로그인 장바구니     
#### Cookie
- 웹 사이트에서 쿠키를 설정하면 모든 웹 요청에는 쿠키 정보가 포함된다. => 서버 부담 증가
- 사용예시: 팝업 창 



### Rest API, Restful API

    REST API를 제공하는 웹사이트를 RESTful 하다고 할 수 있다. 
REST란 HTTP URI를 통해 자원을 명시하고 HTTP메소드(POST, GET, PUT, DELETE)를 통해 
해당 자원(URI)에 대한 CRUD operation을 적용하는 것이다. 
URI란 웹상의 자료의 id, URI는 인터넷 자원을 나타내는 고유 식별자이고 
클라이언트는 이 자원에 요청을 보낸다.
REST API 메세지 만으로 그 요청의 목적을 쉽게 알 수 있다. (URI는 정보의 자원을 표현해야함)
HTTP와 URI 모두 표준이기에 어디서든 동일하게 작동하는 것을 보장할 수 있다.
클라이언트는 유저와 관련된 처리를 요청하고 서버는 REST API로 응답을 제공함으로서, 
역할을 확실히 구분하여 서로간의 의존성을 줄이는 구조를 구성할 수 있다. 

#### REST API 설계 가이드
    1. 리소스에 대한 행위는 HTTP 메소드(POST, GET, PUT, DELETE)로 표현해야 한다. 
    2. / 는 계층 관계를 나타낼 때 사용한다.
    3. URI의 마지막 문자에는 /를 사용하지 않는다.
    4. URI에 _ 는 사용하지 않는다.
    5. URI는 영어 대문자보다 소문자를 사용하며, 긴 단어는 잘 사용하지 않는다.
    6. URI에 파일의 확장자를 포함하지 않는다. 


