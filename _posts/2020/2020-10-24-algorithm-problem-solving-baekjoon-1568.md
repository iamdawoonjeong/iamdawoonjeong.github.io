---
layout: single
title: "[Problem Solving - Baekjoon] 1568 새"
date: 2020-10-24 23:03:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-1568/"
---
# [Baekjoon Online Judge] 1568 새

## 문제
N마리의 새가 나무에 앉아있고, 자연수를 배우기 원한다. 새들은 1부터 모든 자연수를 오름차순으로 노래한다. 어떤 숫자 K를 노래할 때, K마리의 새가 나무에서 하늘을 향해 날아간다. 만약, 현재 나무에 앉아있는 새의 수가 지금 불러야 하는 수 보다 작을 때는, 1부터 게임을 다시 시작한다.

나무에 앉아 있는 새의 수 N이 주어질 때, 하나의 수를 노래하는데 1초가 걸린다고 하면, 모든 새가 날아가기까지 총 몇 초가 걸리는지 출력하는 프로그램을 작성하시오.

### 입력
첫째 줄에 새의 수 N이 주어진다. 이 값은 109보다 작거나 같다.

### 출력
첫째 줄에 정답을 출력한다.


### 예제
- input

```java
14
```

- output

```java
7
```

### 분류
- 구현

## 풀이

### 문제 파악

```java
14
```

- 14마리의 새가 앉아 있음 (n)
- 1마리(k) 2마리(k+1) 3마리(k+2) 4마리(k+3) ... 오름차순 순으로 날아가는데 1초씩(count) 걸림
- 남아있는 새가 적을 경우 다시 1마리(k) 2마리(k+1) ... 날아감
- 모든 새가 날아가기 까지의 시간은?


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1568/Main.java)

- k가 남은 n보다 클 경우 다시 1부터 시작

```java
int k=1;
int count=0;

while(n != 0) {

    if (k > n) {
        k=1;
    }
    n=n-k;
    k++;
    count++;

}
```

---

#### references
<https://www.acmicpc.net/problem/1568>
