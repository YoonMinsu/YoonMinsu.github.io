---
title   : "Spring MVC 흐름"
excerpt : "Spring Framework"
categories : 
    - Spring
tags : 
    - Spring
    - Web
    - back-end
sidebar:
    title: "Spring"
    nav : sidebar-posts
---  
## 스프링 MVC 기본 동작과정  

![springRun](/assets/img/spring/springRun.png)  

DataBase를 제외한 파란색 부분은 SpringMVC가 제공하는 부분이다.  
보라색 부분은 개발자가 만들어야 한다.  
녹색 부분 View는 Spring이 제공하는 것도 있고 개발자가 구현해야 하는것도 있다.  

__진행 과정__  
1. 클라이언트에서 요청이 들어오면 모든 요청을 DispatcherServlet이 받는다.
2. DispatcherServlet은 어떤 컨트롤러, 메소드를 사용해야 하는지 HandlerMapping에게 물어본다.
   - HandlerMapping이 혼자서 알아낼 수는 없다.
   - 개발자가 xml이나 Java 파일에 애노테이션으로 설정해 놓는다.
   - 위 정보를 바탕으로 웹 애플리케이션이 실행 될때 HandlerMapping 객체들이 생성되면서 관리한다.
   - DispatcherServlet은 HandlerMapping으로부터 들어온 요청에 알맞은 컨트롤러와 해당되는 메소드는 무엇인지에 대한 정보를 알아내게 된다.
3. DispacherServlet은 HandlerAdapter에게 실행을 요청한다. 
4. 그 때 결정된 컨트롤러와 해당 메서드가 실행이 된다. 
5. 결과를 Model에 받아서 DispatcherServlet에게 전달 한다.
   - 아직까지는 View가 나온 상태가 아니다.
   - View에 필요한 데이터들 Model에 담겨져 DispatcherServlet에게 전달된 상황이다.
6. DispacherServlet은 컨트롤러가 리턴한 view Name을 알아온다.
   - 컨트롤러가 리턴한 view name 가지고 적절한 ViewResolver를 선택한다.
   - viewResolver가 어떤 View이다라는 정보를 알려준다.
7. View를 출력한다.
8. 응답한다

