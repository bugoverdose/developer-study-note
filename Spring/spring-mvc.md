# Spring MVC

- Servlet : 웹 애플리케이션을 만들 때 필요한 인터페이스
- Spring Web MVC : Dispatcher Servlet을 사용하여 MVC 패턴으로 웹서비스를 만들 수 있게 해주는 Spring 모듈

### 전통적인 Servlet 사용 방법

- 각 라우트(url)마다 종류별로 servlet들을 생성하도록 Web.xml 파일에 등록됨.

- 특정 라우트에 들어오는 모든 요청들은 해당 Servlet에서 처리

  - /member => Member Servlet
  - /line => Line Servlet
  - /station => Station Servlet

### Dispatcher Servlet의 등장

- 복수의 Servlet 대신 하나의 Dispatcher Servlet만으로 모든 요청을 담당.
- 대신 복수의 Controller를 두어 라우트 및 HTTP 메서드에 따라 다르게 처리

  - /member => Dispatcher => Member Controller
  - /line => Dispatcher Servlet => Line Controller
  - /station => Dispatcher => Station Controller

- cf) 모든 요청이 Dispatcher Servlet으로 가도록 Dispatcher Servlet이 Web.xml에 등록된 구조

### Spring Web MVC의 동작 원리 (단순화 버전)

```
                  req                    req                 req
Servlet Container <-> Dispatcher Servlet <-> Handler Adapter <-> Controller
                  res               model & view             결과
```

[1] 들어오는 모든 요청은 우선 Dispatcher Servlet으로 가게 됨.

[2] Handler Adapter : 요청을 처리할 Handler(=Controller)에 대응시키는 역할.

- 들어온 요청에 따라 적절한 Controller를 호출하고, Controller가 처리한 결과를 받아 Dispatcher Servlet에 응답해주는 기능.

- Handler는 Controller를 포함하는 상위 개념.

- Dispatcher Servlet을 Web.xml에 등록하면 Servlet 설정 파일이 자동 생성됨. Servlet 설정 파일에서 어떤 방식의 Handler Mapping을 사용할지 지정 가능.

- 다양한 Handler Mapping 방식들

  1. BeanNameHandlerMapping : Bean명과 Url을 Mapping해주는 방식. 디폴트로 설정되는 방식.

     - ex) /employee로 접근하면 Bean명을 employee로 지은 컨트롤러에 맵핑됨.

  2. ControllerClassNameHandlerMapping
  3. SimpleUrlHandlerMapping

  4. DefaultAnnotationHandlerMapping : Annotation으로 Url과 Mapping하는 방식.
     ```
     @Controller // 가장 모던한 방식
     public class EmployeeController {
         @RequestMapping("/Employee") // "/Employee"로 요청이 들어오면
             public String do() { // do() 메서드로 mapping 해주는 방식
             // ~~
         }
     }
     ```

[3] Controller => Handler Adapter => Dispatcher Servlet => Servlet Container

- Controller가 처리한 결과를 받아 ModelAndView 형태로 Dispatcher Servlet에 응답
  - Model: Data, 즉 Controller의 처리 결과.
  - View: Data를 넘길 페이지. Controller는 대체로 View의 논리적인 이름만 String 형태로 반환.
- 최종 응답 결과는 Servlet Container에 의해 요청을 보낸 사용자에게 그대로 돌아감.
