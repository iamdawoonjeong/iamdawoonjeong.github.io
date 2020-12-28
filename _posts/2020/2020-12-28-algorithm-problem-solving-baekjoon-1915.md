---
layout: single
title: "[Problem Solving - Baekjoon] 1915 가장 큰 정사각형"
date: 2020-12-28 19:10:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-16675/"
---
# [Baekjoon Online Judge] 1915 가장 큰 정사각형

## 문제
n×m의 0, 1로 된 배열이 있다. 이 배열에서 1로 된 가장 큰 정사각형의 크기를 구하는 프로그램을 작성하시오.

0	1	0	0
0	1	1	1
1	1	1	0
0	0	1	0

위와 같은 예제에서는 가운데의 2×2 배열이 가장 큰 정사각형이다.

### 입력
첫째 줄에 n, m(1 ≤ n, m ≤ 1,000)이 주어진다. 다음 n개의 줄에는 m개의 숫자로 배열이 주어진다.

### 출력
첫째 줄에 가장 큰 정사각형의 넓이를 출력한다.

### 예제

- input

```java
4 4
0100
0111
1110
0010
```

- output

```java
4
```

### 분류
- 다이나믹 프로그래밍

## 풀이

### 문제 파악
- 1로 된 가장 큰 정사각형의 크기를 구하기
- (1,1) 이 1인 경우에 정사각형이 될 수 있음 (arr[i] [j] == 1)
- 점화식은 dp[i] [j] = math.min (dp[i-1] [j], dp[i] [j-1], dp[i-1] [j-1]) +1 와 같이 세울 수 있음    

|         |         |
|:-------:|:-------:|
| (0,0) 1 | (1,0) 1 |
| (0,1) 1 | (1,1) 1 |


- dp

|         | **0** | **1** | **2** | **3** | **4** |   
|:-------:|:-----:|:-----:|:-----:|:-----:|:-----:|
|  **0**  |    0  |    0  |    0  |    0  |    0  |
|  **1**  |    0  |    0  |    1  |    0  |    0  |
|  **2**  |    0  |    0  |    1  |    1  |    1  |
|  **3**  |    0  |    1  |    1  |    2  |    0  |
|  **4**  |    0  |    0  |    0  |    1  |    0  |



### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1915/Main.java)


- math.min 이 두가지의 숫자만 비교 가능해서 나누어서 비교

```java
int[][] dp = new int[n+1][m+1];

for (int i = 1; i < n+1; i++) {
    for (int j = 1; j < m+1 ; j++) {
        if (arr[i][j] == 1 ) {
            int min = Math.min(dp[i-1][j], dp[i][j-1]);
            dp[i][j] = Math.min(min, dp[i-1][j-1]) + 1;
        }
    }
}
```

---

#### references
<https://www.acmicpc.net/problem/1915>
