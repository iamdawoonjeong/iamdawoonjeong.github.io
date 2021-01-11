---
layout: single
title: "[Problem Solving - Baekjoon] 9251 LCS"
date: 2020-11-09 22:06:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-9251/"
---
# [Baekjoon Online Judge] 9251 LCS

## 문제
LCS(Longest Common Subsequence, 최장 공통 부분 수열)문제는 두 수열이 주어졌을 때, 모두의 부분 수열이 되는 수열 중 가장 긴 것을 찾는 문제이다.

예를 들어, ACAYKP와 CAPCAK의 LCS는 ACAK가 된다.

### 입력
첫째 줄과 둘째 줄에 두 문자열이 주어진다. 문자열은 알파벳 대문자로만 이루어져 있으며, 최대 1000글자로 이루어져 있다.

### 출력
첫째 줄에 입력으로 주어진 두 문자열의 LCS의 길이를 출력한다.

### 예제

- input

```java
ACAYKP
CAPCAK
```

- output

```java
4
```

### 분류
- 동적프로그래밍

## 풀이

### 문제 파악

- 수열 중 가장 긴 것을 찾는 동적 프로그래밍 문제
- 첫째줄은 x축 둘째줄은 y축에 둠
- x와 y의 문자가 같으면 x-1, y-1 값의 +1
- x와 y의 문자가 다르면 x열 이전값, y열 이전 값과 비교하여 더 큰 값 가져오기


|   | 0 | C | A | P | C | A | K |
|:----:|:----:|:----:|:-----:|:-----:|:-----:|
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| A | 0 | 0 | 1 | 1 | 1 | 1 | 1 |
| C | 0 | 1 | 1 | 1 | 2 | 2 | 2 |
| A | 0 | 1 | 2 | 2 | 2 | 3 | 3 |
| Y | 0 | 1 | 2 | 2 | 2 | 3 | 3 |
| K | 0 | 1 | 2 | 2 | 2 | 3 | 4 |
| P | 0 | 1 | 2 | 3 | 3 | 3 | 4 |



### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem9251/Main.java)

```java
int[][] dp = new int[x.length+1][y.length+1];

dp[0][0] = 0;
for (int i = 1; i < x.length+1; i++) {
    for (int j = 1; j < y.length+1; j++) {

        if (x[i-1] == y[j-1]) {
            dp[i][j] = dp[i-1][j-1]+1;
        }else {
            dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
        }
    }
}

System.out.println(dp[x.length][y.length]);
```

---

#### references
<https://www.acmicpc.net/problem/9251>
