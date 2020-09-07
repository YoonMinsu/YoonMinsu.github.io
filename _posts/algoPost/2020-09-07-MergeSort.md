---
title   : "병합 정렬(Merge Sort)"
excerpt : "Sort"
categories : 
    - Algods
tags : 
    - algorithm
    - sort
---
![merge](/assets/img/algorithm/merge.png)  

원소가 저장되어 있는 배열을 계속 쪼개서 길이가 1인 배열을 만들고, 그 이후 정렬하면서 병합하는 알고리즘이다.  

__병합 정렬의 단계__  
- __분할(Divide)__: 입력 배열을 같은 크기의 2개의 부분 배열로 분할한다.
- __정복(Conquer)__: 부분 배열을 정렬한다. 부분 배열의 크기가 충분히 작지 않으면 순환 호출을 이용하여 다시 분할 단계를 적용한다.
- __결합(Combine)__: 정렬된 부분 배열들을 하나의 배열에 합병한다.  

시간 복잡도는 항상 O(n logn)을 가진다.
```java
package org.sort;

public class MergeSort {

    /* Conquer */
    public static void merge(int[] list, int[] temp, int left, int mid, int right) {
        int i = left;       // 첫 번째 부분 배열의 시작 위치
        int j = mid + 1;    // 두 번째 부분 배열의 시작 위치
        int index = left;   // 임시 배열 temp에 정렬된 원소를 삽입할 위치

        // 각 부분 배열의 길이만큼 반복 해준다.
        while (i <= mid && j <= right) {
            // 왼쪽 부분 배열의 값이 작으면
            if (list[i] <= list[j]) {   
                // 임시 배열 temp에 삽입해준다.
                temp[index] = list[i++];
            } else {
                // 오른쪽 부분 배열의 값이 작으면 오른쪽 값을 temp에 삽입해준다.
                temp[index] = list[j++];
            }
            index = index + 1;
        } // while

        // 남아 있는 데이터를 삽입 해준다.
        while (i <= mid) {
            temp[index++] = list[i++];
        }

        while (j <= right) {
            temp[index++] = list[j++];
        }

        // 임시 배열에 정렬된 값을 원본 배열로 옮겨 준다.
        for (int v = left; v < index; ++v) {
            list[v] = temp[v];
        }
    }

    /* Divide */
    public static void sort(int[] list, int[] temp, int left, int right) {
        if (left < right) {
            // 중간 값
            int mid = (left + right) / 2;

            // left 값부터 중간 값까지 분할한다.
            // 최소 실행 될때는 원소가 혼나 남을 때까지 분할 한다.
            sort(list, temp, left, mid);

            // 중간 값 + 1 부터 right 값까지 분할한다.
            // 왼쪽 부분 배열이 끝날 경우 실행된다.
            sort(list, temp, mid + 1, right);

            // 분활된 왼쪽 그룹과 오른쪽 그룹을 merge함수를 호출해 정렬 & 병합 시킨다.
            merge(list, temp, left, mid, right);
        }
    }

    public static void main(String[] args) {
        int[] list = {38,27,43,3,9,82,10}; // 정렬 대상 배열
        int[] temp = new int[list.length]; // 임시 배열

        sort(list, temp, 0, list.length - 1);

        for (int value : list) {
            System.out.printf("%d ", value);
        }

    }
}
```