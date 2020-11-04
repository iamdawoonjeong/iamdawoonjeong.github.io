---
layout: single
title: "[Problem Solving - Baekjoon] 1715 카드 정렬하기"
date: 2020-11-04 22:12:00.000000000 +09:00
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
- queue
- baekjoon
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1715/"
---
# [Baekjoon Online Judge] 1715 카드 정렬하기

## 문제
정렬된 두 묶음의 숫자 카드가 있다고 하자. 각 묶음의 카드의 수를 A, B라 하면 보통 두 묶음을 합쳐서 하나로 만드는 데에는 A+B 번의 비교를 해야 한다. 이를테면, 20장의 숫자 카드 묶음과 30장의 숫자 카드 묶음을 합치려면 50번의 비교가 필요하다.

매우 많은 숫자 카드 묶음이 책상 위에 놓여 있다. 이들을 두 묶음씩 골라 서로 합쳐나간다면, **고르는 순서에 따라서 비교 횟수가 매우 달라진다.** 예를 들어 10장, 20장, 40장의 묶음이 있다면 10장과 20장을 합친 뒤, 합친 30장 묶음과 40장을 합친다면 (10+20)+(30+40) = 100번의 비교가 필요하다. 그러나 10장과 40장을 합친 뒤, 합친 50장 묶음과 20장을 합친다면 (10+40)+(50+20) = 120 번의 비교가 필요하므로 덜 효율적인 방법이다.

**N개의 숫자 카드 묶음의 각각의 크기가 주어질 때, 최소한 몇 번의 비교가 필요한지를 구하는 프로그램을 작성하시오.**

### 입력
첫째 줄에 N이 주어진다. (1≤N≤100,000) 이어서 N개의 줄에 걸쳐 숫자 카드 묶음의 각각의 크기가 주어진다.

### 출력
첫째 줄에 최소 비교 횟수를 출력한다. (21억 이하)

### 예제
- input

```java
3
10
20
40
```

- output

```java
100
```

### 분류
- Queue

## 풀이

### 문제 파악
- 문제를 잘 읽어보면, 크기가 작은 숫자 카드 묶음들을 먼저 합친 것이 비교 횟수가 제일 적음
- 작은 카드 부터 비교 해야함으로 우선순위 큐를 사용
- [최소힙](http://dawoonjeong.com/algorithm-sort-heap/) 기법으로 작은 수를 root에 놓고 작은 수들 끼리 먼저 dequeue후 더한 합을 inqueue
- 작은 수들 끼리 먼저 dequeue후 더한 합을 inqueue를 반복하여 최종 노드가 1개 남을 때까지 반복

```java
3  //n 개의 카드
10 // 카드 숫자
20
40
```



- queue 에 모든 숫자를 넣음
- 10과 20을 poll() 하기

```java
     10
    /   \
  20    40

비교횟수 : 0
```

- 더한 합을 다시 offer() 로 넣음 (10 + 20 = 30)

```java
     30
    /   
  40

비교횟수 : 10 + 20 = 30  
```

- 30과 40을 poll() 한 후, 더한 합을 다시 offer() 로 넣음 (30+40 = 70)

```java
    70

비교횟수 : 10 + 20 + 30 + 40 = 100
```


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1715/Main.java)

- PriorityQueue 선언

```java
PriorityQueue<Integer> pq = new PriorityQueue<Integer>();
```

- queue 사이즈가 1이 아닐 때까지 2개의 숫자 빼서 더한 후 다시 넣는 과정 반복

```java  
int result = 0;
while ( !(pq.size() == 1)) {
    int a = pq.poll();
    int b = pq.poll();
    int sum = a+b;
    result += sum;
    pq.offer(sum);
}

System.out.println(result);
```

---

#### references
<https://www.acmicpc.net/problem/1715>
