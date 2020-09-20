---
title   : "컴포넌트 스캔"
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
![springFramework](/assets/img/spring/springImg.png)  

저번 포스트에서 빈을 등록하는 방법 3가지를 알아 봤다  
1. xml
2. Java Configuration
3. Component scanning  

3번 컴포넌트 스캔에 대해 알아보자  
__컴포넌트 스캔은 스프링이 직접 클래스를 검색해 빈으로 등록해 주는 기능이다__  
설정 클래스에 빈으로 등록하지 않아도 클래스를 빈으로 등록할 수 있으므로 컴포넌트 스캔 기능을 사용하면 설정 코드가 크게 줄어든다는 점이 있다.  

스프링에서 이 기능을 사용하려면 자바 설정 클래스위에 __@ComponentScan__ 애노테이션을 붙여주면된다.  
```java
@Configuration
@ComponentScan(basePackages={"spring"})
public class ApplicationConfig {
    ....
}
```  

__@ComponentScan__ 애노테이션은 다음 애노테이션이 적용된 Class들을 Scan하여 Bean으로 등록시켜주는 역할을 한다.  
1. @Component
2. @Controller
3. @Service
4. @Repository
5. @Configuration  

@ComponentScan 애노테이션은 scan범위를 지정할 수 있다.  

1. basePackages 속성  
```java
@Configuration
@ComponentScan(basePackages={"spring"})
public class ApplicationConfig {
    ....
}
```  

컴포넌트들을 스캔 대상 패키지를 지정한다.


2. basePackageClasses 속성
```java
@Configuration
@ComponentScan(basePackageClasses = Application.class)
public class ApplicationConfig {
    ...
}
``` 

컴포넌트들을 스캔 대상 타입을 지정한다.  