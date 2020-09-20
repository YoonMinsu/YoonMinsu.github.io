---
title   : "Bean 등록 설정"
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

지금까지의 스프링 버전에서는 컴포넌트 및 다른 컴포넌트와의 관계를 나타내는 하나 이상의 XML파일을 사용해 빈을 상호 연결하도록 컨테이너에게 알려주었다.  

```xml
<bean id="inventoryService" class="com.example.InventoryService" />

<bean id="productService" class="com.example.ProductService" />
    <constructor-arg ref="inventoryService" />
</bean>
```  
위 xml에서는 재고서비스(InventoryService) Bean과 제품서비스(ProductService) Bean을 선언하여 생성자를 사용해 InventoryService 빈은 ProductService빈에 주입했다.  

현재 최신 버전의 스프링에서는 xml을 이용하는 것보다 자바 기반의 구성(Configuration)이 더 많이 사용된다.  

위 xml과 같은 자바 구성 클래스는 다음과 같다  
```java
@Configuration
public class ApplicationConfig {

    @Bean
    public InventorySercvice inventoryService() {
        return new InventoryService();
    }

    @Bean
    public ProductService productService() {
        return new ProductService(inventoryService());
    }
}
```  

아직 코드가 짧아서 차이가 없어 보이지만 엄청 길어진다면 확실히 자바 설정이 더 보기 편할 것 같다.  

자바 기반 구성은 xml에 비해 몇 가지 장점이 있다.  
- 컴파일러나 IDE를 통한 타입 검증이 가능하다.
- 자동완성과 같은 IDE의 지원 기능을 최대한 이용가능하다.
- 이해하기 쉽다
- 복잡한 Bean 설정이나 초기화 작업을 손쉽게 적용할 수 있다.  
- 

`@Configuration` 애노테이션은 각 Bean을 스프링 컨테이너에 제공하는 구성 클래스라는 것을 스프링에게 알려준다.  
구성 클래스의 메서드에는 `@Bean` 애노테이션이 지정되어 있으며, 이것은 각 메서드에서 반환되는 객체가 컨테이너의 Bean으로 추가되어야 한다는 것을 나타낸다.  

또한 스프링은 자동으로 컴포넌트들을 구성할 수 있는 자동-구성 기능이 존재해 애플리케이션을 빌드하는 데 필요한 별도의 구성 코드(xml이나 자바 설정)를 많이 줄여준다.  

자동-구성은 __자동 연결(Autowiring)과 컴포넌트 검색(Component scanning)__ 이라는 스프링 기법을 기반으로 한다.  
컴포넌트 검색을 사용하여 스프링은 자동으로 애플리케이션의 classpath에 지정된 컴포넌트를 찾은 후 스프링 컨테이너의 Bean으로 생성할 수 있다. 또한 스프링은 자동 연결을 사용하여 의존 관계가 있는 컴포넌트를 자동으로 다른 Bean에 주입한다.  



__출저: Spring in Action 5판__