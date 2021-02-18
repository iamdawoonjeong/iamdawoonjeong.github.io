---
layout: single
title: "[Problem Solving - Baekjoon] 11399 ATM "
date: 2021-02-19 18:41:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-11399/"
---
# [Baekjoon Online Judge] 11399 ATM

## 문제
[문제 보기](https://www.acmicpc.net/problem/11399){: target="_blank"}

## 풀이

### 문제 파악
- 오름차순 정렬
- 각 위치별 대기시간(time[])을 구하고
- 대기 시간의 총 합(sum)을 구함


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem11399/Main.java){: target="_blank"}

```java
//오름차순 정렬
Arrays.sort(arr);

//각 위치별 대기 시간 구하기
int[] time = new int[n];
time[0] = arr[0];
for (int i = 1; i < n; i++) {
    time[i] = time[i-1] + arr[i];
}

//대기 총 시간의 합
int sum = 0;
for (int i = 0; i < n; i++) {
    sum += time[i];
}
System.out.println(sum);
```

---

#### references
<https://www.acmicpc.net/problem/11399>{: target="_blank"}
