---
title   : "ArrayList"
excerpt : "Collection Framework-List"
categories : 
    - Java
tags : 
    - Java
    - List
---

ArrayList는 List인터페이스를 구현하기 때문에 데이터의 저장 순위가 유지되고 중복을 허용하는 특징을 가지고 있다.  
ArrayList는 기존의 Vector 클래스를 개선한 것으로 Vector와 구현원리와 기능적인 측면에서 동일하다고 할 수 있다.  
Vector는 기존에 작성된 소스와의 호환성을 위해 계속 남겨 두고 있을 뿐이기 때문에 가능하면 Vector보다는 ArrayList를 사용하는게 좋다.  
  

ArrayList는 Object배열을 이용해서 데이터를 순차적으로 저장한다. 첫 번째로 저장한 객체는 Object배열의 0번째 위치에 저장되고 그 다음에 저장하는 객체는 1번째 위치에 저장된다. 이런 식으로 순서대로 저장되며, 배열에 더 이상 저장할 공간이 없으면 보다 큰 새로운 배열을 생성해서 기존의 배열에 저장된 내용을 새로운 배열에 복사한 다음에 저장된다.  

```java
public class ArrayList extends AbstarctList implements
        List, RandomAccess, Cloneable, java.io.Serializable {
            transient Object[] elementData; // Object 배열
        ...
    }
```  

Object배열을 멤버변수로 선언하고 있어 선언된 배열의 타입이 모든 객체의 최고 조상인 Object이기 때문에 모든 종류의 객체를 담을 수 있다.  

__관련 메서드__  
![ListMethod1](/assets/img/java/ListMethod1.PNG)
![ListMethod2](/assets/img/java/ListMethod2.PNG)  

<br/>


__ArrayList 선언방법__
```java
List list = new ArrayList()                     // 타입 미설정 Object로 선언된다.
List<Member> members = new ArrayList<Member>(); // Member객체 사용가능
List<Integer> list = new ArrayList<Integer>();  // int타입만 가능하다.
List<Integer> list = new ArrayList<>();         // new 연산에서 타입 파라미터 생략가능
List<Integer> list = new ArrayList<>(10);       // 초기 용량 지정
```  

선언시 `List list = new ArrayList()`로 선언 후 임의의 값을 넣고 사용할 수 있지만. 이렇게 사용할 경우 값을 얻어오기 위해서는 캐스팅(Casting) 연산이 필요하고, 잘못된 타입으로 캐스팅을 한 경우에는 에러가 발생해 위와 같은 방식은 추천하지 않는다.  

ArrayList나 다른 컬렉션을 사용할 때에는 타입을 명시에 해주는게 좋다.  
JDK5.0 이후부터 자료형의 안전성을 위해 제네릭스(Generic)라는 개념이 도입되었다.  
`List<String> list = new ArrayList<>();` 라고 선언해주면 String객체들만 추가되고, 나머지 다른 타입의객체는 사용이 불가능하다.  
  
> 제네릭스는 선언할 수 있는 타입이 __객체 타입__ 이다.
> int는 기본 자료형이기 때문에 들어갈 수 없으므로
> int를 __객체화__ 시킨 Wrapper 클래스를 사용해야 한다.
  
Wrapper클래스가 뭔지는 나중에 포스트 하겠지만 간단하게 표만 정리해 둔다.
![wrapper](/assets/img/java/wrapper.PNG)  

<br/>

간단한 예제
```java
public class Main {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();

        // 반복문을 통해 1 ~ 10 까지 list에 값을 추가
        for (int i = 1; i <= 10; ++i) {
            list.add(i);
        }

        System.out.println(list.toString()); // [1,2,3,4,5,6,7,8,9,10]
        
        // 값 가져오기
        // ArrayList는 인덱스가 0부터 시작한다.
        list.get(5) // 5번째 index에 있는 값 6을 가져온다.

        // 값 삭제
        list.remove(5) // 5번쨰 index에 있는 값 6을 삭제

        // 값 삭제 후 리스트 데이터
        // [1,2,3,4,5,7,8,9,10] 
        // 해당 인덱스의 값이 삭제되면 그 값 뒤에있는 인덱스부터 마지막 인덱스까지 앞으로 1씩 당겨진다.

        // 모든 값 삭제
        // list.clear();

        // 해당 값이 리스트 내부에 있는지 확인
        if (list.contains(4)) {
            System.out.println("있음")
        } else {
            System.out.println("없음")
        }
    }
}
```  

참고 : 자바의 정석 3rd Edition