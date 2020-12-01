---
layout: single
title: "[Problem Solving - Baekjoon] 10539 수빈이와 수열"
date: 2020-12-01 21:20:00.000000000 +09:00
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
- baekjoon
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-10539/"
---
# [Baekjoon Online Judge] 10539 수빈이와 수열

## 문제
수빈이는 심심해서 수열을 가지고 놀고 있다. 먼저, 정수 수열 A를 쓴다. 그리고 그 아래에 정수 수열 A의 해당 항까지의 평균값을 그 항으로 하는 정수 수열 B를 쓴다.

예를 들어, 수열 A가 1, 3, 2, 6, 8이라면, 수열 B는 1/1, (1+3)/2, (1+3+2)/3, (1+3+2+6)/4, (1+3+2+6+8)/5, 즉, 1, 2, 2, 3, 4가 된다.

수열 B가 주어질 때, 수빈이의 규칙에 따른 수열 A는 뭘까?

### 입력
첫째 줄에는 수열 B의 길이만큼 정수 N(1 ≤ N ≤ 100)이 주어지고, 둘째 줄에는 수열 Bi를 이루는 N개의 정수가 주어진다. (1 ≤ Bi ≤ 109)

### 출력
첫째 줄에는 수열 A를 이루는 N개의 정수를 출력한다. (1 ≤ Ai ≤ 109)

### 예제1
- input

```java
1
2
```

- output

```java
2
```

### 예제2
- input

```java
4
3 2 3 5
```

- output

```java
3 1 5 11
```

### 예제3
- input

```java
5
1 2 2 3 4
```

- output

```java
1 3 2 6 8
```

### 분류
- 구현

## 풀이

### 문제 파악

- 입력된 수열 B로 수열 A를 복원하는 문제
- 수열 A를 구하는 산술식만 구하면 됨  
- 수열 A[0] = 수열 B[0] 과 같아 초기값 셋팅 해주고 진행

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem10539/Main.java)

- 수열 B (result[i]) = (항의 갯수(i+1) / 수열 A 의 수 (arr[i])) - 수열 B의 합 (sum)     

```java
result[0] = arr[0];  //초기값
int sum = result[0];
for (int i = 1; i < n; i++) {
    result[i] = (i+1)*arr[i] -  sum;
    sum += result[i];
}
```

---

#### references
<https://www.acmicpc.net/problem/10539>
