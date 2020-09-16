---
title   : "DI를 생성하는 방식"
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

# 생성자  

```java
public class MemeberRegisterService {
    private MemberDao memberDao;

    // 생성자를 통해 의존 객체를 주입받는다.
    public MemberRegisterService(MemberDao memberDao) {
        // 주입 받은 객체를 필드에 할당한다.
        this.memberDao = memberDao;
    }

    public Long regist(ResisterRequset req) {
        //주입 받은 의존 객체의 메서드를 사용한다.
        Member member = memberDao.seletByEmail(req.getEmail());
        ....
        memberDao.insert(newMember);
        return newMember.getId();
    }
}
```  

MemberRegisterService클래스는 생성자`public MemberRegisterService(MemberDao memberDao)`를 통해 의존객체를 주입받아 필드에 할당하였다.  
스프링은 설정 클래스에서 생서자를 이용해 의존 객체를 주입하기 위해 해당 설정을 담은 메서드를 호출했다.  

```java
@Bean
public MemeberDao memberDao() {
    return new MemberDao();
}

@Bean
public MemberRegisterService memberRegSvc() {
    return new MemberRegisterService(memberDao());
}
```  

# setter()  
생성자 외에 setter를 이용해서 객체를 주입받기도 한다. 일반적인 setter메서드는 자바빈 규칙에 따라 작성한다.  
- 메서드 이름이 set으로 시작한다.
- set 뒤에 첫 글자는 대문자로 시작한다.
- 파라미터가 1개이다.
- 리턴 타입이 void이다.

set과 get 메서드를 각각 세터(setter)와 게터(getter)라고 부르며, setAge와 같은 쓰기 메서드는 프로퍼티 값을 변경하므로 프로퍼티 설정 메서드라고도 부른다.  

```java
public class MemberInfoPrinter {
    private MemberDao memberDao;
    private MemberPrinter printer;

    public void setMemberDao(MemberDao memberDao) {
        this.memberDao = memberDao;
    }

    public void setPrinter(MemberPrinter printer) {
        this.printer = printer;
    }
}


// 설정 클래스
...
@Bean
public MemberInfoPrinter infoPrinter() {
    MemberInfoPrinter printer = new MemberInfoPrinter();
    printer.setMemberDao(memberDao());
    printer.setPrinter(memberPrinter());
    return printer;
}
```  
infoPrinter Bean은 setter메서드를 이용해서 memberDao()와 memberPrinter() Bean을 주입한다.

