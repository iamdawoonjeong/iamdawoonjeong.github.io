---
layout: single
title: "[Problem Solving - Baekjoon] 11047 동전 0"
date: 2021-02-18 08:45:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-11047/"
---
# [Baekjoon Online Judge] 11047 동전 0

## 문제
[문제 보기](https://www.acmicpc.net/problem/11047){: target="_blank"}

## 풀이

### 문제 파악
- [5585 거스름돈](http://dawoonjeong.com/algorithm-problem-solving-baekjoon-5585/){: target="_blank"} 문제와 유사한 풀이
- 동전의 정렬 (정렬되어있는 문제이므로 정렬 필요 없음) a
- 동전의 큰 금액부터 계산
- 동전의 사용 갯수(count)는 나누기 연산 이용  
- 잔액(k)은 % 나머지 계산을 이용하여 계산

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem11047/Main.java){: target="_blank"}

```java
int count = 0;
for (int i = n-1; i >= 0; i--) {

    // 현재 동전의 금액이 잔액보다 큰 경우 다음 동전으로 넘어감
    if (k < arr[i]) {
        continue;
    }

    count = count + k/arr[i]; //동전의 갯수
    k = (k%arr[i]);   // 잔액
    if (k==0) {
        break;
    }
}
```

---

#### references
<https://www.acmicpc.net/problem/11047>{: target="_blank"}
