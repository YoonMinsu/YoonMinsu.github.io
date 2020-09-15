---
title   : "컬렉션 프레임워크(Collection Framework)"
excerpt : "Collection"
categories : 
    - Java
tags : 
    - Java
    - Collection
sidebar:
    title: "Java"
    nav : sidebar-posts
---
![CollectionFramework](/assets/img/java/CF.PNG)

__CollectionFramework의 핵심 인터페이스와 특징__
![interface](/assets/img/java/interface.PNG)  

컬렉션 프레임워크의 모든 컬렉션 클래스들은 List, Set, Map 중의 하나를 구현하고 있으며, 구현한 인터페이스의 이름이 클래스의 이름이 포함되어있어서 이름만으로도 클래스의 특징을 쉽게 알 수 있도록 되어있다.  

그러나 __Vector, Stack, HashTable, Properties__ 와 같은 클래스들은 컬렉션 프레임워크가 만들어지기 이전부터 존재하던 것이기 때문에 컬렉션 프레임워크의 명명법을 따르지 않는다.  

Vector나 HashTable과 같은 기존의 컬렉션 클래스들은 호환을 위해, 설계를 변경해서 남겨두었지만 가능하면 사용하지 않는 것이 좋다. 새로 추가한 `ArrayList`와 `HashMap`을 사용하도록 하자.  

## Collection Interface
List와 Set의 상위 인터페이스인 Collection 인터페이스에는 다음과 같은 메서드들의 정의되어 있다.  
![method](/assets/img/java/method.PNG)  

Collection 인터페이스는 컬렉션 클래스에 저장된 데이터를 읽고, 추가하고 삭제하는 등 컬렉션을 다루는데 가장 기본적인 메서드들을 정의하고 있다.  

참고 : 자바의 정석 3rd Edition
