---
title   : "퀵 정렬(Quick Sort)"
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

## 빠른 정렬, 퀵 정렬  

퀵 정렬은 `분할 정복(Divide and Conquer)`에 기반한 알고리즘이다.  

__1.__ 데이터 집합 내에서 임의의 기준 요소를 선택하고, 기준 요소보다 작은 요소들은 순서에 관계 없이 기준 요소의 왼편에, 큰 값은 오른편에 위치 시킨다.  
__2.__ 기준 값 왼쪽에는 기준 값보다 작은 값들이 모여 있고 오른쪽에는 기준 값보다 큰 값들이 모여 있다. 이렇게 나눈 데이터 집합들을 다시 1번 과정과 같이 임의의 기준 요소를 선택하고 같은 방법으로 데이터 집합을 분할한다.  
__3.__ 1과 2의 과정을 더 이상 데이터 집합을 나눌 수 없을 때까지 반복하면 정렬된 데이터 집합을 얻게 된다.  


```java
public class QuickSort {

    public static void swap( int[] arr, int a, int b ) {
        int temp = arr[ a ];
        arr[ a ] = arr[ b ];
        arr[ b ] = temp;
    }

    public static int partition( int[] arr, int start, int end ) {
        int pivot = arr[ start ];
        int left = start;
        int right = end;
        while( left < right ) {
            while( pivot < arr[ right ] ) {
                right = right - 1;
            }

            while( left < right && pivot >= arr[ left ] ) {
                left = left + 1;
            }
            swap( arr, left, right );
        }
        arr[ start ] = arr[ left ];
        arr[ left ] = pivot;
        return left;
    }

    public static void quickSort( int[] arr, int start, int end ) {

        if( start >= end ) {
            return;
        }
        int index = partition( arr, start, end );

        quickSort(arr, start, index - 1 );
        quickSort(arr, index + 1, end );
    }

    public static void main( String[] args ) {
        int arr[] = { 1,2,6,4,1,1,86,78,3,681,1 };

        quickSort(arr, 0, arr.length -1 );

        for( int value : arr ) {
            System.out.println( value );
        }
    }
}
```