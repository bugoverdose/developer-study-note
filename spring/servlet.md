# Servlet

- Servlet은 웹 애플리케이션을 만들 때 필요한 인터페이스
- Spring Web MVC : Dispatcher Servlet을 사용하여 MVC 패턴으로 웹서비스를 만들 수 있게 해주는 Spring 모듈

### 등장 배경

1. 원래 웹서버는 정적인 웹페이지만 응답 가능했음.

2. CGI 구현체(Common Gateway Interface)를 통한 동적 웹페이지 응답이 가능해짐.

   문제점

   1. 요청이 들어올 때마다 웹서버는 매번 새로운 Process를 생성하고 CGI 구현체를 만들어냄
   2. 이전에 생성한 CGI 구현체를 그대로 사용할 수 없음. 매번 쓰레드별로 새로운 CGI 구현체를 생성.

   해결방안

   1. 각 요청을 Process가 아니라 `Thread로 처리`하자!
   2. SingleTon 패턴을 통해 `복수의 쓰레드가 하나의 구현체와 소통하도록` 하자!

### Servlet을 통한 요청 처리

- 특정 라우트에 들어오는 모든 요청들은 해당되는 Servlet에서 처리하는 구조

- Web Container(Servlet Container)의 기능

  1. 요청이 들어오면 요청별로 Thread를 하나 생성
  2. 각 Thread를 관련 Servlet 구현체에 연결
  3. 해당 Servlet에 정의된 메서드들을 호출

- Servlet 자체는 싱글톤 패턴으로 관리되므로 data 영역에서 일정 영역의 메모리만 공유하여 사용.

  - 각 요청에 대한 처리가 끝나더라도 Servlet은 소멸되지 않음.
  - 동일한 요청이 들어왔을 때 Servlet Container에 의해 다시 호출되고 재사용됨.

- 각 요청은 쓰레드별로 처리되므로 각 쓰레드의 heap 영역 & stack 영역의 메모리만 사용.

### 부록 : Servlet Container

Servlet Container는 서블릿을 담고 관리하는 컨테이너

- Servlet의 생명주기를 관리하는 역할을 수행하는 객체.
- 즉, 서블릿을 생성하고, 필요한 순간에 호출, 적절한 시점에 소멸시키는 역할

사용자로부터 요청이 들어왔을 때의 세부 과정

1. Servlet Request / Servlet Response 객체 생성

2. 서블릿 컨테이너는 해당 요청과 매핑된 Servlet을 찾음

   - 설정 파일을 읽어서 해당 url에 해당되는 요청이 어떤 Servlet을 필요로 하는지를 알아내고, 해당 Servlet 인스턴스가 컨테이너에 존재하는지를 확인.

3. 만약 해당 Servlet 인스턴스가 컨테이너에 존재하면 해당 인스턴스를 그대로 사용.

   - 컨테이너에 없다면 Servlet의 init 메서드를 호출하여 해당 Servlet을 새로 생성하여 사용.

4. Server Container에 쓰레드를 생성.

   - HttpServletResponse와 HttpServletRequest 객체를 인자로 Servlet의 service 메서드를 호출

5. service 처리 이후 최종적으로 사용자에게는 HttpResponse를 반환

6. 로직 수행 후 Servlet Request, Servlet Response 객체 소멸시키면서 종료
