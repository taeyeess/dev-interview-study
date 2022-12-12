## 인증 및 인가 방식

### Authentication & Authorization

|   인증 Authentication   |  인가 Authorization   |
| :----------: | :----------------: |
| 사용자가 누구인지 확인 | 사용자가 리소스에 접근하는 것에 대한 허락을 결정 |
| Login Form, <br>HTTP Authentication, <br> Custom auth. method | Access Control URLs, <br>Access Control List(ACLs) |

### 세션을 통한 인증

<img src="https://github.com/93jpark/dev-interview-study/blob/main/assets/images/backend/session.png" width="600" height="300">

1. 지정된 user의 id와 pw를 통해 로그인 요청
2. 서버는 request의 id/pw를 DB에 저장된 값과 비교하여 유효한지 확인
3. 유효한 로그인 정보의 경우, 세션DB에 회원 정보 세션(session id)생성
4. 생성된 유저의 session id를 서버로 전송
5. 로그인 요청에 대한 응답으로 session id 전송
6. 서버에 인증이 요구되는 api콜. 이때, 이전에 발급받은 session id를 쿠키에 담아 함께 전송
7. 쿠키에서 session id를 가져와 세션DB에서 조회하여 유효한 세션인지 확인
8. 유효하다면 서버에서 api콜에 대한 비즈니스 로직 수행
9. 로직 수행 결과에 대한 응답 전송

### 세션 방식의 특징

유효기간이 존재하는 세션을 통해서 회원에 대한 인증/인가를 함으로 보안 취약성을 막을 수 있다.

하지만, 세션을 저장하기 위한 DB가 따로 존재해야하며, 인증이 필요한 요청이 올때마다 세션DB에 접근해야하는 낭비가 발생한다.

### 토큰 방식

<img src="https://github.com/93jpark/dev-interview-study/blob/main/assets/images/backend/token.png" width="600" height="300">


1. 지정된 user의 id와 pw를 통해 로그인 요청
2. 서버는 request의 id/pw를 DB에 저장된 값과 비교하여 유효한지 확인
3. 유효한 로그인 정보의 경우, 유저의 정보를 포함하여 JWT 토큰을 발급
4. 로그인 요청에 대한 응답으로 쿠키에 발급한 토큰을 담아 응답 전송

5. 서버에 인증이 요구되는 api콜. 이때, 이전에 발급받은 Access Toekn을 HTTP Header의 Authorization에 담아 전송

6. 쿠키에서 Token을 가져와 유효한 토큰인지 검증

7. 유효하다면 서버에서 api콜에 대한 비즈니스 로직 수행

### 토큰 방식의 특징
- `AccessToken(AT)`과 `RefreshToken(RT)`를 사용한다. 이때, AT는 유효기간이 짧고 유저의 권한 정보 및 관련 정보를 포함한다. RT는 유저에 대한 최소한의 정보와 긴 유효기간을 가진다.

- RT를 통해 AT의 유효기간을 짧게 설정할 수 있다. (탈취방지)
- AT의 유효기간이 짧더라도 RT를 통해서 반복 로그인 없이 인증 유효기간을 길게 설정할 수 있다.


### 토큰 인증과 재발급

<img src="https://github.com/93jpark/dev-interview-study/blob/main/assets/images/backend/AT&RT.png" width="600" height="300">

AT가 만료된 경우, 서버는 토큰이 만료되었다는 응답을 전송한다. 프론트는 해당 응답을 받으면, 토큰을 갱신해달라는 요청을 RT와 함께 전송한다. 서버는 RT의 유효성을 검증한 후, AT&RT를 모두 재발급하여 전송한다. 프론트는 해당 토큰을 다시 저장하고, 처음의 요청을 재발급된 AT와 함께 다시 전송한다.

#### 언제/어떤 방식을 채용해야 하나?
서버가 다수 존재하는 어플리케이션 환경이라면, 세션을 사용하면 세션정보를 서버들이 공유해야함으로 부담이 생긴다. 또한, 세션DB에 대한 접근이 많아짐으로 동시성 이슈 및 DB 접근 리소스 낭비가 발생한다. 또한, 매 요청시 DB를 조회하는것을 토큰방식을 통해 피할 수 있음으로 정보/권한에 대한 과정에서 발생할 수 있는 병목현상을 피할 수 있다.

#### 토큰의 저장과 전송

- JWT는 유저의 브라우저 내 안전한 장소에 저장되어야 한다.

- `LocalStorage`이나 `SessionStorage`에 저장하게되면 페이지 내부의 모든 스크립트에서 엑세스할 수 있기에 XSS 공격대상이 되거나 외부 공격자가 토큰에 접근할 수 있게 된다.

- JWT는 HTTP요청으로만 서버에 전송되는 `HttpOnly쿠키` 내에 저장되어야 한다.

- HTTP request 전송 시 토큰을 담아서 보낼 땐, `HTTP Header의 Authorization`에 저장하여 전송한다.