# Coroutine

- 비동기적으로 실행되는 코드를 간소화하기 위한 동시 실행 설계 패턴.
- 기본적으로 Kotlin, C#, Python, Go 등 다양한 언어에서 지원되는 개념이자 문법.

## Kotlin의 코루틴

- coroutine is an `instance of suspendable computation`
- 나머지 코드와 동시에 실행될 수 있는 코드 블록을 관리하는 구조, 즉 비동기적 처리 지원.
- 쓰레드보다 가벼우며, 특정 쓰레드에 종속되지 않음.

- 각각의 코루틴은 실행되어야 하는 하나의 작업으로, 쓰레드는 복수의 코루틴이 실행되는 공간

- 쓰레드와의 차이: Concurrency(동시성) vs Parallelism(병렬처리)

  - 복수의 쓰레드 존재시, 각 쓰레드는 서로 별개의 작업을 `병렬`적으로 실행함.
  - 코루틴을 통한 비동기 처리는 `동시성`, 즉 하나의 쓰레드에서 짧은 전환으로 여러 실행단위를 번갈아 실행하면서 동시에 처리되는 것처럼 보이는 것.

  - [공식문서](https://kotlinlang.org/docs/coroutines-overview.html)
  - [코틀린 코루틴(Coroutines) 강좌](https://www.youtube.com/watch?v=Vs34wiuJMYk&list=PLbJr8hAHHCP5N6Lsot8SAnC28SoxwAU5A)

### 코루틴의 기본 구조

```
fun main() = runBlocking { // this: CoroutineScope
    launch { // launch a new coroutine and continue
        delay(1000L) // non-blocking delay for 1 second (default time unit is ms)
        println("World!") // print after delay
    }
    println("Hello") // main coroutine continues while a previous one is delayed
}
// Hello
// World!
```

- `runBlocking` : 코루틴 빌더. 코루틴들과 일반적인 코드 사이를 잇는 다리 역할.

  - runBlocking { ... }에서 중괄호 내부에 코루틴들을 실행

- `launch` : 코루틴 빌더. 현재 실행하던 작업을 계속 실행시키면서 새로운 코루틴을 실행시킴.

- `delay` : suspending function. 일정 기간 동안 특정 코루틴의 실행을 중단시키는 기능.

  - 해당 코루틴이 중단되더라도 쓰레드는 블록시키지 않으므로 다른 코루틴들은 실행될 수 있음.

- `suspending function` : `suspend` 키워드로 선언된 함수들

  - 기본적으로 코루틴에서 일반적인 함수처럼 사용 가능.
  - delay와 같은 다른 suspending function을 실행하여 코루틴의 실행을 중단시킬 수 있음.

```
fun main() = runBlocking { // this: CoroutineScope
    launch { doWorld() }
    println("Hello")
}

suspend fun doWorld() { // suspending function
    delay(1000L)
    println("World!")
}
```

### 코루틴을 통한 비동기 처리 기본 구조

- 안드로에드에서는 코드를 백그라운드 쓰레드에서 처리하기 위해 코루틴을 사용함.

- 특히 네트워크 통신 작업과 화면 렌더링 작업의 경우 코루틴을 통해 서로 다른 쓰레드에서 비동기적으로 처리하는 것이 일반적

- [안드로이드 네트워크 통신 - 라이브 코딩 예제](https://www.youtube.com/watch?v=yIdFRXHawYc)

```
CoroutineScope(Dispatchers.코루틴_컨텍스트).동기/비동기 {
    ...
}
```

- 3가지 CoroutineContext

  - Main: 메인 스레드. 화면 UI 작업 등을 하는 곳
  - IO: 네트워크, DB 등 백그라운드에서 필요한 작업을 하는 곳
  - Default: 정렬이나 무거운 계산 작업 등을 하는 곳

- 해당 쓰레드를 동기 혹은 비동기로 돌릴 것임을 지정
  - launch: 동기
  - async: 비동기

```
// 동기식 메인 쓰레드 안에서, 비동기식 IO 쓰레드를 실행하는 구조
CoroutineScope(Dispatchers.Main).launch {
    val html = CoroutineScope(Dispatchers.IO).async {
        getHtml()
    }.await()  // await : 작업이 완료될 때까지 대기

    textView.text = html.toString()
}
```
