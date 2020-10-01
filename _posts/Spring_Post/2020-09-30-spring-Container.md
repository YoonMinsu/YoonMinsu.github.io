---
title   : "스프링 컨테이너"
categories : 
    - Spring
tags : 
    - java
    - spring
    - web
sidebar:
    title: "Spring"
    nav : sidebar-posts
---  
## 스프링은 객체 컨테이너  

스프링의 핵심 기능은 객체를 생성하고 초기화 하는 것이다.  

이와 관련된 기능은 __ApplicationContext__ 라는 인터페이스에 정의 되어 있다.  

스프링에서는 ApplicationContext를 스프링 컨테이너라고 한다.  

스프링 컨테이너는 XML파일이나, 그루비 설정코드, 애노테이션 기반의 자바 설정 클래스로 만들 수 있다.  

요즘 스프링 부트에서 많이 사용 하는 어노테이션 기반의 자바 설정 클래스로 스프링 컨테이너를 만들려면  

__AnnotationConfigureAppplicationContext__ 라는 클래스를 사용하면 된다. 이 클래스는 위에서 설명한 ApplicationContext 인터페이스에 구현 클래스이다.  

간단한 계층도를 살펴보자 원래는 이 외에 더 많은 인터페이스가 존재한다.  

![container](/assets/img/spring/Container.png)  
__[참고 - 초보 웹 개발자를 위한 스프링5 프로그래밍 입문 49P]__  

위 계층도를 보면 가장 상위의 BeanFactory 인터페이스가 존재한다.  

BeanFactory는 스프링 컨테이너의 최상위 인터페이스이다. 스프링 Bean을 관리하고 조회하는 역할을 담당한다.  

생성되는 빈을 검색하는데 필요한 getBean() 메서드가 정의되어 있다. 객체를 검색하는 것 이외에 싱글톤/프로토타입 빈인지 확인하는 기능도 제공한다.  

ApplicationContext는 BeanFactory의 기능을 모두 상속받아 제공한다.  

둘 다 빈을 관리하고 검색하는 기능이 존재하지만 애플리케이션 개발에 있어서 빈을 관리하고 검색하는 기능을 넘어서 많은 부가 기능을 필요로 한다.  

ApplicationContext는 메시지소스를 활용한 국제화 기능, 프로필/환경변수, 애플리케이션 이벤트, 편리한 리소스 조회 등 더 많은 부가기능을 제공한다.  

위 게층도에서 AnnotationConfigureApplicationContext를 비롯해 계층도의 가장 하단에 위치한 3개의 클래스는 BeanFactory와 ApplicationContext에 정의된 기능의 구현을 제공한다.  

- __AnnotationConfigureApplicationContext__: 자바 애노테이션 기반의 설정 클래스를 이용해 정보를 가져온다.  
- __GenericXmlApplicationContext__: XML로부터 객체 설정 정보를 가져온다.  
- __GenericGroovyApplicationContext__: 그루비 코드드를 이용해 설정 정보를 가져온다.  

어떤 구현 클래스를 사용하든, 각 구현 클래스는 설정 정보로부터 빈(Bean)이라고 불리는 객체를 생성하고 그 객체를 내부에서 보관한다.  

ApplicationContext(또는 BeanFactory)는 Bean객체의 생성, 초기화, 보관, 제거 등을 관리하고 있어서 ApplicationContext 또는 BeanFactory를 컨테이너(Container)라고도 부른다.  

BeanFactory를 직접 사용할 일은 거의 없다. 부가기능이 포함된 ApplicationContext를 사용한다.  

### 스프링 컨테이너의 Bean 객체 관리  

스프링 컨테이너는 내부적으로 Bean 객체와 Bean 이름을 연결하는 정보를 갖는다.  

![config](/assets/img/spring/config.png)  

```java
ApplicationContext ac = new AnnotationConfigureApplicationContext(AppConfig.class);
```  
스프링 컨테이너를 생성할 때는 구성 정보를 지정해주어야 한다.  
위 그림은 자바 애노테이션 기반의 설정 클래스인 AppConfig를 사용하였다.  


![config2](/assets/img/spring/config2.png)  
스프링 컨테이너는 파라미터로 넘어온 설정 클래스 정보를 사용해서 스프링 빈을 등록한다.  

> 스프링 빈 이름은 항상 다른 이름을 부여해야 한다. 같은 이름을 부여하면 다른 빈이 무시되거나 기존 빈을 덮어버리거나 설정에 따라 오류가 발생한다.

### 스프링 빈 의존관계 설정  

![containerBean](/assets/img/spring/continerBean.PNG)

스프링 컨테이너는 설정 정보를 참고해서 의존관계를 주입(Dependency Injection)한다.  

스프링은 빈을 생성하고, 의존관계를 주입하는 단계가 나누어져 있다. 위 처럼 자바코드로 스프링 빈을 등록하면 생성자를 호출하면서 의존관계 주입도 한번에 처리된다.  


__[정리]__
스프링 컨테이너는 이름과 실제 객체의 관계뿐만 아니라 실제 객체의 생성, 초기화, 의존 주입 등 스프링 컨테이너는 객체 관리를 위한 다양한 기능을 제공한다.  

---

참고  
- __초보 웹 개발자를 위한 스프링5 프로그래밍 입문__
- __인프런 스프링 핵심 원리 - 기본편__