## 하이퍼텍스트 시스템의 구성
- 하이퍼텍스트 시스템은 4가지 블록으로 구성된다.
- HTML, HTTP, 문서 실행기 (클라이언트, 브라우저 등 유저가 문서를 읽을 수 있도록 하기 위한 도구), httpd 초기 버전
- httpd는 서버에서 HTTP 요청에 대해 문서를 내보낸다.

## HTTP/0.9
- 원-라인 프로토콜 : 한 줄의 문서로 요청을 전달한다. `GET /mypage.html`로 보면

#### 요청
```
GET /mypage.html
```
- 요청이 단일 라인으로 표현되기 때문에 '원-라인 프로토콜'이라고 불린다.

#### 응답
```
<HTML>
A very simple HTML page
</HTML>
```
- 초기에는 HTTP 헤더 없이 HTML 파일만 전송하는 방식이었다. 추후 헤더가 추가되며 응답에 메타 데이터를 추가할 수 있게 되었다.


## HTTP/1.0
### 버전 정보 추가
- HTTP 버전에 따라서 HTTP 프로토콜의 해석/처리를 달리하기 위해서 버전 정보가 추가되었다.
```
GET /mypage.html HTTP/1.0
```

### 상태 코드 추가
- 응답의 시작 부분에 상태코드가 추가되어 상태코드에 따른 처리를 달리할 수 있도록 만들었다.
- (예를 들어 브라우저는 이 정보를 토대로 성공 응답 받은 정보를 캐싱 처리하도록 하고 있다.)
```
GET /mypage.html HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

200 OK
```
- `200`은 상태코드로 이 코드를 통해서 응답 상태를 파악한다.
- `OK`는 상태 메시지. HTTP 프로토콜이 `OK`로 성공과 실패를 판단하는 정보는 아니다.

### 헤더의 추가
- 요청과 응답에 헤더 정보가 추가되었다.
- 헤더에 정보를 추가할 수 있어 프로토콜을 유연하고 확장가능하도록 하였다.
- 헤더 설정에 따라 HTML 문서 이외의 다른 문서들도 다운로드 할 수 있게 하였다. (문서의 유형을 설정할 때는 Content-Type 키를 사용한다.)
```
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

200 OK
Date: Tue, 15 Nov 1994 08:12:31 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/html
```
- `key :` 형식으로 되어 있는 것이 헤더

## HTTP/1.1



## Reference
- https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/Evolution_of_HTTP
