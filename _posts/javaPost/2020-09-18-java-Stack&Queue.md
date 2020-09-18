---
title   : "스택과 큐"
excerpt : "Collection Framework-Stack & Queue"
categories : 
    - Java
tags : 
    - Java
    - List
sidebar:
    title: "Java"
    nav : sidebar-posts
---  

## Stack & Queue  

개념과 특징  

![stackQueue](/assets/img/java/stackQueue.PNG)  

__스택__: 마지막에 저장한 데이터를 가장 먼저 꺼내게 되는(LIFO, Last in First Out) 구조  
__큐__  : 처음에 저장한 데이터를 가장 먼저 꺼내게 되는(FIFO, First in First Out) 구조  

스택의 경우 `0, 1, 2`의 순서로 데이터를 넣었다면 `2, 1, 0`의 순서로 꺼내게된다. 넣은 순서와 꺼낸 순서가 뒤집어진다.  
큐는 `0, 1, 2`의 순서로 데이터를 넣었다면 꺼낼 때 역시 `0, 1, 2`의 순서로 꺼내게 된다. 순서의 변경 없이 먼저 넣은 것을 꺼내게 된다.  

```java
// 선언 방법
Stack<type> stack = new Stack<>();
Queue<type> queue = new LinkedList<>();
```  
자바에서는 스택을 `Stack 클래스`로 구현하여 제공하고 있지만, 큐는 `Queue 인터페이스`로만 정의해 놓았을 뿐 별도의 클래스를 제공하고 있지 않다.  

__Stack의 메서드__  
![stackMethod](/assets/img/java/stackMethod.PNG)  


__Queue의 메서드__  
![queueMethod](/assets/img/java/queueMethod.PNG)  


```java
import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;

public class Main {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();
        Queue<Integer> queue = new LinkedList<>();

        for (int i = 1; i <= 5; ++i) {
            stack.push(i);
            queue.offer(i);
        } // end for

        System.out.println("==Stack==");
        while (!stack.empty()) {
            System.out.println(stack.pop());
        }

        System.out.println("==Queue==");
        while (!queue.isEmpty()) {
            System.out.println(queue.poll());
        }
    }
}
```  

![result](/assets/img/java/result.PNG)  

스택과 큐에 각각 1, 2, 3, 4, 5를 같은 순서로 넣고 꺼내었을 때의 결과가 다른 것을 알 수 있다.  
큐는 먼저 넣은 것이 먼저 꺼내지는 구조(FIFO)이기 때문에 넣을 때와 같은 순서이다.  
스택은 먼저 넣은 것이 나중에 꺼내지는 구조(LIFO)이기 때문에 넣을 떄의 순서와 반대로 꺼내진 것을 알 수 있다.  

__스택과 큐의 활용__  

__스택__: 수식 계산, 수식 괄호 검사, 워드프로세서의 undo/redo, 웹 브라우저의 뒤로가기/앞으로가기 등  
__큐__  : 최근 사용 문서, 인쇄작업 대기 목록, 버퍼(buffer) 등  

### 참고 : 자바의 정석 3rd Edition