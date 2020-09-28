---
title   : "Entity Relationship Diagram"
categories : 
    - DB
tags : 
    - DataBase
sidebar:
    title: "DataBase"
    nav : sidebar-posts
---

ERD(Entity Relationship Diagram)란?  
__ERD는 말로서 되어있는 요구분석사항을 그림으로 그려내여 그 관계를 도출하는 것__  

관계형 데이터 모델은 실체(Entity), 속성(Attribute), 관계(Relationship)로 구성된 ERD로 표현된다.  

![ERD](/assets/img/database/ERD.png)


#### 개체(Entity)  
DB에 표현하려고 하는 유형, 무형의 객체(object)로써 서로 구별되는 것을 뜻한다. 이 개체는 현실 세계에 대해 사람이 생각하는 개념이나 정보의 단위로서 의미를 가지고 있다. 개체는 단독으로 존재할 수 있으며, 정보로서의 역할을 한다. 하나의 개체는 하나 이상의 속성(Attribute)로 구성되고 각 속성은 그 개체의 특성이나 상태를 기술 해준다. 네모로 표현한다.  


#### 속성(Attribute)  
이름을 가진, 데이타의 가장 작은 논리적 단위가 된다. 학생이란 개체에서 학번, 이름, 나이가 있다고 할때 학번, 이름, 나이가 속성이 된다. 원으로 표시한다.  

#### 관계(Relationship)  
개체들을 서로 연관시켜 어떤 의미를 나타내어 개체와 다름이 없다. 그러나 특성상 이 관계는 보통 무형적이고 다루기가 아주 복잡하다는 의미에서 별개의 요소로 취급되고 있다.  
예를 들어 학생과 교수 사이에는 "지도"라는 관계를 가진다. 이때 지도를 Relation Type이라 하며 속성을 가질 수 있다. 마름모로 표현된다.  





