# R2DBC (Reactive Relational Database Connectivity)

- JDBC Datasource의 문제점 : 특정 쿼리에 대한 결과를 받기까지 Blocking 상태가 되어 쓰레드 전체가 대기해야 함.

- R2DBC : Asynchronous Non-blocking Datasource

- WebFlux를 사용해도 Spring을 사용하는 주된 사용자들은 DB와의 연결을 걸어놓았을 텐데, DB가 Blocking 인 경우 결국 Non-Blocking의 이점을 하나도 못얻기 때문에 R2DBC의 이점은 크다고 말할 수 있다

R2DBC는 다음과 같은 뜻을 내포하고 있다고 한다

Features

Based on the Reactive Streams specification. R2DBC is founded on the Reactive Streams specification, which provides a fully-reactive non-blocking API.

Works with relational databases. In contrast to the blocking nature of JDBC, R2DBC allows you to work with SQL databases using a reactive API.

Supports scalable solutions. With Reactive Streams, R2DBC enables you to move from the classic “one thread per connection” model to a more powerful and scalable approach.

Provides an open specification. R2DBC is an open specification and establishes a Service Provider Interface (SPI) for driver vendors to implement and clients to consume.
