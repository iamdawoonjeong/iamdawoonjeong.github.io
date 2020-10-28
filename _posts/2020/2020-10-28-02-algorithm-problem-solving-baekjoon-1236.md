---
layout: single
title: "[Problem Solving - Baekjoon] 1236 성 지키기"
date: 2020-10-28 22:35:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-1236/"
---
# [Baekjoon Online Judge] 1236 성 지키기

## 문제
영식이는 직사각형 모양의 성을 가지고 있다. 성의 1층은 몇 명의 경비원에 의해서 보호되고 있다. 영식이는 모든 행과 모든 열에 한 명 이상의 경비원이 있으면 좋겠다고 생각했다.

성의 크기와 경비원이 어디있는지 주어졌을 때, 몇 명의 경비원을 최소로 추가해야 영식이를 만족시키는지 구하는 프로그램을 작성하시오.

### 입력
첫째 줄에 성의 세로 크기 N과 가로 크기 M이 주어진다. N과 M은 50보다 작거나 같은 자연수이다. 둘째 줄부터 N개의 줄에는 성의 상태가 주어진다. 성의 상태는 .은 빈칸, X는 경비원이 있는 칸이다.

### 출력
첫째 줄에 추가해야 하는 경비원의 최솟값을 출력한다.

### 예제

- input

```java
4 4
....
....
....
....
```

- output

```java
4
```

### 분류
- 구현

## 풀이

### 문제 파악

- 세로 크기(N) * 가로 크기(M) 행렬에서 경비원은 X로 표시됨
- 모든 행,열에 대해서 최소 한명의 경비원이 필요함
- 세로, 가로 중 경비원이 필요한 최소값 출력


```java
4 4  // N*M 행렬
.... // 경비원위치는 X
....
....
....
```


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1236/Main.java)

- 경비원있는 위치(X)를 세로(col), 가로(row)에 1로 입력함     
- col, row를 탐색하면서 경비원이 없는 경우 count 증가
- col, row 비교 후 더 큰 값 출력


```java
StringTokenizer st = new StringTokenizer(br.readLine());
int N = Integer.parseInt(st.nextToken());  //세로 col
int M = Integer.parseInt(st.nextToken());  //가로 row

String[][] arr = new String[N][M];

int[] col = new int[N];
int[] row = new int[M];

for (int i = 0; i < N; i++) {
    String[] temp= br.readLine().split("");
    for (int j = 0; j < M; j++) {
        arr[i][j] = temp[j];
        if  ("X".equals(arr[i][j])){
            col[i] = 1;
            row[j] = 1;
        }
    }
}

int colCount = 0;
for (int i = 0; i < N; i++) {
    if ( col[i] == 0) {
        colCount += 1;
    }
}

int rowCount = 0;
for (int i = 0; i < M; i++) {
    if ( row[i] == 0) {
        rowCount += 1;
    }
}

int max = Math.max(colCount,  rowCount);
System.out.println(max);
```


---

#### references
<https://www.acmicpc.net/problem/1236>
