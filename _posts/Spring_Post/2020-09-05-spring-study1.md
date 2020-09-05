---
title   : "스프링 DI"
excerpt : "Dependency Injection"
categories : 
    - Spring
tags : 
    - Spring
    - Web
    - Java
---

# 1. 의존이란?

DI는 Dependency Injection의 약자로 우리말로는 의존 주입이라고한다. 여기서 의존은 __객체 간의 의존을 의미__ 한다.

```java
public class MemberRegisterService {
    private MemberDao memberDao = new MemberDao();

    public void regist(RegisterRequest rq) {
        // 이메일로 회원 데이터(Member) 조회
        Member member = memberDao.selectByEmail(rq.getEmail());

        if (member != null) {
            // 같은 이메일을 가진 회원이 존재하면 예외 발생
            throw new DuplicateMemberException("dup email" + rq.getEmail());
        }

        // 같은 이메일을 가진 회원이 존재하지 않으면 DataBase에 삽입
        Memeber newMember = new Member(rq.getEmail(), rq.getPassword(), rq.getName(), LocalDateTime.now());

        memberDao.insert(newMember);
    }
}
```

서로 다른 이메일 주소를 사용할 수 없는 요구사항이 있다고 가정할 때, 이 제약 사항을 처리하기위해 MemberRegisterService 클래스는 MemberDao 객체의 selectByEmail() 메서드를 이용해서 동일한 이메일을 가진 회원 데이터가 존재하는지 확인한다. 같은 이메일을 가진 회원이 존재한다면 예외를 발생시키고, 존재 하지 않으면 회원 정보를 담은 Member객체를 생성하고 MemberDao객체의 insert() 메서드를 이용해 DB에 삽입한다.  

위 코드에서 중요한 건 MemberRegisterService 클래스는 DB처리를 위해 MemberDao 클래스의 메서드를 사용한다는 점이다.  

이렇게 __한 클래스가 다른 클래스의 메서드를 실행할 때 이를 "의존"한다고 표현한다__ 위 코드는 `MemberRegisterService가 MemberDao 클래스에 의존 한다`고 표현할 수 있다.  

> 의존은 변경에 의해 영향을 받는 관계를 의미한다. 예를 들어 MemberDao의 insert() 메서드의 이름을 insertMember()로 변경하면 이 메서드를 사용하는 MemberRegisterService 클래스의 소스 코드도 함께 변경된다. 이렇게 __변경에 따른 영향이 전파되는 관계를 의존한다고 표현한다__


의존하는 대상을 구하는 가장 쉬운 방법은 의존 대상 객체를 직접 생성하는 것이다. 위 코드도 MemberRegisterService 클래스도 의존 대상인 MemberDao의 객체를 직접 생성에 필드에 할당했다.  
```java
public class MemberRegisterService {
    private MemberDao memberDao = new MemberDao();
    ....
}
```  

MemberRegisterService 클래스에서 의존하는 MemberDao 객체를 직접 생성하기 때문에 MemberRegisterService 객체를 생성하는 순간에 MemberDao 객체도 함께 생성된다.  
```java
MemberRegisterService registerService = new MemberRegisterService();
```  

클래스 내부에 직접 의존 객체를 생성하는 것이 쉽긴 하지만 유지보수 관점에서 문제점을 유발할 수 있다.

# 2. DI를 통한 의존 처리  

__DI(Dependency Injection, 의존 주입)는 의존하는 객체를 직접 생성하는 대신 의존 객체를 전달 받는 방식__ 을 사용한다.

```java
public class MemberRegisterService {
    private MemberDao memberDao;

    public MemberRegisterService(MemberDao memberDao) {
        this.memberDao = memberDao;
    }

    public Long regist(RegisterRequest rq) {
        // 이메일로 회원 데이터(Member) 조회
        Member member = memberDao.selectByEmail(rq.getEmail());

        if (member != null) {
            // 같은 이메일을 가진 회원이 존재하면 예외 발생
            throw new DuplicateMemberException("dup email" + rq.getEmail());
        }

        // 같은 이메일을 가진 회원이 존재하지 않으면 DataBase에 삽입
        Memeber newMember = new Member(rq.getEmail(), rq.getPassword(), rq.getName(), LocalDateTime.now());

        memberDao.insert(newMember);
        return newMember.getid();
    }
}
```  

