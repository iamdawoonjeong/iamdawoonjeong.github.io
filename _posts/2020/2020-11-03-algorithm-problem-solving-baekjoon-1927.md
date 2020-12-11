---
layout: single
title: "[Problem Solving - Baekjoon] 1927 최소 힙"
date: 2020-11-03 23:22:00.000000000 +09:00
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
- heap
- baekjooon
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1927/"
---
# [Baekjoon Online Judge] 1927 최소 힙

## 문제
널리 잘 알려진 자료구조 중 **최소 힙**이라는 것이 있다. 최소 힙을 이용하여 다음과 같은 연산을 지원하는 프로그램을 작성하시오.

1. 배열에 자연수 x를 넣는다.
2. **배열에서 가장 작은 값을 출력하고, 그 값을 배열에서 제거**한다.

프로그램은 처음에 비어있는 배열에서 시작하게 된다.

### 입력
첫째 줄에 연산의 개수 N(1≤N≤100,000)이 주어진다. 다음 N개의 줄에는 연산에 대한 정보를 나타내는 정수 x가 주어진다. 만약 x가 자연수라면 배열에 x라는 값을 넣는(추가하는) 연산이고, x가 0이라면 배열에서 가장 작은 값을 출력하고 그 값을 배열에서 제거하는 경우이다. 입력되는 자연수는 2^31보다 작다.

### 출력
입력에서 0이 주어진 회수만큼 답을 출력한다. 만약 배열이 비어 있는 경우인데 가장 작은 값을 출력하라고 한 경우에는 0을 출력하면 된다.

### 예제
- input

```java
9
0
12345678
1
2
0
0
0
0
32
```

- output

```java
0
1
2
12345678
0
```

### 분류
- heap(최소힙)

## 풀이

### 문제 파악
- 노드 중 최소 값을 추출하는 [최소힙](http://dawoonjeong.com/algorithm-sort-heap/) 문제

```java
9   // n개의 정수 입력
0   // 0 이 입력된 경우 가장 작은 값 출력하고 제거. 배열이 비어있는 경우 0출력
12345678
1
2
0
0
0
0
32
```

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1927/Main.java)

- 최소 heap구조를 가진 PriortyQueue 선언

```java
PriorityQueue<Integer> pq = new PriorityQueue<Integer>();
```

- 0이 입력되면
	- 배열내 제일 작은수를 출력
	- 배열이 비어있으면 0 출력

- 입력된 수가 0이 아니면 queue에 추가   

```java
for (int i = 0; i < n; i++) {
    int number = Integer.parseInt(br.readLine());
	//0 이 입력되면
    if (number == 0 ) {

        if (pq.isEmpty()) {
			// 배열이 비어있으면 0출력
            System.out.println(0);
        }else {
			// 배열내 제일 작은 수를 출력
            System.out.println(pq.poll());
        }

    } else {
        pq.offer(number);
    }
}
```

---

#### references
<https://www.acmicpc.net/problem/1927>
