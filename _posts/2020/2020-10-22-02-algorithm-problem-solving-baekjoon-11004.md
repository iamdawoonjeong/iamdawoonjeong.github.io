---
layout: single
title: "[Problem Solving - Baekjoon] 11004 K번째 수"
date: 2020-10-22 21:20:00.000000000 +09:00
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
- quick
- recursive
- baekjoon
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-11004/"
---
# [Baekjoon Online Judge] 11004 K번째 수

## 문제
수 N개 A1, A2, ..., AN이 주어진다. A를 오름차순 정렬했을 때, 앞에서부터 K번째 있는 수를 구하는 프로그램을 작성하시오.

### 입력
첫째 줄에 N(1 ≤ N ≤ 5,000,000)과 K (1 ≤ K ≤ N)이 주어진다.

둘째에는 A1, A2, ..., AN이 주어진다. (-109 ≤ Ai ≤ 109)

### 출력
A를 정렬했을 때, 앞에서부터 K번째 있는 수를 출력한다.


### 예제
- input

```java
5 2
4 1 2 3 5
```

- output

```java
2
```

### 분류
- 정렬


## 풀이

### 문제 파악

- [퀵](http://dawoonjeong.com/algorithm-sort-quick/), [병합](http://dawoonjeong.com/algorithm-sort-merge/), [힙](http://dawoonjeong.com/algorithm-sort-heap/) 정렬 이용하기(모두다 DAC로 재귀 용법을 이용)


### 구현

#### Quick Sort 구현해서 정렬
- Merge Sort를 써도 되나 지난 문제에서 썼으니 이번엔 Quick Sort 이용

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem11004/Main.java)

```java
private static int[] sort(int[] arr, int start, int end) {
    int left = start;
    int right = end;

    int pivot = arr[(left+right)/2];

    while(left <= right) {
        while( arr[left] < pivot) {
            left++;
        }

        while (arr[right] > pivot) {
            right--;
        }

        if (left <= right) {
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;

            left++;
            right--;
        }
    }

    if(start < right) {
        sort (arr, start, right);
    }

    if (left < end) {
        sort(arr, left, end);
    }

    return arr;
}
```

#### Collections.sort() 이용

- StringTokenizer() 사용 : br.readline().split(" ") 시간초과로 실패

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem11004/MainSort.java)

```java
StringTokenizer st = new StringTokenizer(br.readLine());
```

- LinkedList<Integer> 사용 : Arrays.sort(arr) 시간초과로 실패

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem11004/MainCollection.java)

```java
LinkedList<Integer> list = new LinkedList<Integer>();
```  



### 결론
- QuickSort가 Collecions.sort()에 비해 속도, 메모리에서 훨씬 효율이 좋은 문제
- Collecitons.sort()가 시간내에 성공 할 수 있다면 구현 하는 것이 쉬우므로 이용

| 항목	   | Collections.sort() |  QuickSort |
|:--------:|:--------:|:--------:|
|  코드길이(Byte) |  1059    |   1677 	|
|  메모리(KB) 	 |  785724 	|  551924 	|
|  시간(ms) 	     |  4928	|  1832   	|


----

#### references
<https://www.acmicpc.net/problem/11004>
