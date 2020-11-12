---
layout: single
title: "[Problem Solving - Baekjoon] 5585 거스름돈"
date: 2020-11-12 22:51:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-5585/"
---
# [Baekjoon Online Judge] 5585 거스름돈

## 문제
타로는 자주 JOI잡화점에서 물건을 산다. JOI잡화점에는 잔돈으로 500엔, 100엔, 50엔, 10엔, 5엔, 1엔이 충분히 있고, 언제나 거스름돈 개수가 가장 적게 잔돈을 준다. 타로가 JOI잡화점에서 물건을 사고 카운터에서 1000엔 지폐를 한장 냈을 때, 받을 잔돈에 포함된 잔돈의 개수를 구하는 프로그램을 작성하시오.

예를 들어 입력된 예1의 경우에는 아래 그림에서 처럼 4개를 출력해야 한다.

### 입력
입력은 한줄로 이루어져있고, 타로가 지불할 돈(1 이상 1000미만의 정수) 1개가 쓰여져있다.

### 출력
제출할 출력 파일은 1행으로만 되어 있다. 잔돈에 포함된 매수를 출력하시오.

### 예제
- input

```java
380
```

- output

```java
4
```

### 분류
- 탐욕알고리즘

## 풀이

### 문제 파악
-  1000엔에서 입력받은 금액(n)을 빼서 잔돈(changes)으로 거슬러주어야할 동전의 갯수(count)를 구하는 문제
-  전형적인 greedy algorithm  


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem5585/Main.java)


- 잔돈의 종류는 미리 정해주었으므로 내림차순순으로 배열에 담아 둠 (conis[])

```java
int changes = 1000 - n;
int[] coins = new int[]{500,100,50,10,5,1};  // 500엔, 100엔, 50엔, 10엔, 5엔, 1엔
int count = 0;

for (int i = 0; i < coins.length; i++) {
    if( changes >= 0 ) {
        count = count + (changes/coins[i]);
        changes %= coins[i];
    }
}

System.out.println(count);
```

---

#### references
<https://www.acmicpc.net/problem/5585>
