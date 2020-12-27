---
layout: single
title: "[Problem Solving - Baekjoon] 2167 2차원 배열의 합"
date: 2020-12-27 10:10:00.000000000 +09:00
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
- Cumulative Sum
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-2167/"
---
# [Baekjoon Online Judge] 2167 2차원 배열의 합

## 문제

### 입력
2차원 배열이 주어졌을 때 (i, j) 위치부터 (x, y) 위치까지에 저장되어 있는 수들의 합을 구하는 프로그램을 작성하시오. 배열의 (i, j) 위치는 i행 j열을 나타낸다.

### 출력
첫째 줄에 배열의 크기 N, M(1 ≤ N, M ≤ 300)이 주어진다. 다음 N개의 줄에는 M개의 정수로 배열이 주어진다. 배열에 포함되어 있는 수는 절댓값이 10,000보다 작거나 같은 정수이다. 그 다음 줄에는 합을 구할 부분의 개수 K(1 ≤ K ≤ 10,000)가 주어진다. 다음 K개의 줄에는 네 개의 정수로 i, j, x, y가 주어진다(i ≤ x, j ≤ y).

### 예제

- input

```java
2 3
1 2 4
8 16 32
3
1 1 2 3
1 2 1 2
1 3 2 3
```

- output

```java
63
2
36
```

### 분류
- 누적합
- 다이나믹 프로그래밍

## 풀이

### 문제 파악

- arr 행렬 입력받기

|         |          |          |
|:-------:|:--------:|:--------:|
| (1,1) 1 | (1,2) 2  | (1,3) 4  |
| (2,1) 8 | (2,2) 16 | (2,3) 32 |


- 더해야할 좌표 입력 받기
- (1,1) ~ (2,3) : 1+2+4+8+16+32 =  63
- (1,2) ~ (1,2) : 2
- (1,3) ~ (2,3) : 4+8+16+32 = 60


- dp : 누적합으로 만들기  
- 누적합 계산식 : dp[i] [j] = dp[i-1] [j] + dp[i] [j-1]- dp[i-1] [j-1] + arr[i] [j

|          |          |          |
|:--------:|:--------:|:--------:|
| (1,1) 1  | (1,2) 3  | (1,3) 7  |
| (2,1) 9  | (2,2) 27 | (2,3) 63 |

- 누적 합으로 계산 하기 dp[x] [y] - dp[i-1] [y] - dp[x] [j-1] + dp [i-1] [j-1]
- (1,1) ~ (2,3) : dp[2] [3] - dp[0] [3] - dp[2] [0] + dp[0] [0] = 63 - 0 - 0 + 0 = 63
- (1,2) ~ (1,2) : dp[1] [2] - dp[0] [2] - dp[1] [1] + dp[0] [1] = 3 - 0 - 1 + 0 = 2
- (1,3) ~ (2,3) : dp[2] [3] - dp[0] [3] - dp[2] [2] + dp[0] [2] = 63 - 0 - 27 + 0 = 32


### 구현


[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2167/Main.java)


- 부분 합으로 dp를 채우기

```java
int[][] dp = new int[n+1][m+1];
for (int i = 1; i < n+1; i++) {
    for (int j = 1; j < m+1; j++) {
        dp[i][j] = dp[i-1][j] + dp[i][j-1]- dp[i-1][j-1] + arr[i][j];
    }
}
```

- 구할 범위를 계산해주기

```java
int k = Integer.parseInt(br.readLine());
int[] result = new int[k];
for (int p = 0; p < k; p++) {
    String[] input = br.readLine().split(" ");
    int i = Integer.parseInt(input[0]);
    int j = Integer.parseInt(input[1]);
    int x = Integer.parseInt(input[2]);
    int y = Integer.parseInt(input[3]);
    result[p]= dp[x][y] - dp[i-1][y] - dp[x][j-1] + dp[i-1][j-1];
}       
```

---

#### references
<https://www.acmicpc.net/problem/2167>
