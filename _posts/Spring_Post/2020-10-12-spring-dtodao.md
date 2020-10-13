---
title   : "Spring web 계층"
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

![webLayer](/assets/img/spring/webLayer.png)  

### Web Layer  

- 흔히 사용하는 @Controller와 JSP/Freemarker 등의 뷰 템플릿 영역이다.  
- 필터(@Filter), 인터셉터, 컨트롤러 어드바이스(@ControllerAdvice)등 외부 요청에 대한 전반적인 영역을 의미한다.  

### Service Layer  

- @Service에 사용되는 서비스 영역이다.  
- Controller와 DAO의 중간 영역에서 사용된다.  
- @Transactional이 사용되어야 하는 영역이기도 하다.  

### Repository Layer  

- DataBase와 같이 데이터 저장소에 접근하는 영역이다.  
- DAO(Data Access Object)영역 이라고 생각하면 쉽다.  

### DTOs  

- DTO(Data Transger Object)는 **계층 간에 데이터 교환을 위한 객체**를 이야기 하며 DTOs는 이들의 영역을 의미한다.  
- 예를 들어 뷰 템플릿 엔진에서 사용될 객체나 Repository Layer에서 결과로 넘겨준 객체 등이 이들을 이야기 한다.  

### Domain Model  

- Domain이라 불리는 개발 대상을 모든 사람이 동일한 관점에서 이해할 수 있고 공유할 수 있도록 단순화 시킨 것을 도메인 모델이라 한다.  
- @Entity가 사용된 영역 역시 도메인 모델이라고 이해하면 된다.  
- 무조건 데이터베이스의 테이블과 관계가 있어야만 하는 것은 아니다. VO처럼 값 객체들도 이 영역에 해당하기 때문이다.  
- 비즈니스 로직을 처리하는 영역이다.  



---
__출처: 스프링 부트와 AWS로 혼자 구현하는 웹 서비스 | 이동욱 저__
