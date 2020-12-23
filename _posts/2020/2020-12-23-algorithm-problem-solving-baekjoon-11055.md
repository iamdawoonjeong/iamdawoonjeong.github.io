---
layout: single
title: "[Problem Solving - Baekjoon] 11055 가장 큰 증가 부분 수열"
date: 2020-12-23 15:05:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-11055/"
---
# [Baekjoon Online Judge] 11055 가장 큰 증가 부분 수열

## 문제
수열 A가 주어졌을 때, 그 수열의 증가 부분 수열 중에서 합이 가장 큰 것을 구하는 프로그램을 작성하시오.

예를 들어, 수열 A = {1, 100, 2, 50, 60, 3, 5, 6, 7, 8} 인 경우에 합이 가장 큰 증가 부분 수열은 A = {1, 100, 2, 50, 60, 3, 5, 6, 7, 8} 이고, 합은 113이다.

### 입력
첫째 줄에 수열 A의 크기 N (1 ≤ N ≤ 1,000)이 주어진다.

둘째 줄에는 수열 A를 이루고 있는 Ai가 주어진다. (1 ≤ Ai ≤ 1,000)

### 출력
첫째 줄에 수열 A의 합이 가장 큰 증가 부분 수열의 합을 출력한다.

### 예제

- input

```java
10
1 100 2 50 60 3 5 6 7 8
```

- output

```java
113
```

### 분류
- 다이나믹프로그래밍

## 풀이

### 문제 파악
- [11053 가장 긴 증가하는 부분 수열](http://dawoonjeong.com/algorithm-problem-solving-baekjoon-11053/) 와 유사한 문제
- 수열의 합을 구해야함
- dp[i] = Math.max(dp[i], dp[j]+arr[i])


|           | (i=0)  1 | (i=1) 100 | (i=2) 2 | (i=3) 50 | (i=4) 60 | (i=5) 3 | (i=6) 5 | (i=7) 6 | (i=8) 7 | (i=9) 8 |
|:---------:|:--------:|:---------:|:-- ----:|:--------:|:--------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|           |    1     |   100     |  2      |  50      |  60      |  3      |  5      |  6      | 7       |  8      |
| (j=0)   1 |    1     |   101     |  3      |  51      |  61      |  4      |  6      |  7      | 8       |  9      |
| (j=1) 100 |    -     |    -      |  3      |  51      |  61      |  4      |  6      |  7      | 8       |  9      |
| (j=2)   2 |    -     |    -      |  -      |  53      |  63      |  6      |  8      |  9      | 10      | 11      |
| (j=3)  50 |    -     |    -      |  -      |  -       |  113     |  6      |  8      |  9      | 10      | 11      |
| (j=4)  60 |    -     |    -      |  -      |  -       |  -       |  -      |  8      |  9      | 10      | 11      |
| (j=5)  3  |    -     |    -      |  -      |  -       |  -       |  -      |  11     |  12     | 13      | 14      |
| (j=6)  5  |    -     |    -      |  -      |  -       |  -       |  -      |  -      |  17     | 18      | 19      |
| (j=7)  6  |    -     |    -      |  -      |  -       |  -       |  -      |  -      |  -      | 24      | 25      |
| (j=8)  7  |    -     |    -      |  -      |  -       |  -       |  -      |  -      |  -      | -       | 32      |
| (j=9)  8  |    -     |    -      |  -      |  -       |  -       |  -      |  -      |  -      | -       | -       |



### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem11055/Main.java)

```java
for (int i = 1; i < n; i++) {
    dp[i] = arr[i];
    for (int j = 0; j < i; j++) {
        if (arr[j] < arr[i]) {
            dp[i] = Math.max(dp[i], dp[j]+arr[i]);
        }
    }
}     
```


---

#### references
<https://www.acmicpc.net/problem/11055>
