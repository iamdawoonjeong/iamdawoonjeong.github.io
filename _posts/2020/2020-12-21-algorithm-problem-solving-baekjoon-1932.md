---
layout: single
title: "[Problem Solving - Baekjoon] 1932 정수 삼각형"
date: 2020-12-21 18:40:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-1932/"
---
# [Baekjoon Online Judge] 1932 정수 삼각형

## 문제
```    
        7
      3   8
    8   1   0
  2   7   4   4
4   5   2   6   5
```
위 그림은 크기가 5인 정수 삼각형의 한 모습이다.

맨 위층 7부터 시작해서 아래에 있는 수 중 하나를 선택하여 아래층으로 내려올 때, 이제까지 선택된 수의 합이 최대가 되는 경로를 구하는 프로그램을 작성하라. 아래층에 있는 수는 현재 층에서 선택된 수의 대각선 왼쪽 또는 대각선 오른쪽에 있는 것 중에서만 선택할 수 있다.

삼각형의 크기는 1 이상 500 이하이다. 삼각형을 이루고 있는 각 수는 모두 정수이며, 범위는 0 이상 9999 이하이다.

### 입력
첫째 줄에 삼각형의 크기 n(1 ≤ n ≤ 500)이 주어지고, 둘째 줄부터 n+1번째 줄까지 정수 삼각형이 주어진다.

### 출력
첫째 줄에 합이 최대가 되는 경로에 있는 수의 합을 출력한다.

### 예제

- input

```java
5
7
3 8
8 1 0
2 7 4 4
4 5 2 6 5
```

- output

```java
30
```

### 분류
- 동적 프로그래밍

## 풀이

### 문제 파악
1. 대각선 왼쪽, 대각선 오른쪽에 있는 것 중 큰 값을 선택 
2. 점화식  : dp[i][j] = Math.max(dp[i-1][j-1], dp[i-1][j]) + arr[i][j]

### 구현


[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1932/Main.java)

- 문제 입력 받기

```java
for (int i = 1; i < n+1; i++) {
    String[] input = br.readLine().split(" ");
    for (int j = 1; j < input.length+1; j++) {
        arr[i][j] = Integer.parseInt(input[j-1]);

    }
}
```

- 첫 col, row는 0으로 받아 둠

```java
0 0 0 0 0 0
0 7 0 0 0 0
0 3 8 0 0 0
0 8 1 0 0 0
0 2 7 4 4 0
0 4 5 2 6 5
```

- 계산해주면서  dp 에 넣기
- 첫col 첫row는 0으로 채워야  
- dp[i][j] = Math.max(dp[i-1][j-1], dp[i-1][j]) + arr[i][j] 이 계산식이 쉬움

```java
int[][] dp = new int[n+1][n+1];

for (int i = 1; i < n+1; i++) {
    for (int j = 1; j < n+1; j++) {
        dp[i][j] = Math.max(dp[i-1][j-1], dp[i-1][j]) + arr[i][j];
    }
}
```

- dp에 계산된 값이 아래와 같이 입력 됨

```java
0  0  0  0  0  0
0  7  0  0  0  0
0 10 15  0  0  0
0 18 16 15  0  0
0 20 25 20 19  0
0 24 30 27 26 24
```


- 마지막 줄의 최대값 출력

```java
int max = 0;
for (int i = 0; i < dp.length; i++) {
    max = Math.max(max, dp[n][i]);
}
```

---

#### references
<https://www.acmicpc.net/problem/1932>
