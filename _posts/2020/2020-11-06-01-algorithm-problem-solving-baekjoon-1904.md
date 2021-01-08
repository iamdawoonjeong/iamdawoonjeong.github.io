---
layout: single
title: "[Problem Solving - Baekjoon] 1904 01타일"
date: 2020-11-06 22:26:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-1904/"
---
# [Baekjoon Online Judge] 1904 01타일

## 문제
지원이에게 2진 수열을 가르쳐 주기 위해, 지원이 아버지는 그에게 타일들을 선물해주셨다. 그리고 이 각각의 타일들은 0 또는 1이 쓰여 있는 낱장의 타일들이다.

어느 날 짓궂은 동주가 지원이의 공부를 방해하기 위해 0이 쓰여진 낱장의 타일들을 붙여서 한 쌍으로 이루어진 00 타일들을 만들었다. 결국 현재 1 하나만으로 이루어진 타일 또는 0타일을 두 개 붙인 한 쌍의 00타일들만이 남게 되었다.

그러므로 지원이는 타일로 더 이상 크기가 N인 모든 2진 수열을 만들 수 없게 되었다. 예를 들어, N=1일 때 1만 만들 수 있고, N=2일 때는 00, 11을 만들 수 있다. (01, 10은 만들 수 없게 되었다.) 또한 N=4일 때는 0011, 0000, 1001, 1100, 1111 등 총 5개의 2진 수열을 만들 수 있다.

우리의 목표는 N이 주어졌을 때 지원이가 만들 수 있는 모든 가짓수를 세는 것이다. 단 타일들은 무한히 많은 것으로 가정하자.

### 입력
첫 번째 줄에 자연수 N이 주어진다.(N ≤ 1,000,000)

### 출력
첫 번째 줄에 지원이가 만들 수 있는 길이가 N인 모든 2진 수열의 개수를 15746으로 나눈 나머지를 출력한다.

### 예제
- input

```java
4
```
- output

```java
5
```


### 분류
- 동적프로그래밍

## 풀이

### 문제 파악

- n의 갯수에 따른 출력값을 파악해보기
- f(0) = 0
- f(1) = 1 (1)
- f(2) = 2 (00, 11)
- f(3) = 3 (100, 111, 001)
- f(4) = 4 (1111, 0000, 0011, 1100, 1001)

- 피보나치 수열임을 알수 있다. f(n) =  f(n-1) + f(n-2)
- 동적 프로그래밍으로 품


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1904/Main.java)

- 문제에서 주어진 n의 수가 (N ≤ 1,000,000) 이기때문에 1,000,000 까지의 수가 들어갈수 있도록, 1000001 크기의 배열 선언

```java
int[] arr = new int[1000001];
```

- 문제에 주어진 경우의 수 **N=1일 때 1만 만들 수 있고, N=2일 때는 00, 11을 만들수 있다.**

```java
arr[0] = 0;
arr[1] = 1;
arr[2] = 2;
```


- 문제에 주어진 출력시 나누어야할 문제 실제 동적프로그래밍 부분  

```java
for (int i = 3; i < n+1; i++) {
    arr[i] = (arr[i-1] + arr[i-2]) % 15746;
}
```

---

#### references
<https://www.acmicpc.net/problem/1904>
