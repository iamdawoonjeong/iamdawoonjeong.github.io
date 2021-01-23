---
layout: single
title: "[Problem Solving - Baekjoon] 1495 기타리스트"
date: 2020-11-09 22:22:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-1495/"
---
# [Baekjoon Online Judge] 1495 기타리스트

## 문제
Day Of Mourning의 기타리스트 강토는 다가오는 공연에서 연주할 N개의 곡을 연주하고 있다. 지금까지 공연과는 다른 공연을 보여주기 위해서 이번 공연에서는 매번 곡이 시작하기 전에 볼륨을 바꾸고 연주하려고 한다.

먼저, 공연이 시작하기 전에 각각의 곡이 시작하기 전에 바꿀 수 있는 볼륨의 리스트를 만들었다. 이 리스트를 V라고 했을 때, V[i]는 i번째 곡을 연주하기 전에 바꿀 수 있는 볼륨을 의미한다. 항상 리스트에 적힌 차이로만 볼륨을 바꿀 수 있다. 즉, 현재 볼륨이 P이고 지금 i번째 곡을 연주하기 전이라면, **i번 곡은 P+V[i]나 P-V[i] 로 연주**해야 한다. 하지만, 0보다 작은 값으로 볼륨을 바꾸거나, M보다 큰 값으로 볼륨을 바꿀 수 없다.

곡의 개수 N과 시작 볼륨 S, 그리고 M이 주어졌을 때, 마지막 곡을 연주할 수 있는 볼륨 중 최댓값을 구하는 프로그램을 작성하시오. 모든 곡은 리스트에 적힌 순서대로 연주해야 한다.

### 입력
첫째 줄에 N, S, M이 주어진다. (1 ≤ N ≤ 100, 1 ≤ M ≤ 1000, 0 ≤ S ≤ M) 둘째 줄에는 각 곡이 시작하기 전에 줄 수 있는 볼륨의 차이가 주어진다. 이 값은 1보다 크거나 같고, M보다 작거나 같다.

### 출력
첫째 줄에 가능한 마지막 곡의 볼륨 중 최댓값을 출력한다. 만약 마지막 곡을 연주할 수 없다면 (중간에 볼륨 조절을 할 수 없다면) -1을 출력한다.

### 예제
- input

```java
3 5 10
5 3 7
```

- output

```java
10
```

### 분류
- 동적프로그래밍

## 풀이

### 문제 파악

- 곡의 갯수 n = 3
- 볼륨초기값 s = 5
- 최대볼륨값 m = 10;
- 1번째 곡은 이전볼륨값 5 + 현재볼륨값 5  = 10 or 이전볼륨값 5 - 현재볼륨값 5 = 0 으로 연주

```java
3 5 10
5 3 7  
```

- 처음은 볼륨(s)=5부터 시작
- 1번곡은 처음 볼륨부터 5만큼 차이 (0, 10)
- 2번곡은 1번곡의 볼륨 3만큼 차이 (3, 7)
- 3번곡은 2번곡의 볼륨 7만큼 차이 (0, 10)

|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|:----:|:----:|:----:|:-----:|:-----:|:-----:|
| 0 | F | F | F | F | F | T | F | F | F | F | F |
| 1 | T | F | F | F | F | F | F | F | F | F | T |
| 2 | F | F | F | T | F | F | F | T | F | F | F |
| 3 | T | F | F | F | F | F | F | F | F | F | T |


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1495/Main.java)

- 곡 순서별 볼륨차이 i=1 부터 담음(나중에 비교하기 쉽게)

```java
int[] arr = new int[n+1];
for (int i = 1; i < n+1; i++) {
    arr[i] = Integer.parseInt(st.nextToken());
}
```

- 문제의 조건인 첫 볼륨값 셋팅 dp[0] [s] = 1;
- 이전 곡의 같은 볼륨이 1인 경우에만 연산 수행 if(dp[i-1] [j] == 0)
- 현재볼륨의 위치에서 곡의 볼륨 차를 뺀 값이 0이상 일 경우 현재볼륨 체크 :  dp[i] [j-arr[i]] = 1;
- 현재볼륨의 위치에서 곡의 볼륨 차를 더한 값이 m이하 일 경우 현재볼륨 체크 :  dp[i] [j+arr[i]] = 1;

```java
int[][] dp = new int[n+1][m+1];
dp[0][0] = 0;
dp[0][s] = 1;

for (int i = 1; i < n+1; i++) {
    for (int j = 0; j < m+1; j++) {
        if (dp[i-1][j] == 0) {
            continue;
        }

        if ( j-arr[i] >= 0 ) {
            dp[i][j-arr[i]] = 1;
        }

        if ( j+arr[i] <= m ) {
            dp[i][j+arr[i]] = 1;
        }
    }
}
```

- 마지막곡을 index=m부터 탐색해서 제일 먼저 나오는 볼륨 리턴 (for (int j = m ; j > -1; j--))
- 마지막 곡을 연주할 수 없다면 -1 리턴이 조건이기때문에 초기값 -1로 저장 (result = -1)

```java
int result = -1;

// 마지막 곡만 탐색
for (int j = m ; j > -1; j--) {
    if (dp[n][j]==1) {
        result = j;
        break;
    }
}
```

---

#### references
<https://www.acmicpc.net/problem/1495>
