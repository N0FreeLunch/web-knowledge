## 프레임
- 프레임은 프로토콜 동작에 필요한 정보를 정의하는 최소 단위이다. 
- HTTP2 이전의 프레임은 사람이 읽을 수 있는 시멘틱을 가졌지만 HTTP2 부터는 프레임이 캡슐화 되어 이해하기 어려운 구조로 되어 있다.
- 다음은 기본적인 HTTP 프레임의 구조이다.
```
GET / HTTP/1.1
Host: developer.mozilla.org
Accept-Language: fr
```

## 리퀘스트
```
GET / HTTP/1.1
Host: developer.mozilla.org
Accept-Language: fr
```

#### `GET`
- Method
- 클라이언트가 수행하고자 하는 동작을 정의합니다.
- GET, POST, options, HEAD 명사

#### `/`
- Path
- 프로토콜 `http://`, 도메인 `developer.mozilla.org`, TCP 포트 `TCP 포트`(80, 443 등)를 제외한 URL 리소스이다.

#### `HTTP/1.1`
- version of protocol

#### Headers
```
Host: developer.mozilla.org
Accept-Language: fr
```


## 리스폰스
```
HTTP/1.1 200 OK
Date: Sat, 09 Oct 2010 14:28:02 GMT
Server: Apache
Last-Modified: Tue, 01 Dec 2009 20:18:22 GMT
ETag: "51142bc1-7449-479b075b2891b"
Accept-Ranges: bytes
Content-Length: 29769
Content-Type: text/html

<!DOCTYPE html... (here comes the 29769 bytes of the requested web page)
```

#### `HTTP/1.1`
- 프로토콜 버전

#### `200`
- Status code
- 요청의 성공과 실패를 나타낸다.

#### `OK`
- Status message
- 상태 코드를 설명하는 메시지이다. 프로토콜의 정의에 따라 처리 방식이 달라지는 것은 아니다.
- 클라이언트의 처리 방식에 따라 이 정보를 이용하여 처리를 달리할 수는 있다.

#### Headers
```
Server: Apache
Last-Modified: Tue, 01 Dec 2009 20:18:22 GMT
ETag: "51142bc1-7449-479b075b2891b"
Accept-Ranges: bytes
Content-Length: 29769
Content-Type: text/html
```

#### Body
- 바디를 포함하고 포함하지 않을지는 선택사항이다.


## HTTP의 동작 방식
1. TCP 연결을 엽니다.
2. HTTP 메시지를 전송합니다.
3. 서버에 의해 전송된 응답을 읽어들입니다.
4. TCP 연결을 닫거나 다른 요청들을 위해 재사용합니다.

## HTTP 메시지
- 기본적으로 HTTP2도 HTTP1을 기반으로 구성되었기 때문에 이해하기 쉬운 시멘틱 언어로 쓰인 HTTP1이나 HTTP1.1을 이해함으로써 HTTP2의 구조도 이해해 볼 수 있다.


## Reference
- https://developer.mozilla.org/ko/docs/Web/HTTP/Overview#http_%ED%9D%90%EB%A6%84
