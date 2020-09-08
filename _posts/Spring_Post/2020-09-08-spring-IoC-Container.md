---
title   : "스프링은 객체 컨테이너"
excerpt : "Inversion of Control"
categories : 
    - Spring
tags : 
    - Spring
    - Web
    - Java
---

# __IoC(Inversion of Control)이란?__    

IoC 한글로 표현하면 __제어의 역전__ 이다.  
IoC란 기존 사용자가 모든 작업을 제어하던 것을 컨테이너에게 위임하여 객체의 생성부터 생명주기 등 모든 객체에 대한 제어권이 넘어 간 것을 IoC, 제어의 역전 이라고 한다.  

이러한 제어권을 위임받은 컨테이너가 IoC 컨테이너이다.

# __IoC Container__    
IoC 컨테이너는 등록된 Bean들을 관리하는 객체로 `Bean Factory` 또는 확장된 기능을 가진 `Application Context`를 사용한다. 주로 Bean의 생성 및 보관 제거 등을 관리하는 역할을 한다.  

BeanFactory는 DI의 기본사항을 제공하는 가장 단순한 컨테이너이다 빈(Bean) 객체를 호출했을 때 빈(Bean)의 생성이 이루어진다.  
Application context는 BeanFactory 인터페이스를 상속한 인터페이스이다. BeanFacroty와 달리 모든 싱글톤 빈(Bean)을 미리 생성해 두어 지연시간을 단축할 수 있다.  

빈(Bean)은 별도 설정을 하지 않는 경우 스프링은 한 개의 빈(Bean) 객체만을 생성하며, 이때 Bean 객체는 `싱글톤 범위를 갖는다`고 표현한다.  

빈을 등록하는 방법으로는 XML에 직접 등록, 어노테이션 이용, @configuration(자바설정파일)으로 명시된 클래스에 등록하는 방법이있다.  

# __Bean__  

__IoC 컨테이너에 등록되어 관리되는 객체를 빈(Bean)이라고 한다__  
빈은 스프링 Ioc 컨테이너에 의해서 인스턴스화되어 조립되거나 관리되는 객체를 말한다.  

## Bean 등록 방법 3가지  

#### __Application context.xml(root-context.xml)__ (Bean id와 클래스 명, 변수 이름, 의존관계 등을 xml로 작성하는 방법)  


크게 두 가지의 단점이 있다.
- 빈의 성격을 구분하기가 힘들어진다.
- xml에 작성해야할 빈의 양이 많아질 수록 코드의 양도 따라서 늘어난다.  


#### __컴포넌트 스캔__
빈으로 등록할 클래스에 어노테이션으로 명시해준다. 스프링은 컴포넌트 어노테이션이 붙은 클래스들을 스캔하여 자동으로 IoC컨테이너에 등록해준다.  

컴포넌트 어노테이션
@Component : 기본형   
@Repository : 데이터 접근 객체   
@Service : 서비스 객체   
@Controller : 컨트롤러 객체   
@Repository, @service, @Controller는 역할 구분을 위해 @Component를 재정의한 것이다.  

#### __Java Config Class__  
자바 클래스에 @Configuration 어노테이션으로 설정 파일임을 명시한다.     
Application context.xml(root-context.xml)에 등록할 내용을 자바 설정 클래스에 등록하는 방법이다.  
빈으로 등록할 클래스들의 객체 반환 함수를 작성하고 @Bean 어노테이션을 붙여줍니다.  
의존성이 있는 객체 반환 함수들은 생성자와 setter함수를 사용해 의존성을 명시해줍니다.  
@Configuration 어노테이션이 붙은 클래스에서 @Bean 어노테이션이 붙은 객체 반환 함수는 new를 사용해 생성해도 객체를 새로 생성하지 않고 싱글톤 빈 객체를 반환해줍니다.