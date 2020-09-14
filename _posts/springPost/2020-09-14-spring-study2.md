---
title   : "스프링을 이용한 객체 조립과 사용"
excerpt : "초보 웹 개발자를 위한 스프링5 프로그래밍 입문 - 최범균 저"
categories : 
    - Spring
tags : 
    - Spring
    - Web
---  

앞서 구현한 Assembler 클래스 대신 스프링을 사용하는 코드를 사용해보자.  
스프링을 사용하려면 먼저 스프링이 어떤 객체를 생성하고, 의존을 어떻게 주입하리를 정의한 설정 정보를 작성해야 한다.  

설정 정보를 작성하는 방법이 몇 가지 있는데, 나중에 다뤄야겠다.  
최신 버전의 스프링에서는 자바 기반의 구성이 더 많이 사용된다고 한다.  

```java
@Configuration
public class AppConfig {

    @Bean
    public MemberDao memberDao() {
        return new MemberDao();
    }

    @Bean
    public MemberRegisterService memberRegSvc() {
        return new MemberRegisterService(memberDao());
    }

    @Bean 
    public ChangePasswordService changePwdSvc() {
        ChangePasswordService pwdSvc = new ChangePasswordService();
        pwdSvc.setMemberDao(memberDao());
        return pwdSvc;
    }
}
```  

`@Configuration` 애노테이션은 이것이 각 Bean을 __스프링 애플리케이션 컨텍스트(컨테이너)__ 에 제공하는 구성 클래스라는 것을 스프링에게 알려준다.  
구성 클래스의 메서드에는 `@Bean` 애노테션이 지정되어 있으며, 이것은 각 메서드에서 반환되는 객체가 스프링 애플리케이션 컨텍스트(컨테이너)의 Bean으로 추가되어야 한다는 것을 나타낸다.  

memberDao() 메서드를 이용해 생성한 Bean 객체는 "memberDao"라는 이름으로 등록된다.  

이제 객체를 생성하고 의존 객체를 주입하는 것은 스프링 컨테이너이므로 설정 클래스를 이용해서 컨테이너를 생성해야 한다.  

```java
public class MainForSpring {
 
    private static ApplicationContext ctx = null;
 
    public static void main(String[] args) {
        // 입력으로 설정 정보를 받아서 스프링 컨테이너를 생성한다.
        ctx = new AnnotationConfigApplicationContext(AppCtx.class);
 
        // 스프링 컨테이너로부터 이름이 "memberRegSvc"인 빈 객체를 가져온다. 
        // 두 번째 매개변수는 가져올 빈 객체의 타입이다.
        MemberRegisterService regSvc = ctx.getBean("memberRegSvc", MemberRegisterService.class);
        
        // 스프링 컨테이너로부터 이름이 "changePwdSvc"인 빈 객체를 가져온다.
        // 두 번째 매개변수는 가져올 빈 객체의 타입이다.
        ChangePasswordService changePwdSvc = ctx.getBean("changePwdSvc", ChangePasswordService.class);
    }
}
```
