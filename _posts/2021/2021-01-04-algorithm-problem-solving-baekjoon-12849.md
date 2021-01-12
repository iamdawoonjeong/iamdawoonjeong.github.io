---
layout: single
title: "[Problem Solving - Baekjoon] 12849 본대 산책"
date: 2021-01-04 21:05:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-12849/"
---
# [Baekjoon Online Judge] 12849 본대 산책

## 문제
실 대학교 정보 과학관은  캠퍼스의 길 건너편으로 유배를 당했다. 그래서 컴퓨터 학부 학생들은 캠퍼스를 ‘본대’ 라고 부르고 정보 과학관을 ‘정보대’ 라고 부른다. 준영이 또한 컴퓨터 학부 소속 학생이라서 정보 과학관에 박혀있으며 항상 본대를 가고 싶어 한다. 어느 날 준영이는 본대를 산책하기로 결심하였다. 숭실 대학교 캠퍼스 지도는 아래와 같다.

(편의 상 문제에서는 위 건물만 등장한다고 가정하자)

한 건물에서 바로 인접한 다른 건물로 이동 하는 데 1분이 걸린다. 준영이는 산책 도중에 한번도 길이나 건물에 멈춰서 머무르지 않는다. 준영이는 할 일이 많아서 딱 D분만 산책을 할 것이다. (산책을 시작 한 지 D분 일 때, 정보 과학관에 도착해야 한다.) 이때 가능한 경로의 경우의 수를 구해주자.

### 입력
D 가 주어진다 (1 ≤ D ≤ 100,000) 

### 출력
가능한 경로의 수를 1,000,000,007로 나눈 나머지를 출력 한다.

### 예제

- input

```java
10
```

- output

```java
9857
```

### 분류
- 다이나믹 프로그래밍

## 풀이 

### 문제 파악

- 정보과학관에서 n분 후 다시 정보과학관으로 돌아오는 경우의 수 구하기

### 구현

- **문제 틀림**


[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem12849/Main.java)

- 각 건물에 대해새 어느 인덱스로 들어갈 것인지 정해놓고 시작

```
0: 정보과학관
1: 전산관
2: 미래관
3: 신양관
4: 한경직기념관
5: 진리관
6: 학생회관
7: 형남공학관
```


- 1분 후 위치를 점화식으로 표현 
- 각 위치에 대해서 들어오는 경로로를 모두 써 주어 계산

```java
public static int[] next(int[] state) {
    int[] temp = new int[8];
    temp[0] = state[1] + state[2];
    temp[1] = state[0] + state[2] + state[3];
    temp[2] = state[0] + state[1] + state[3] + state[4];
    temp[3] = state[1] + state[2] + state[4] + state[5];
    temp[4] = state[2] + state[3] + state[5] + state[7];
    temp[5] = state[3] + state[4] + state[6];
    temp[6] = state[5] + state[7];
    temp[7] = state[4] + state[6];
    
    for (int i = 0; i < 8; i++) {
        temp[i] = temp[i]%1000000007;
    }
    
    return temp;
}
```


---

#### references
<https://www.acmicpc.net/problem/12849>