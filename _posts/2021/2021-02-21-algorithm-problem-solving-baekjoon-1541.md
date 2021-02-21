---
layout: single
title: "[Problem Solving - Baekjoon] 1541 잃어버린 괄호"
date: 2021-02-21 10:52:00.000000000 +09:00
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
- greedy
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1541/"
---
# [Baekjoon Online Judge] 1541 잃어버린 괄호

## 문제
[문제 보기](https://www.acmicpc.net/problem/1541){: target="_blank"}

## 풀이

### 문제 파악
- "-" 연산을 나중에 하는 것이 더 작은 숫자가 나옴
- "-" 기준으로 나누어서 + 연산을 먼저 해주는 로직을 짜야함

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1541/Main.java){: target="_blank"}


- "-" 기준으로 피연산자들 구하기
- [55]   [50+40] 으로 나누어짐

```java
String[] input = br.readLine().split("\\-");
```

- "+" 기준으로 나누어서 합을 구함

```java
int[] sum = new int[input.length]; //숫자들의 합

for (int i = 0; i < input.length; i++) {
    String[] operand = input[i].split("\\+"); //+ 기호 기준으로 피연산자들 구하기

    for (int j = 0; j < operand.length; j++) {
        sum[i] += Integer.parseInt(operand[j]) ;
    }
}
```

- 마지막으로 "-" 연산 해주기

```java
int result = sum[0];
for (int i = 1; i < sum.length; i++) {
    result = result - sum[i];
}

```

---

#### references
<https://www.acmicpc.net/problem/1541>{: target="_blank"}
