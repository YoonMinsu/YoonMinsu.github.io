---
title   : "삽입 정렬(Insertion Sort)"
excerpt : "Sort"
categories : 
    - Algorithm
tags : 
    - algorithm
    - sort
sidebar:
    title: "Algorithm"
    nav : sidebar-posts
---

![insertion](/assets/img/algorithm/insertion-sort.PNG)  
차례로 범위를 늘려가며 정렬하는 알고리즘으로, 하나의 값을 선정하고 해당 값을 자신보다 작은 요소를 찾을 때까지 이동하면서 자리를 교환한다. 배열이 길어질 수록 효율이 떨어지지만, 버블 정렬에 비해 좀 더 빠르며 버블정렬과 마찬가지로 구현이 단순하다.  

삽입 정렬은 선택된 값보다 앞에 있는 원소들을 비교하는 것이기 때문에,  
첫 시작은 배열의 두 번째 원소부터 시작한다(index = 1)
시간 복잡도는 __O(n^2)__ 을 가진다.
```java
package org.sort;

public class InsertionSort {
    public static void sort(int[] list) {
        for (int index = 1; index < list.length; ++index) {
            int temp = list[index];
            int aux  = index - 1;
            while (aux >= 0 && list[aux] > temp) {
                list[aux + 1] = list[aux];
                aux = aux - 1;
            }
            list[aux + 1] = temp;
        }
    }
    public static void main(String[] args) {
        int[] list = {1,5,6,7,8,9,1,8};

        sort(list);

        for (int value : list) {
            System.out.println(value);
        }

    }
}
```
