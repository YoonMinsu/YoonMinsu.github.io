---
title   : "스프링 프레임워크 동작 방식"
excerpt : "Spring Framework"
categories : 
    - Spring
tags : 
    - Spring
    - Java
---

# 1. 스프링 MVC 핵심 구성 요소
![run](/assets/img/spring/run.PNG)


- __DispatcherServlet__
  - 모든 연결을 담당한다.
  - 웹 브라우저로부터 요청이 들어오면 요청 처리를 위한 컨트롤러 객체를 검색한다.
  - 직접 컨트롤러를 검색하지 않고 `HandlerMapping`이라는 Bean 객체에게 컨트롤러 검색을 요청한다.(2번 과정)
- __HandlerMapping__
  - 클라이언트의 요청 경로를 이용해서 이를 처리할 컨트롤러 Bean 객체를 `DispatcherServlert'에 전달한다.
  - ex) 웹 요청 경로가 `/hello`라면 등록된 컨트롤러 Bean 중에서 `/hello` 요청 경로를 처리할 컨트롤러를 리턴한다

`DispatcherServlet`은 `HandlerMapping`이 찾아준 컨트롤러 객체를 처리할 수 있는 `HandlerAdapter`에게 요청 처리를 위임한다.  

- __HandlerAdapter__
  - 컨트롤러의 알맞은 메서드를 호출해서 요청을 처리하고(4 ~ 5번 과정) 그 결과를 `DispatcherServlet`에게 리턴한다.(6번 과정)
  - 이때 컨트롤러의 처리 결과를 `ModelAndView`라는 객체로 변환해서 `DispatcherServlet`에 리턴한다.

`HandlerAdapter`로부터 컨트롤러의 요청 처리 결과를 `ModelAndView`로 받으면 `DispatcherServlet`은 결과를 보여줄 __View__ 를 찾기 위해 `ViewResolver`객체를 사용한다.(7번 과정)

- __ViewResolver__
  - `ModelAndView`는 컨트롤러가 리턴한 `View`이름을 담고 있는데, 해당하는 `View`객체를 찾거나 생성해서 리턴한다.
  - 응답을 생성하기위해 `JSP`를 사용하는 `ViewResolver`는 매번 새로운 `View`객체를 생성해서 `DispatcherServlet`에 리턴한다.

`DispatcherServlet`은 `ViewResolver`가 리턴한 `View`객체에게 응답 결과 생성을 요청한다.(8번 과정) `JSP`를 사용하는 경우 `View`객체는 `JSP`를 실행함으로써 웹 브라우저에 전송할 응답 결과를 생성하고, 모든 과정이 끝이 난다.  

처리 과정을 보면 `DispatcherServlet`을 중심으로 `HandlerMapping, HandlerAdapter, Controller, View, JSP`가 각자 역할을 수행해서 클라이언트의 요청을 처리하는 것을 알 수 있다. 이 중 하나라도 어긋나면 클라이언트의 요청을 처리 할 수 없게 되므로 각각의 구성요소를 올바르게 설정하는 것이 중요하다.
