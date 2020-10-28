---
layout: single
title: "[Problem Solving - Baekjoon] 2751 수 정렬하기2"
date: 2020-10-22 21:10:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Problem Solving
tags:
- data structure
- algorithm
- sort
- recursive
- merge
- DAC
- baekjoon
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-2751/"
---
# [Baekjoon Online Judge] 2751 수 정렬하기2

## 문제
N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.

### 입력
첫째 줄에 수의 개수 N(1 ≤ N ≤ 1,000,000)이 주어진다. 둘째 줄부터 N개의 줄에는 숫자가 주어진다. 이 수는 절댓값이 1,000,000보다 작거나 같은 정수이다. 수는 중복되지 않는다.

### 출력
첫째 줄부터 N개의 줄에 오름차순으로 정렬한 결과를 한 줄에 하나씩 출력한다.

### 예제

- input

```java
5
5
4
3
2
1
```

- output

```java
1
2
3
4
5
```

### 분류
- 정렬


## 풀이

### 문제 파악
- 1,000,000개의 수를 2초 안에 정렬해야하는 문제
- 시간복잡도 O(NlogN)의 정렬알고리즘 이용하기
- [퀵](http://dawoonjeong.com/algorithm-sort-quick/), [병합](http://dawoonjeong.com/algorithm-sort-merge/), [힙](http://dawoonjeong.com/algorithm-sort-heap/) 정렬 이용하기(모두다 DAC로 재귀 용법을 이용)


### 구현

#### Merge Sort 구현해서 정렬

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2751/Main.java)

- 최악의 시간복잡도 O(NlogN)인 merge sort를 구현

```java
private static void sort(int[] arr, int left, int right) {

    if (left < right) {
        int mid = (left+right)/2;
        sort (arr, left, mid);
        sort (arr, mid+1, right);

        merge(arr, left, mid, right);
    }
}

private static void merge(int[] arr, int left, int mid, int right) {
    int sizeLeft = mid-left+1;
    int sizeRight = right-mid;

    int[] L = new int[sizeLeft];
    int[] R = new int[sizeRight];

    for (int i = 0; i < sizeLeft; i++) {
        L[i] = arr[left+i];
    }

    for (int j = 0; j < sizeRight; j++) {
        R[j] = arr[mid+1+j];
    }

    int i = 0;
    int j = 0;
    int k = left;

    while ( i < sizeLeft && j < sizeRight) {
        if( L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        }else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    while(i < sizeLeft) {
        arr[k] = L[i];
        i++;
        k++;
    }

    while(j < sizeRight) {
        arr[k] = R[j];
        j++;
        k++;
    }
}
```

#### Collections.sort() 이용

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2751/MainCollection.java)

- ArrayList 사용 : Arrays.sort() 사용시  **시간초과**로 실패  

```java
ArrayList<Integer> list = new ArrayList<Integer>();
```

- 정렬

```java
Collections.sort(list);
```

- 출력 : System.out.println() 사용시  **시간초과**로 실패

```java
OutputStreamWriter osw = new OutputStreamWriter(System.out);
BufferedWriter bw = new BufferedWriter(osw);

for (int i : list) {
   bw.write(i+"\n");
}           
```


### 결론
- 속도면에서는 mergesort가 좋으나 mergesort를 정해진 시간안에 구현하는 것은 어려울 듯하니 Collections.sort를 사용
- Arrays.sort()보다 Collecitons.sort()가 빠름

| 항목	   | Collections.sort() |  MergeSort |
|:--------:|:--------:|:--------:|
|  코드길이(Byte) |  1217    |   2207 	|
|  메모리(KB) 	 |  167284 	|  248284 	|
|  시간(ms) 	     |  1440	|  1012   	|


----

#### references
<https://www.acmicpc.net/problem/2751>
