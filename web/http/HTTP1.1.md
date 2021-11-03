# HTTP/1.1

- 아직까지도 웹에서 가장 많이 사용되고 있는 프로토콜 (1999년에 출시)
- 기본적으로 각 연결당 하나의 Request과 Response를 처리
- 동시전송 문제와 다수의 리소스를 처리할 때 성능 이슈 지님: HOLB, RTT, 중복되는 헤더 값 등

## Pipelining

- pipelining 기법: 하나의 connection 내에서 다수 개의 파일을 Request/Response 받을 수 있는 기법
- HTTP/1.1이 지닌 `connection당 하나의 요청만 처리한다는 문제점`을 개선하기 위해 pipelining 도입되었으나 HOLB와 같은 파이프라이닝 기법이 본질적으로 지닌 단점들을 여전히 지님.

## 단점

### HOLB(Head Of Line Blocking) - 특정 응답 지연 문제

- 3가지 이미지 파일을 처리해야 하는 경우, 먼저 들어온 이미지가 처리되는 동안 2번째, 3번째 이미지는 처리되지 못하고 그대로 대기하게 되는 현상.
- pipelining 기법이 지닌 문제점 중 하나

### RTT(Round Trip Time) 증가 문제

- 하나의 connection마다 tcp 연결을 함.
- 문제는 신뢰성 연결을 하는 tcp connection은 시작시 3-way handshake, 종료시 4-way handshake가 반복적으로 발생, 이로인한 오버헤드가 발생합니다.
- HTTP1.1가 하나의 connection에 하나의 request를 처리하기 때문에 발생하는 문제.

### heavy header

- HTTP/1.1의 header에는 많은 metadata가 저장되어 있음.
- 한 명의 사용자는 각 요청마다 중복된 header값을 반복하여 전송해서 요청이 매우 무거움.
- 특히 계속 전송되는 cookie가 큰 문제.
