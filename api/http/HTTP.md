# HTTP(Hypertext Transfer Protocol)

- [HTTP/1.1](./HTTP1.1.md)
- [HTTP/2.0](./HTTP2.0.md)
- [HTTP 버전별 요청 처리 순서 차이](./HTTP_버전별_차이.PNG)

## HTTP : 웹에서 쓰이는 통신 프로토콜.

- 프로토콜: 상호간에 정의한 규칙.
- HTTP 프로토콜은 TCP/IP 프로토콜 위의 레이어(Application layer)에서 동작
- HTTP는 기본적으로 서버-클라이언트 구조를 따름: HTTP 프로토콜로 데이터를 주고받기 위해서는 Request를 보내고 Response를 받아야 함.

## 핵심

### HTTP 프로토콜은 stateless 프로토콜

- '상태가 없다' : 데이터를 주고 받기 위한 각각의 데이터 요청이 서로 `독립적으로 관리`됨.
- 즉, 이전 데이터 요청과 다음 데이터 요청은 서로 관련이 없음.

### URL과 HTTP 요청 메소드 활용

- URL을 통해 특정 서버 주소에 특정 데이터를 요청할 수 있음.
- REST API에서 지정하는 HTTP 메소드는 4가지: GET, POST, PUT, DELETE
