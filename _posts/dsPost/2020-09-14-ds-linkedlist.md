---
title   : "단순 연결 리스트"
excerpt : "Simple Linked List"
categories : 
    - DataStructure
tags :
    - datastructure
    - list
sidebar:
    title: "DataStructure"
    nav : sidebar-posts
---

# Simple Linked List  
가장 단순한 연결 리스트의 형태로 각 노드들은 다음 노드를 가리키는 하나의 참조만을 가진다.  
다음 노드의 참조밖에 가지고 있지 않으므로 노드의 접근은 한 방향으로만 가능하다.  


![LinkedList](/assets/img/ds/LinkedList.PNG)  

## 노드 클래스
```java
    public class LinkedList {
        private Node headNode;
        private int size;

        private class Node {
            private Node nextNode;
            private Object data;

            public Node() {}
            public Node(Object data) {
                // 새로 추가한 Node의 nextNode 초기값은 null로 설정한다.
                this.data = data;
                this.nextNode = null;
            }
        }
    }
```

## 특정 노드의 값 가져오기 및 출력하기
```java
    public Object get(int index) {
        return getNode(index).data;
    }

    public Node getNode(int index) {
        Node node = headNode;
        for (int i = 0; i < index; ++i) {
            node = node.nextNode;
        }
        return node;
    }
```

## 노드 삽입
```java
    public void addFirst(Object data) {
        // 새로운 노드 생성
        Node newNode = new Node(data);

        // 새로운 노드의 다음 노드는 헤드 노드를 가리킨다.
        newNode.nextNode = headNode;

        // 헤드노드는 새로운 노드를 가리키게 한다.
        headNode = newNode;
        size++;
    }

    public void add(int index, Object data) {
        // 새로운 노드 생성
        Node newNode = new Node(data);
        if (index == 0) {
            addFirst(data);
        } else {
            // 삽입하려는 위치의 전에 있는 노드를 구해온다.
            Node prevNode = getNode(index - 1);
            
            // 삽입하려는 위치 다음에 있는 노드를 구해온다.
            Node nextNode = prevNode.nextNode;
            
            // 삽입하려는 위치 전에 있는 노드는 새로 생성된 노드를 가리킨다.
            prevNode.nextNode = newNode;

            // 새로 생성된 노드는 삽입하려는 위치 다음에 있는 노드를 가리킨다/
            newNode.nextNode = nextNode;
            size++;
        }
    }

    public void addLast(Object data) {
        add(size, data);
    }
```

![insert1](/assets/img/ds/addFirst.PNG)  
![insert2](/assets/img/ds/addFirst2.PNG)  

## 데이터 삭제  
```java
    public Object removeFirst() {
        // 가장 처음에 있는 데이터를 삭제하는 함수이므로 삭제하려는 노드를 헤드노드로 지정한다.
        Node removeNode = headNode;

        // 헤드 노드를 유지하기 위해 헤드는 노드는 삭제하려는 노드의 다음 노드를 가리킨다.
        headNode = removeNode.nextNode;

        // 삭제하려는 데이터
        Object removeData = removeNode.data;

        // 노드 삭제
        removeNove = null;
        size--;
        return removeData;
    }
```    

```java
    public Object remove(int index) {
       if (index == 0) {
           return removeFirst();
       } else {
           // 삭제 하려는 위치 전 노드를 구해온다.
           Node prevNode = getNode(index - 1);

           // 삭제 하려는 노드를 구해온다.
           Node removeNode = prevNode.nextNode;

           // 삭제하려는 노드의 전 노드를 삭제하는 노드의 다음 노드를 가리키게 한다.
           prevNode.nextNode = removeNode.nextNode;

           Object removeData = removeNode.data;

           // 노드 삭제
           removeNode = null;
           size--;
           return removeData;
       }
    }

    public Object removeLast() {
        return removeMiddle(size - 1);
    }
```  
![delete1](/assets/img/ds/del1.PNG)  
![delete2](/assets/img/ds/del2.PNG)  

## 모든 데이터 출력  
```java
    public void printAllNode() {
        Node node = headNode;
        if (node == null) {
            System.out.println("No Data");
        } else {
            System.out.print("[" + node.data);
            for (int i = 1; i < size; ++i) {
                node = node.nextNode;
                System.out.print(" -> " + node.data);
            }
            System.out.println("]");
        }
    }
```
