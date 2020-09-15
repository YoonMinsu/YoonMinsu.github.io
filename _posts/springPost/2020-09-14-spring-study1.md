---
title   : "객체 조립기"
excerpt : "초보 웹 개발자를 위한 스프링5 프로그래밍 입문 - 최범균 저"
categories : 
    - Spring
tags : 
    - Spring
    - Web
sidebar:
    title: "Spring"
    nav : sidebar-posts
---

DI를 사용할 때 객체 생성에 사용할 클래스를 변경하기 위해 객체를 주입하는 코드 한 곳만 변경하면 된다.  
그렇다면 실제 객체를 생성하는 코드는 어디에 있는게 좋을까?  

```java
public class Main {
    public static void main(String[] args) {
        MemberDao memberDao = new MemberDao();
        MemeberRegisterService regSvc = new MemeberRegisterService(memberDao);
        ...
    }
}
```  

main 메서드에서 의존 대상 객체를 생성하고 주입하는 방법이 나쁘지는 않다. 이 방법보다 나은 방법은 객체를 생성하고 의존 객체를 주입해주는 클래스를 따로 작성하는 것이다. 의존 객체를 주입한다는 것은 서로 다른 두 객체를 조립한다고 생각할 수 있는데, 이러한 클래스를 __조립기__ 라고도 표현한다.  

```java
public class Assembler {
    
    private MemberDao memberDao;
    private MemberRegisterService regSvc;
    private ChangePasswordService pwdSvc;

    public Assembler() {
        memberDao = new MemberDao();
        regSvc = new MemberRegisterService(memberDao);
        pwdSbc = new ChangePasswordService();
        pwdSvc.setMemberDao(memberDao);
    }

    public MemberDao getMemberDao() {
        return memberDao;
    }

    public MemberRegisterService getMemberRegisterService() {
        return regSvc;
    }

    public ChangePasswordService getChangePasswordService() {
        return pwdSvc;
    }
}
```  

Assembler 클래스의 생성자에서 MemberRegisterService와 ChangePasswordService 객체에 대한 의존을 주입한다. MemberRegisterService는 생성자를 통해 ChangePasswordService는 setter를 통해 주입 받는다.  

Assembler 클래스를 사용하는 코드는 Assembler 객체를 생성하고, getter를 이용해 필요한 객체를 구하고 그 객체를 사용한다.  

```java
Assembler assembler = new Assembler();
ChangePasswordService pwdSvc = assmebler.getChangePasswordService();
...
```  

조립기는 객체를 생성하고 의존 객체를 주입하는 기능을 제공한다. 또한 특정 객체가 필요한 곳에 객체를 제공해준다.
