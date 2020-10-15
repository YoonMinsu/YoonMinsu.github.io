---
title   : "persistence.xml 설정"
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

JPA는 persistence.xml을 사용해서 필요한 설정 정보를 관리한다.  

설정이 **META-INF/persistence.xml (표준 경로)** 클래스 패스 경로에 있으면 별도의 설정 없이 JPA가 인식할 수 있다.  

```xml
<?xml version="1.0" encoding="UTF-8"?>
<persistence version="2.2"
 xmlns="http://xmlns.jcp.org/xml/ns/persistence" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence http://xmlns.jcp.org/xml/ns/persistence/persistence_2_2.xsd">
    <persistence-unit name="hello">
        <properties>
        <!-- 필수 속성 -->
        <property name="javax.persistence.jdbc.driver" value="org.h2.Driver"/>
        <property name="javax.persistence.jdbc.user" value="sa"/>
        <property name="javax.persistence.jdbc.password" value=""/>
        <property name="javax.persistence.jdbc.url" value="jdbc:h2:tcp://localhost/~/test"/>
        <property name="hibernate.dialect" value="org.hibernate.dialect.H2Dialect"/>

        <!-- 옵션 -->
        <property name="hibernate.show_sql" value="true"/>
        <property name="hibernate.format_sql" value="true"/>
        <property name="hibernate.use_sql_comments" value="true"/>
        <!--<property name="hibernate.hbm2ddl.auto" value="create" />-->
        </properties>
    </persistence-unit>
</persistence> 
```  

설정 파일은 `<persistence>`로 시작한다. 이곳에 XML 네임스페이스와 사용할 버전을 지정해 준다.  

JPA 설정은 영속성 유닛(persistence-unit)이라는 것부터 시작하는데 일반적으로 연결 할 데이터베이스 하나당 하나의 영속성 유닛을 등록한다.  

`<persistence-unit name="hello">`  

영속성 유닛에는 고유한 이름을 부여해야 하는데 위 예시에서는 hello라는 이름을 사용했다.  

위 예시에서 사용한 속성을 살펴보자  

JPA 표준 속성   
**javax.persistence.jdbc.driver**: JDBC 드라이버
**javax.persistence.jdbc.user**: DB 접속 아이디
**javax.persistence.jdbc.password**: DB 접속 비밀번호
**javax.persistence.jdbc.url**: DB 접속 URL  

하이버네이트 속성  
**hibernate.dialect**: 데이터베이스 방언(Dialect) 설정


이름이 javax.persistence로 시작하는 속성은 JPA 표준 속성으로 특정 구현체에 종속되지 않는다.  

반면에 hiberante로 시작하는 속성은 하이버네이트 전용 속성이므로 하이버네이트에서만 사용할 수 있다.  

위에서 사용한 속성 대부분은 데이터베이스에 연결하기 위한 설정이다. 여기서 중요한 속성은 데이터베이스 방언을 설정하는 **hibernate.dialect** 이다.  


## 데이터베이스 방언  

![dialect](/assets/img/JPA/dialect.PNG)  

JPA는 특정 데이터베이스에 종속적이지 않은 기술이다. 따라서 다른 데이터베이스로 쉽게 교체할 수 있다.  

그런데 각각의 데이터베이스가 제공하는 SQL은 문법과 함수가 서로 차이가 있다.  

ex) 데이터 타입, 함수명, 페이징 처리 등  

이처럼 **SQL 표준을 지키지 않거나 특정 데이터베이스만의 고유한 기능을 JPA에서는 방언(Dialect)**라고 한다.  

개발자가 특정 데이터베이스에 종속되는 기능을 많이 사용하면 나중에 데이터베이스를 교체하기가 어렵다. 하이버네이트를 포함한 대부분의 JPA 구현체들은 이런 문제를 해결하기 위해 다양한 데이터베이스 방언 클래스를 제공한다.  

개발자는 JPA가 제공하는 표준 문법에 맞추어 JPA를 사용하면 된다. 특정 데이터베이스에 의존적인 SQL은 데이터베이스 방언이 처리해준다. 따라서 데이터베이스가 변경되어도 애플리케이션 코드를 변경할 필요 없이 데이터베이스 방언만 교체해주면 된다.  


위에서 나온 속성과 옵션을 자세하게 알고 싶다면 문서를 찾아보자  
참고: <https://docs.jboss.org/hibernate/stable/orm/userguide/html_single/Hibernate_User_Guide.html#configurations>  

---

#### 출처  
- **자바 ORM 표준 JPA 프로그래밍 김영한 저**  
- **인프런: 자바 ORM 표준 JPA 프로그래밍 - 기본편**  
