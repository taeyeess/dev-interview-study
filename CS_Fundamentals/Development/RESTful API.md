           ### API란
API란 프로그램들이 서로 소통하는 방법이다. 즉, 코드들이 서로 소통하기 위하여 만들어진 것이 API이다.

- **API의 종류**
  - WEB API : 브라우저
  - 공공 API : 공공 데이터


### REST API와 RESTFUL
- **REST API**
  - Representational State Transfer 의 약자
  - 서버의 자원을 어떠한 방식으로 접근하도록 해야 구체적으로 명시한 것
  - 웹에 존재하는 모든 자원(이미지, 동영상, DB 자원)에 고유한 URI를 부여해 활용하는 것
  - 자원을 정의(HTTP URI)하고 자원에 대한 주소를 지정(HTTP Method)하는 방법론
  - HTTP 프로토콜을 그대로 사용하여 웹/모바일 개발에서 서버/클라이언트가 통신하기에 적합  
  

- **REST의 구성 요소**
  - 자원(Resource) : URI를 이용하여 표현
  - 행위(Verb): HTTP 메서드를 이용하여 표현
  - 표현(Representations)
  

- **RESTFUL이란?**
  - REST의 형식을 따르는 시스템을 의미한다.

### REST API 설계하기
사용하기 쉬운 API란 팀 멤버들과 유저가 쉽게 활용할 수 있도록 설계된 API를 의미한다.

좋은 API를 설계하는 방법에 대해 알아보자

API가 필요한 URL을 만들 때 삽입, 수정, 삭제 명령어를 다음과 같이 구성 할 수 있다.
```
1) /createBook  
2) /seeBooks  
3) /getBook/HarryPotter  
4) /deleteBook/HarryPotter  
5) /updateBook/HarryPotter  
6) /getTopRatedBook
```
[예시1]  

<예시1>의 URL은 여러개의 동사로 정의되었으며 명확한 패턴이 없다. 따라서 좋은 설계 방식이라고 할 수 없다.

이를 몇가지 과정을 거쳐 개선해보자  

**첫번째, URL에서 동사를 제거한다.**

1) /Book => 단수 제거
2) /Books  
3) /Book/HarryPotter  
4) /Book/HarryPotter  
5) /Book/HarryPotter  
6) /TopRatedBook  

예시1에서 동사를 없애면 URL에는 명사만 존재한다.
이때 명사는 2가지 방식으로 분류한다.

1) Books와 같은 **복수형 명사**.
2) 책 제목인 HarryPotter. 이때 책 제목은 DB에서 **고유 식별자**(Unique identifier)가 된다.

이때, 3-5가 같아지는 것을 알 수 있다. 데이터 가져오기, 삭제, 삽입 역할을 하던 URL이 동사 제거 후
그 형태가 같아졌다.

**두번째, Http Method를 사용한다.**   

즉, 명사만 남은 URL에서 데이터를 삽입, 갱신, 삭제하기 위하여 Http Method와 결합한다.  

> Http Method: GET,POST,PUT,DELETE

적용하면 다음과 같다  

1) 복수형 명사와 결합
- 데이터 삽입  

    - GET/Books

2) 고유 명사와 결합

- 데이터 갱신
  - POST/Books/HarryPotter

- 데이터 삭제
  - DELETE/Books/HarryPotter

응용하면 위의 형식을 계속 확장해 나갈 수 있다.  

만약, 책의 등장 인물을 알고 싶다면 **GET/Books/HarryPotter/character** 의 형식으로 요청 가능하다.

> 참고
> REST란 : https://hckcksrl.medium.com/rest%EB%9E%80-c602c3324196
> 노마드 코더: 

