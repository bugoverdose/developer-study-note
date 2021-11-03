# HTTP/2.0

- HTTP2.0은 HTTP1.1의 프로토콜을 계승한 동일한 API면서 성능 향상에 초점을 맞춤.
- HTTP/2 requests are multiplexed over a single TCP connection, allowing multiple concurrent messages to be in flight without compromising network resource usage.

## Multiplexed Streams: 멀티플렉싱

- 하나의 TCP connection에 대해 동시에 복수의 메시지를 주고 받을 수 있음. 이 과정에서 네트워크 자원 사용에 있어 별도의 비용 발생하지 않음.
- Response는 순서에 상관없이 stream으로 주고 받음.

## 장점

### Stream Prioritization

- 리소스 간 우선순위를 설정해 클라이언트가 더욱 필요로 하는 리소스부터 응답하고자 함.

### Server Push

- 클라이언트가 요청하지 않은 리소스도 서버에서 보내줄 수 있음.

### Header Compression을 통한 요청/응답 사이즈 감소

- Header table과 Huffman Encoding 기법(HPACK 압축방식)을 이용하여 압축을 함.