위 코드는 직접 의존 객체를 생성하지 않고, 생성자를 통해 MemberRegisterService 클래스가 __의존(Dependency)__ 하고 있는 MemberDao 객체를 __주입(Injection)__ 받은 것이다.  

DI를 적용한 결과 MemberRegisterService 클래스를 사용하는 코드는 MemberRegisterService 객체를 생성할 때 생성자에 MemberDao 객체를 전달해야 한다.  
```java
MemberDao memberDao = new MemberDao();
MemberRegisterService registerService = new MemberRegisterService(memberDao);
```

# 3. DI와 의존 객체 변경의 유연함  

의존 객체를 직접 생성하는 방식은 필드나 생성자에서 new 연산자를 이용해서 객체를 생성한다.  
MemberRegisterService 클래스도 밑의 코드처럼 의존 객체를 직접 생성할 수 있다.
```java
public class MemberRegisterService {
    private MemberDao memberDao = new MemberDao();
    ....
}
```

회원의 암호를 변경 기능을 제공하는 ChangePasswordService 클래스도 의존 객체를 직접 생성한다고 하자
```java
public class ChangePasswordService {
    private MemberDao memberDao = new MemberDao();
    ....
}
```

MemberDao 클래스는 회원 데이터를 데이터베이스에 저장한다고 가정해보자. 이 상태에서 회원 데이터의 빠른 조회를 위해 캐시를 적용해야 하는 상황이 발생했다. 그래서 MemberDao 클래스를 상속받은 CachedMemberDao 클래스를 만들었다.

```java
public class CachedMemberDao extends MemberDao {
    ....
}
```  

> 캐시(cache)는 데이터 값을 복사해 놓은 임시 장소를 가리킨다. 보통 조회 속도 향상을 위해 캐시를 사용한다.

캐시 기능을 적용한 CachedMemberDao를 사용하려면 위에서 작성한 회원 암호 기능과 회원 등록 기능을 제공하는 클래스는 밑에와 같이 바뀌어야 한다.  
```java

public class MemberRegisterService {
    private MemberDao memberDao = new CachedMemberDao();
    ....
}

public class ChangePasswordService {
    private MemberDao memberDao = new CachedMemberDao();
    ....
}
```

만약에 MemberDao 객체가 필요한 클래스가 3개 또는 10개 그 이상이라면 모두 위와 같이 소스 코드를 변경해야 한다.  

하지만 동일한 상황에서 DI를 적용한 코드라면 수정할 코드가 줄어든다.
```java
public class MemberRegisterService {
    private MemberDao memberDao;

    public MemberRegisterService(MemberDao memberDao) {
        this.memberDao = memberDao;
    }
    .....
}

public class ChangePasswordService {
    private MemberDao memberDao;

    public ChangePasswordService(MemberDao memberDao) {
        this.memberDao = memberDao;
    }
    .....
}
```  

위 두 클래스의 객체를 생성한 코드는 정말로 간단해 졌다.
```java
MemberDao memberDao = new MemberDao();
MemberRegisterService registerService = new MemberRegisterService(memberDao);
ChangePasswordService changePwService = new ChangePasswordService(memberDao);
```

이제 MemberDao 대신 CachedMemberDao를 사용하도록 수정해보면 밑에 처럼 수정되는 부분은 한곳 뿐이다.
```java
MemberDao memberDao = new CachedMemberDao();
MemberRegisterService registerService = new MemberRegisterService(memberDao);
ChangePasswordService changePwService = new ChangePasswordService(memberDao);
```

__의존 객체를 주입하는 방식을 사용하면, 객체를 생성할 때 사용할 클래스를 한 곳만 변경하면 된다__  

DI를 사용하면 의존 객체를 직접 생성했던 방식에 비해 변경할 코드가 한 곳으로 집중되는 것을 알 수 있다.

다음에는 DI의 3가지 방법에 대해 알아보겠다.  
참고 : __초보 웹 개발자를 위한 스프링5 프로그래밍 입문__