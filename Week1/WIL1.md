# WIL1

## 강의 내용 정리

- 스프링부트를 활용한 웹 개발 3가지로 구분
1. 정적 컨텐츠
    - html 파일 자체를 그대로 웹에 전달.
    웹에서 localhost:8080/file_name.html 요청 → 내장 톰캣 서버가 요청 받아서 스프링 컨테이너에게 전달 →  컨트롤러에서 file_name이 있는지 확인(컨트롤러가 우선임) → 맵핑된 컨트롤러 없는 경우, resources/static에서 file_name이 있는지 확인→ 웹 브라우저에 전달
2. MVC + 템플릿 엔진
    - MVC : Model, View, Controller. 역할별로 3가지로 구분
        - Model: 어플리케이션 정보, 데이터, DB
        - View: 사용자에게 보여지는 화면(UI)
        - Controller: M-V를 잇는 역할.
        - EX
            - GetMapping : “hello-mvc”을 GET 방식으로 호출
            - @RequestParam("name"): 호출할 때 파라미터를 정의. required는 true가 default라서 이 경우는 url을 쓸 때 [localhost:8080/hello-mvc?name=___](http://localhost:8080/hello-mvc?name=___) 방식으로 name에 들어갈 데이터 넣어줌
                
                ```java
                @Controller
                public class HelloController {
                	@GetMapping("hello-mvc")
                	 public String helloMvc(@RequestParam("name") String name, Model model) {
                		 model.addAttribute("name", name);
                		 return "hello-template";
                	 }
                }
                ```
                
            - <p th:text="'hello ' + ${name}">hello! empty</p>: 태그 뒤에 나오는 hello! empty는 절대 경로로 찾아갔을 경우에 보여짐(서버에 빌드하지 않은 경우)
                
                ```html
                <html xmlns:th="http://www.thymeleaf.org">
                <body>
                <p th:text="'hello ' + ${name}">hello! empty</p>
                </body>
                </html>
                ```
                
3. API
    
    : JSON/HTML(XML) 방식으로 return해줌
    
    - @ResponseBody: http의 body에 리턴값을 넣어준다는 의미
    - HttpMessageConverter가 JSON 형식으로 리턴값을 웹브라우저에 띄움.

## 기타 필수 정리내용

- **RESTful**? REST의 원리를 따른다는 의미
    - **REST :** HTTP URI 를 통해 자원(Resource)을 명시(자윈 기반의 구조, ROA)하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것
        - CRUD? Create: 생성(POST)/Read: 조회(GET)/Update: 수정(PUT)/Delete: 삭제(DELETE)
    - **REST API** : REST 기반으로 서비스 API를 구현한 것