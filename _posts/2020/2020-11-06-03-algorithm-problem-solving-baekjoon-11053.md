---
layout: single
title: "[Problem Solving - Baekjoon] 11053 가장 긴 증가하는 부분 수열"
date: 2020-11-06 22:40:00.000000000 +09:00
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
- DP
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-11053/"
---
# [Baekjoon Online Judge] 11053 가장 긴 증가하는 부분 수열

## 문제
수열 A가 주어졌을 때, 가장 긴 증가하는 부분 수열을 구하는 프로그램을 작성하시오.

예를 들어, 수열 A = {10, 20, 10, 30, 20, 50} 인 경우에 가장 긴 증가하는 부분 수열은 A = {10, 20, 10, 30, 20, 50} 이고, 길이는 4이다.

### 입력
첫째 줄에 수열 A의 크기 N (1 ≤ N ≤ 1,000)이 주어진다.

둘째 줄에는 수열 A를 이루고 있는 Ai가 주어진다. (1 ≤ Ai ≤ 1,000)

### 출력
첫째 줄에 수열 A의 가장 긴 증가하는 부분 수열의 길이를 출력한다.

### 예제

- input

```java
6
10 20 10 30 20 50
```

- output

```java
4
```

### 분류
- 동적프로그래밍

## 풀이

### 문제 파악

- 이전 증가 값을 알아야 다음 증가값을 구할 수 있는 동적 프로그래밍


|           | (i=0) 10 | (i=1) 20 | (i=2) 10 | (i=3) 30 | (i=4) 20 | (i=5) 50 |
|:---------:|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|
| 초기 값     |    1     |    1     |  1       |  1       |  1       |  1       |
| (j=0) 10  |   **1**  |  **2**   |  1       |  **2**   |  **2**   |  **2**   |
| (j=1) 20  |     -    |    2     |  1       |  **3**   |  2       |  **3**   |
| (j=2) 10  |     -    |    -     |  -       |  3       |  2       |  3       |
| (j=3) 30  |     -    |    -     |  -       |  -       |  2       |  **4**   |
| (j=4) 20  |     -    |    -     |  -       |  -       |  -       |  4       |
| (j=5) 50  |     -    |    -     |  -       |  -       |  -       |  -       |


- i = 1 부터 시작해서 j = 0 ~ j < i 까지의 증가 값을 구함
- f(0) = 1, f(1) = 1  


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem11053/Main.java)

```java
dp[0] = 1;

for (int i = 1; i < n; i++) {
    dp[i] = 1;
    for (int j = 0; j < i; j++) {
        if (arr[j] < arr[i]) {
            dp[i] = Math.max(dp[i], dp[j]+1);
        }
    }
}

```

---

#### references
<https://www.acmicpc.net/problem/11053>
