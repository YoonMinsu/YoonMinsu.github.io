---
title   : "@MappedSuperclass"
categories : 
    - jpa
tags : 
    - java
    - spring
    - jpa
sidebar:
    title: "JPA"
    nav : sidebar-posts
---  

앞서 학습한 상속 관계 매핑에서 상위 클래스와 하위 클래스를 모두 데이터베이스 테이블과 매핑했다.  

상위 클래스는 테이블과 매핑하지 않고 상위 클래스를 상속받는 하위 클래스 에게 매핑 정보만 제공하고 싶으면 `@MappedSuperclass` 애노테이션을 사용 하면 된다.  

`@MappedSuperclass`는 실제 테이블과 매핑되지 않는다. 단순히 매핑 정보를 상속할 목적으로만 사용된다.  

| MEMBER |
| ------ |
| ID(PK) |
| NAME   |
| EMAIL  |

| SELLER |
| ------ |
| ID(PK) |
| NAME   |
| EMAIL  |

회원가 판매자 두 개의 테이블이 있다고 가정해보자  

위 두 개의 테이블에는 ID와 NAME을 서로 가지고있어 공통된 속성이라 할 수 있다.  

![공통속성상속](/assets/img/JPA/공통속성상속.PNG)  

그럼 위 그림처럼 공통된 속성을 상위 클래스로 모으고 하위 클래스에서 상속받아 사용할 수 있다.  

```java
@MappedSuperclass
public class BaseEntity {
    
    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String name;
}

@Entity
public class Member extends BaseEntity{

    private String email;
}

@Entity
public class Seller extends BaseEntity{

    private String shopName;
}
```  

BaseEntity에는 객체들이 주로 사용하는 **공통 매핑 정보**를 정의했다.  

그리고 하위 엔티티들은 상속을 통해 BaseEntity의 매핑 정보를 상속받았다.  

BaseEntity는 테이블과 매핑할 필요가 없고 하위 엔티티들에게 공통으로 사용되는 매핑 정보만 제공하면 되므로 `@MappedSuperclass`를 사용했다.  

```java
// 저장
Member member = new Member();

member.setName("멤버 1");
member.setEmail("hello@jpa.com");

em.persist(member);
```

| ID  | NAME   | EMAIL         |
| --- | ------ | ------------- |
| 1   | 멤버 1 | hello@jpa.com |

Member 테이블의 ID를 member_id로 변경하고 싶다.  

상위 클래스로부터 상속받은 매핑 정보를 재정의하려면 `@AttributeOverride` 또는 `@AttributeOverrides`를 사용하면 된다. 애노테이션 이름이 직관적이라 무엇을 뜻하는지 바로 알 수 있다.  

```java
@Entity
@AttributeOverride(name = "id", column = @Column(name = "member_id"))
public class Member extends BaseEntity{

    private String email;
}
```  

상위 클래스(BaseEntity)로 부터 상속 받은 **id** 속성의 컬럼 명을 **member_id**로 변경하였다.  

위 애노테이션을 적용하고 저장하게 되면 아래의 테이블처럼 컬럼 명이 바뀌게 된다.  

| MEMBER_ID | NAME   | EMAIL         |
| --------- | ------ | ------------- |
| 1         | 멤버 1 | hello@jpa.com |  


둘 이상을 재정의 하려면 @AttributeOverrides 애노테이션을 사용하면 된다.  

```java
@Entity
@AttributeOverrides({
    @AttributeOverride(name = "id", column = @Column(name = "member_id")),
    @AttributeOverride(name = "name", column = @Column(name = "member_name"))
})
public class Member extends BaseEntity{

    private String email;
}
```  

@MappedSuperclass의 특징을 정리해 보면  

- 테이블과 매핑되지 않고 하위 클래스에 엔티티의 매핑 정보를 상속하기 위해 사용된다.
- @MappedSuperclass로 지정한 클래스는 엔티티가 아니므로 em.find()나 JPQL을 사용할 수 없다.
- 위의 예시에서 사용한 BaseEntity같은 상속을 목적으로 만든 클래스를 직접 생성해서 사용할 일은 거의 없다.
- 따라서 추상 클래스로 만드는 것을 권장한다.

@MappedSuperclass 애노테이션은 테이블과는 관계가 없고 단순히 **엔티티가 공통으로 사용하는 매핑 정보를 모아주는 역할을 할 뿐이다**  

---

## 출처  
- **자바 ORM 표준 JPA 프로그래밍 김영한 저**  
- **인프런: 자바 ORM 표준 JPA 프로그래밍 - 기본편**  