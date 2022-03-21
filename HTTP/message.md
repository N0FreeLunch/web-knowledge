## 메시지란?
- 서버와 클라이언트 간에 데이터가 교환되는 방식

### 요청
- 클라이언트가 서버로 전달해서 서버의 액션이 일어나게끔 하는 메시지이다.

### 응답
- 요청에 대한 서버의 답변이다.

## HTTP 메시지의 구성
- ASCII로 인코딩되어 있다.
- 텍스트 정보이다.
- 여러 줄로 되어 있다.

### 공개적 전달
- HTTP 프로토콜 초기 버전, HTTP/1.1
- 메시지를 사람이 읽고 해석할 수 있었다.

### 비공개적 전달
- HTTP/2
- 성능 최적화를 위해 사람이 읽고 해석하기 어려운 방식으로 바뀌었다.

## HTTP 메시지의 사용
- 직접 HTTP 메시지 텍스트를 작성하지 않는다.
- 소프트웨어, 브라우저, 프록시, 또는 웹 서버가 HTTP 메시지를 작성한다.

## HTTP/2

### 이진 프레이밍 메커니즘

## HTTP 문법해석
- 빈 줄 위로는 헤더(header), 빈 줄 밑으로는 바디(body)

### 응답과 요청의 예
#### 요청
```
POST / HTTP/1.1
Host: localhost:8000
User-Agent: Mozilla/5.0 (Macintosh;... )... Firefox/51.0
Accept:	text/html, application/xhtml+xml,..., */*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: qzip, deflate
Connection: keep-alive
Upgrade-Insecure-Requests: 1
Content-Type: multipart/form-data; boundary=-12656974
Content-Length: 345

-12656974
(more data)
```

#### 응답
```
http/1.1 403 Forbidden
Server: Apache
Content-Type: text/html; charset=iso-8859-l
Date: Wed, 10 Aug 2016 09:23:25 GMT
Keep-Alive: timeout=5, max=1000
Connection: Keep-Alive
Age: 3464
Date: Wed, 10 Aug 2016 09:46:25 GMT
X-Cache-Info: caching
Content-Length: 220

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML
2.0//EN">
(more data)
```

### 시작줄 (start-line)
#### 요청
- 항상 한 줄로 끝나는 부분으로 HTTP 전송에 필요한 가장 핵심적인 내용을 담고 있다.
```
POST / HTTP/1.1
```
- 실행 되어야 할 요청으로 **메소드, 경로, 프로토콜** 정보를 요구한다.

#### 응답
```
http/1.1 403 Forbidden
```
- 요청에 대한 응답으로 **프로토콜, 스테이터스(요청의 성공과 실패), 스테이터스 메시지**으로 구성된다.

### 헤더세트
#### 요청
```
Host: localhost:8000
User-Agent: Mozilla/5.0 (Macintosh;... )... Firefox/51.0
Accept: text/html, application/xhtml+xml,..., */*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: qzip, deflate
Connection: keep-alive
Upgrade-Insecure-Requests: 1
Content-Type: multipart/form-data; boundary=-12656974
Content-Length: 345
```

#### 응답
```
Server: Apache
Content-Type: text/html; charset=iso-8859-l
Date: Wed, 10 Aug 2016 09:23:25 GMT
Keep-Alive: timeout=5, max=1000
Connection: Keep-Alive
Age: 3464
Date: Wed, 10 Aug 2016 09:46:25 GMT
X-Cache-Info: caching
Content-Length: 220
```

### 빈 줄 (blank line)
- 메타 데이터 전송이 완료 되었음을 나타내는 구문이다.

#### 요청
```
Content-Length: 345

-12656974
```

#### 응답
```
Content-Length: 220

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML
```

### 본문
#### 요청
```
-12656974
(more data)
```
- HTML 폼 콘텐츠 등 요청과 관련된 추가적인 내용이 들어간다.

#### 응답
```
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML
2.0//EN">
(more data)
```
- 보통 HTML문서와 같은 document를 반환한다. 


## 요청 HTTP 메시지 상세
### 시작줄
#### HTTP 메소드
- 서버가 수행해야 할 동작을 정의함
- GET : 리소스를 클라이언트로 가져와 달라는 것을 의미
- POST : 데이터가 서버로 들어가야 함을 의미 (클라이언트로 꼭 데이터를 가져오지 않아도 됨)

#### 경로
-  URL, 프로토콜, 포트, 도메인의 절대 경로 등을 지정할 수 있다.

