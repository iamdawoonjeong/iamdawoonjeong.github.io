---
layout: single
title: "[Problem Solving - Baekjoon] 15969 행복"
date: 2020-12-01 21:10:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-15969/"
---
# [Baekjoon Online Judge] 15969 행복

## 문제
코이 초등학교에 새로 부임하신 교장 선생님은 어린 학생들의 행복감과 학생들의 성적 차이 관계를 알아보기로 했다. 그래서 이전 성적을 조사하여 학생 들의 시험 점수 차이 변화를 알아보려고 한다.

예를 들어서 2016년 학생 8명의 점수가 다음과 같다고 하자.

27, 35, 92, 75, 42, 53, 29, 87

그러면 가장 높은 점수는 92점이고 가장 낮은 점수는 27점이므로 점수의 최대 차이는 65이다. 한편 2017년 학생 8명의 점수가 다음과 같았다.

85, 42, 79, 95, 37, 11, 72, 32

이때 가장 높은 점수는 95점이고 가장 낮은 점수는 11점이므로 점수의 최대 차이는 84이다.

N명 학생들의 점수가 주어졌을 때, 가장 높은 점수와 가장 낮은 점수의 차이를 구하는 프로그램을 작성하시오

### 입력
표준 입력으로 다음 정보가 주어진다. 첫 번째 줄에는 학생 수 N이 주어진다. 다음 줄에는 N명의 학생 점수가 공백 하나를 사이에 두고 주어진다.

### 출력
표준 출력으로 가장 높은 점수와 가장 낮은 점수의 차이를 출력한다.

### 제한
모든 서브태스크에서 2 ≤ N ≤ 1,000이고 입력되는 학생들의 점수는 0 이상 1,000 이하의 정수이다.

### 서브태스크1
학생 수가 2명인 경우만 존재한다.

### 서브태스크2
점수가 낮은 점수부터 높은 점수까지 순서대로 주어진다.

### 서브태스크3
원래의 제약 조건 이외에 아무 제약 조건이 없다.

### 예제
- input

```java
5
27 35 92 75 42
```

- output

```java
65
```


### 예제2
- input

```java
8
85 42 79 95 37 11 72 32
```

- output

```java
84
```

### 분류
- 구현

## 풀이

### 문제 파악

- 배열의 최대 값과 최소 값을 구해서 연산하면 되는 문제

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem15969/Main.java)

- 정렬 후, 최대 값과 최소값을 추출하여 연산한 후 출력  

```java
Arrays.sort(arr);

int min = arr[0];
int max = arr[n-1];

System.out.println(max-min);
```

---

#### references
<https://www.acmicpc.net/problem/15969>
