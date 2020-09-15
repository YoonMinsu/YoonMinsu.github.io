---
title   : "이중 연결 리스트"
excerpt : "Doubly Linked List"
categories : 
    - DataStructure
tags :
    - datastructure
---  

# 이중 연결 리스트  
단순 연결 리스트는 각 노드가 서로 연결되어 있지 않고 다음 노드만을 바라본다 하지만 이중 연결 리스트는 노드와 노드가 서로 연결되어 있는 구조이다.  
즉, 단순 연결 리스틑 한 쪽 방향으로 연결 되어 있고, 이중 연결 리스트는 쌍방향으로 연결되어 있다.  

![dl](/assets/img/ds/doubleLinkedList.PNG)  

prevNode는 이전 노드이고 nextNode는 다음 노드이다.  

이중 연결 리스트는 양방향으로 연결되어 있기 때문에 노드를 탐색하는 방향이 양쪽으로 가능하다는 것이다.  
단순 연결 리스트의 경우 리스트의 마지막에 있는 데이터를 가져오려면 head부터 순차적으로 탐색을 해야 하기 때문에 많은 연산을 필요로 한다.  
하지만 이중 연결 리스트는 처음부터 탐색 할 필요 없이 tail노드를 이용해 탐색을 하면 된다.  

이전 노드를 지정하기 위해 변수를 하나 더 사용해 메모리를 많이 사용한다는 점이 있다. 구현이 단순 연결 리스트에 비해 복잡하다.  
하지만 단순 연결 리스트에 비해 장점이 더 크기 때문에 많이 사용한다.  

### 노드 클래스
```java
public class DoubleLinkedList {
    private class Node {
        private Node prevNode;
        private Node nextNode;
        private Object data;

        public Node(Object data) {
            this.data = data;
            this.prevNode = null;
            this.nextNode = null;
        }
    } // end Node class

    private Node headNode;
    private Node tailNode;
    private Node size;

    public DoubleLinkedList() {
        size = 0;
        headNode = null;
        tailNode = null;
    }
}
```


### 데이터 추가

![add1](/assets/img/ds/addNode.PNG)  
![add2](/assets/img/ds/addNode1.PNG)  
새로운 노드를 생성한 후에 기존 노드간의 연결을 끊고 새로운 노드와 연결을 시켜준다.  

```java
/* 해당 위치의 노드를 가져오는 함수 */
public Node getNode(int index) {
    Node node;
    if (index > size / 2) {
        node = tailNode;
        for (int i = index; i < size; ++i) {
            node = node.prevNode;
        }
    } else {
        node = headNode;
        for (int i = 0; i < index; ++i) {
            node = node.nextNode;
        }
    }
    return node;
}

/* 리스트 가장 앞에 데이터를 추가하는 함수 */
public void addFirst(Object data) {
    Node newNode = new Node(data);

    if (headNode != null) {
        newNode.nextNode = headNode;
        headNode.prevNode = newNode;
    }

    headNode = newNode;
    if (headNode.nextNode == null) {
        tailNode = headNode;
    }
    size++;
}

/* 리스트 가장 뒤에 데이터를 추가하는 함수 */
public void addLast(Object data) {
    if (size == 0) {
        addFirst(data);
    } else {
        Node newNode = new Node(data);
        tailNode.nextNode = newNode;
        newNode.prevNode = tailNode;
        tailNode = newNode;
        size++;
    }
}

/* 리스트 중간에 데이터를 추가하는 함수 */
public void addMiddle(int index, Object data) {
    if (index == 0) {
        addFirst(data);
    } else if (index == size) {
        addLast(data);
    } else {
        Node newNode = new Node(data);
        Node prevNode = getNode(index - 1);
        Node nextNode = prevNode.nextNode;

        newNode.prevNode = prevNode;
        newNode.nextNode = nextNode;

        prebNode.nextNode = newNode;
        nextNode.prevNode = nextNode;
        size++;
    }
}
```  

### 데이터 삭제  
![del1](/assets/img/ds/remove.PNG)  
![del2](/assets/img/ds/remove2.PNG)  

```java
/* 리스트의 첫 번째 데이터 삭제 */
public Object removeFirst() {
    if (size == 0) {
        System.out.println("No Data");
        return null;
    }
    Node removeNode = headNode;
    headNode = null;
    headNode = removeNode.nextNode;
    headNode.prevNode = null;
    size--;
    return removeNode.data;
}

/* 리스트의 가장 마지막에 있는 데이터 삭제 */
public Object removeLast() {
    if (size == 0) {
        System.out.println("No Data");
        return null;
    }
    Node removeNode = tailNode;
    tailNode = null;
    tailNode = removeNode.prevNode;
    tailNode.nextNode = null;
    size--;
    return removeNode.data;
}

/* 리스트의 index위치에 있는 데이터 삭제 */
public Object removeMiddle(int index) {
    if (index == 0) {
        return removeFirst();
    } else if (index == size - 1) {
        return removeLast();
    } else {
        Node removeNode = getNode(indext);

        Node prevNode = removeNode.prevNode;
        Node nextNode = removeNode.nextNode;

        prevNode.nextNode = nextNode;
        nextNode.prevNode = prevNode;

        Object data = removeNode.data;
        removeNode = null;
        size--;
        return data;
    }
}
```