#### 경로 형식
**origin 형식**
- 가장 일반적인 형식
- `?`와 쿼리 문자열이 붙는 절대 경로 
- GET, POST, HEAD, OPTIONS 메서드와 함께 사용
```
POST / HTTP 1.1
```
```
GET /background.png HTTP/1.0
```
```
HEAD /test.html?query=alibaba HTTP/1.1
```
```
OPTIONS /anypage.html HTTP/1.0
```
**absolute 형식**
- 완전한 형식의 URL
- 프록시에 연결되는 경우 GET과 함께 사용
```
GET http://developer.mozilla.org/en-US/docs/Web/HTTP/Messages HTTP/1.1
```

**authority 형식**
- 도메인 이름 및 옵션 포트가 존재 (':'가 앞에 붙는다)
- HTTP 터널을 구축하는 경우 CONNECT과 함께 사용한다.
```
CONNECT developer.mozilla.org:80 HTTP/1.1
```

**asterisk 형식**
- OPTIONS와 함께 별표('\*') 하나로 간단하게 서버 전체를 나타낸다. (서버 전체를 지칭해야 할 경우 사용)
```
OPTIONS * HTTP/1.1
```

#### HTTP 버전
- HTTP 버전을 명기하는 이유는 메시지의 남은 구조를 결정하기 때문

### 헤더
- 헤더는 필드 네임과 필드 값을 포함해서 한 줄로 구성된다. (길어져도 한 줄로 구성된다.)
#### 헤더 필드 네임
- 대소문자 구분 없는 문자열이다.
- 헤더의 필드 네임 뒤에는 `:` 콜론이 붙는다.

### 헤더 필드 값
- 필드 네임 뒤의 : 다음에 오는 문자열

### 헤더의 종류
#### 제너럴 헤더
- HTTP 메시지 전체에 적용 됨
```
Host: localhost:8000
User-Agent: Mozilla/5.0 (Macintosh;... )... Firefox/51.0
Accept: text/html, application/xhtml+xml,..., */*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: qzip, deflate
```

#### 리퀘스트 헤더
- 요청의 내용을 구체화 시킴
```
Connection: keep-alive
Upgrade-Insecure-Requests: 1
```

#### 엔티티 헤더
- 요청 본문에 적용된다.
- 요총 내용이 없는 경우 엔티티 헤더는 적용되지 않는다.
```
Content-Type: multipart/form-data; boundary=-12656974
Content-Length: 345
```

### 본문
- 본문은 요청의 마지막 부분에 위치한다.
- 모든 요청에 본문이 들어가지는 않아도 된다.
- GET, HEAD, DELETE , OPTIONS처럼 리소스를 가져오는 요청은 보통 본문이 필요가 없다. POST 요청일 경우 서버에 입력하기 위한 데이터를 전달하기 위해 파라메터 메시지가 담긴다.

#### 단일 리소스 본문과 다중 리소스 본문
- 흔히 HTML에서 Form 태그를 통해서 여러가지 데이터를 보낸다. 몇 가지 단순 값일 수도 있고 파일과 같은 단일 파일을 전송하는데 사용할 수도 있다. 이를 하나의 요청에 묶어서 전송하기 때문에 

**단일 리소스 본문**
- 헤더 두 개로 정의된 단일 파일로 구성
- Content-Type와 Content-Length로 헤더로 이뤄진다.

**다중 리소스 본문 (multipart/form-data)**
- 다중 리소스 본문 : 멀티 파트 본문으로 구성


## 응답 HTTP 메시지 상세
### 시작 줄 (status line)
- 요청의 첫 줄이 start-line 이라고 하는 것에 반해 응답의 시작 줄은 status line이라고 부른다.
```
HTTP/1.1 404 Not Found.
```

#### 프로토콜 버전
- 보통 HTTP/1.1

#### 요청의 성공 여부
- 요청의 성공 여부에 대한 status 코드를 담는다.

#### 상태 택스트
- 상태 코드에 대한 설명을 글로 나타내어 상태 코드의 상세 내용을 보고 대응할 수 있도록 한다.

### 헤더
#### 제너럴 헤더

#### 리스폰스 헤더
- status line 에서 넣지 못한 정보를 넣는 역할을 한다.

#### 엔티티 헤더
- Content-Length와 같은 본문에 적용되는 헤더.
- 본문의 내용이 없다면 엔티티 헤더는 전송되지 않는다.

### 본문
- 응답의 마지막 부분에 들어간다.
- 모든 응답에 본문이 들어가는 것은 아니다. 201, 204과 같은 상태 코드를 가진 응답에는 보통 본문이 없다.

#### 길이가 알려진 단일 파일
- Content-Type와 Content-Length으로 정의한다.

#### 길이를 모르는 단일 파일
- Transfer-Encoding 헤더 필드 이름의 값이 `chunked`으로 설정되어 있다.
- 파일은 chunked 로 나눠져 인코딩 되어 있다.

#### 다중 리소스 본문
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types#multipartform-data

## Reference
- https://developer.mozilla.org/ko/docs/Web/HTTP/Messages
