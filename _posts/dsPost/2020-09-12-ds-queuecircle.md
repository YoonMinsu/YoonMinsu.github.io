---
title   : "원형 큐"
excerpt : "CircleQueue-FIFO"
categories : 
    - DataStructure
tags :
    - DataStructure
---

선형 큐의 단점을 보완한 원형 큐이다. 기존에 선형 큐는 front부분에 대해서 다시 활용할 수가 없어 메모리를 낭비한다는 단점이 있다.  
원형 큐는 큐의 맨 끝과 맨 처음이 연결된 형태의 구조이기 때문에 이미 꺼내어 사용한 큐의 앞부분에 다시 데이터르 저장하여 재사용이 가능한 형태이다.  

# 원형 큐 구현  
앞에 선형 큐와 기능은 동일하지만 내부 함수의 구현 방식이 달라졌다  


```Java
    public class CircleQueue {
        private int[] qArr;
        private int size;
        private int rear;
        private int front;

        public CircleQueue( int size ) {
            this.size = size;
            qArr = new int[ size ];
            front = 0;
            rear = 0;
        }

        public boolean isEmpty() {
            if ( rear == front ) {
                return true;
            } else {
                return false;
            }
        }

        public boolean isFull() {
            if ( front == ( rear + 1 ) % size ) {
                return true;
            } else {
                return false;
            }
        }

        public void enqueue( int value ) {
            if ( isFull() ) {
                throw new ArrayIndexOutOfException();
            }
            rear = ( rear + 1 ) % size;
            qArr[ rear ] = value;
        }

        public int dequeue() {
            if ( isEmpty() ) {
                throw new ArrayIndexOutOfException();
            }
            front = ( front + 1 ) % size;
            return qArr[ front ];
        }

        public int size() {
            return ( rear - front + size ) % size; 
        }

        public static void main(String[] args) {

        }
    }
```