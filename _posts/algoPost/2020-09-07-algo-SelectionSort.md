---
title   : "선택 정렬(Selection Sort)"
excerpt : "Sort"
categories : 
    - Algo
tags : 
    - algorithm
    - sort
---
![Selection](/assets/img/algorithm/Selection-sort.png)  

- 주어진 리스트 중에 최소값을 찾는다
- 그 값을 맨 앞에 위치한 값과 교체한다.
- 맨 처음 위치를 제외한 나머지 배열을 같은 방법으로 교체한다
- 하나의 원소만 남을 때까지 위의 3개 과정을 반복한다  

시간 복잡도는 O(n^2)을 가진다.


```java
package org.sort;

public class SelectionSort {

    public static void sort(int[] list) {
        int temp = 0;
        int minIndex = 0;
        for (int i = 0; i < list.length - 1; ++i) {
            minIndex = i;
            for (int j = i + 1; j < list.length; ++j) {
                if (list[j] < list[minIndex]) {
                    minIndex = j;
                } // end if
            }
            temp = list[minIndex];
            list[minIndex] = list[i];
            list[i] = temp;
        } // end for
    }

    public static void main(String[] args) {
        int[] arr = {1,5,6,7,23,5,9,7};

        sort(arr);

        for (int value : arr) {
            System.out.println(value);
        }
    }
}

```