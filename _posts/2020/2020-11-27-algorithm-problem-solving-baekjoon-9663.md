---
layout: single
title: "[Problem Solving - Baekjoon] 9663 N-Queen"
date: 2020-11-27 18:20:00.000000000 +09:00
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
- backtracking
- n-queen
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-9663/"
---
# [Baekjoon Online Judge] 9663 N-Queen

## 문제
N-Queen 문제는 크기가 N × N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제이다.

N이 주어졌을 때, 퀸을 놓는 방법의 수를 구하는 프로그램을 작성하시오.

### 입력
첫째 줄에 N이 주어진다. (1 ≤ N < 15)

### 출력
첫째 줄에 퀸 N개를 서로 공격할 수 없게 놓는 경우의 수를 출력한다.

### 예제

- input

```java
8
```

- output

```java
92
```

### 분류
- 백트래킹

## 풀이

### 문제 파악

- 대표적인 백트래킹문제
- 백트래킹 문제는 DFS 로 구현하는 것 이 쉬우나, BFS에 비해 시간이 오래 걸림
- 각 행을 차례대로 확인하면서, 각 열에 퀸을 놓는 경우를 고려
	-  즉, 위쪽 행을 모두 확인하면서 현재 열에 위치에 놓을 수 있는지 확인

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem9663/Main.java)

- x번째 행에 대하여 처리

```java
public static void dfs(int x ) {

    if ( x == n ) {
        result += 1;
    }else {

        // x번째 행의 각 열에  퀸을 두어서 괜찮은지 확인해보기
        for (int i = 0; i < n ; i++) {
            row[x] = i;

            //  해당 위치에 두어도 괜찮은 경우
            if (check(x)) {
                 // 다음 행으로 넘어가기
                dfs(x+1);
            }
        }

    }
}
```

- x번째 행에 놓은 Queen 에 대해서 위쪽, 대각선을 확인 하여 검증

```java
public static boolean check(int x) {

    // 이전 행에서 놓았던 모든 Queen 들을 확인
    for (int i = 0; i < x; i++) {
        // 위쪽 확인
        if (row[x] == row[i]){
            return false;
        }
        // 대각선 확인
        if ((Math.abs(row[x] - row[i])) == x - i) {
            return false;
        }
    }

    return true;
}
```


---

#### references
<https://www.acmicpc.net/problem/9663>
