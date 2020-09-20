---
title   : "컨테이너와 빈"
excerpt : "Spring Framework"
categories : 
    - Spring
tags : 
    - Spring
    - Web
    - back-end
sidebar:
    title: "Spring"
    image: http://placehold.it/350x250
    image_alt: "image"
    nav : sidebar-posts
---  
![springFramework](/assets/img/spring/springImg.png)  


## 스프링 컨테이너(= IoC 컨테이너)  

> 컨테이너란?
> 특정 객체의 생성과 관리를 담당하며 객체 운용에 필요한 다양한 기능을 제공한다.  

스프링은 __스프링 애플리케이션 컨텍스트(Spring application context)__ 라는 __컨테이너(Container)__ 를 제공한다. 이것은 애플리케이션 컴포넌트를 생성하고, 관리한다 그리고 애플리케이션 컴포넌트 또는 __빈(Bean)__ 들은 스프링 애플리케이션 컨텍스트 내부에서 서로 연결되어 완전한 애플리케이션을 구성한다.  

빈의 상호 연결은 __의존성 주입__ 이라고 알려진 패턴을 기반으로 수행된다. 애플맄케이션 컴포넌트에서 의존(사용)하는 다른 빈의 생성과 관리를 자체적으로 하는 대신 __컨테이너__ 가 해주며, 컨테이너는 모든 컴포넌트를 관리, 생성하고 필요로 하는 빈에 주입(연결)한다.

__[스프링 컨테이너의 종류]__  
스프링에서는 BeanFactory와 이를 상속한 ApplicationContext 두 가지 유형의 컨테이너를 제공한다.  

__Bean Factory__  
스프링 IoC를 담당하는 핵심 컨테이너를 가리킨다.  
빈을 등록, 생성, 조회 및 부가적인 빈을 관리하는 기능을 담당한다.  
생성된 객체를 검색하는데 필요한 getBean()과 같은 메소드가 정의되어있다.  

__ApplicationContext__  
BeanFactory를 확장한 IoC컨테이너이다. 빈을 등록하고 관리하는 기능은 BeanFactory와 동일하다.  
메시지, 프로필/환경변수 등을 처리할 수 있는 기능을 추가로 정의한다.  



## Bean(= 자바 객체)  
__스프링 IoC 컨테이너에 의해서 관리되고 애플리케이션의 핵심을 이루는 객체__ 들을 스프링에서는 Beans라고 부른다.
빈은 스프링 __IoC 컨테이너__ 에 의해서 인스턴스화 되어 조립되거나 관리되는 객체를 말한다.
빈과 빈 사이의 의존성은 컨테이너가 사용하는 메타데이터 환경설정에 반영된다.  
