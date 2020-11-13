---
layout: single
title: "[Problem Solving - Baekjoon] 2012 등수 매기기"
date: 2020-11-13 22:05:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-2012/"
---
# [Baekjoon Online Judge] 2012 등수 매기기

## 문제
2007년 KOI에 N명의 학생들이 참가하였다. 경시일 전날인 예비소집일에, 모든 학생들은 자신이 N명 중에서 몇 등을 할 것인지 예상 등수를 적어서 제출하도록 하였다.

KOI 담당조교로 참가한 김진영 조교는 실수로 모든 학생의 프로그램을 날려 버렸다. 1등부터 N등까지 동석차 없이 등수를 매겨야 하는 김 조교는, 어쩔 수 없이 각 사람이 제출한 예상 등수를 바탕으로 임의로 등수를 매기기로 했다.

자신의 등수를 A등으로 예상하였는데 실제 등수가 B등이 될 경우, 이 사람의 불만도는 A와 B의 차이 절대값으로 수치화할 수 있다. 당신은 N명의 사람들의 불만도의 총 합을 최소로 하면서, 학생들의 등수를 매기려고 한다.

각 사람의 예상 등수가 주어졌을 때, 김 조교를 도와 이러한 불만도의 합을 최소로 하는 프로그램을 작성하시오.

### 입력
첫째 줄에 자연수 N이 주어진다. (1 ≤ N ≤ 500,000) 둘째 줄부터 N개의 줄에 걸쳐 각 사람의 예상 등수가 순서대로 주어진다. 예상 등수는 500,000 이하의 자연수이다.

### 출력
첫째 줄에 불만도의 합을 최소로 할 때, 그 불만도를 출력한다.

### 예제

- input

```java
5
1
5
3
1
2
```

- output

```java
3
```

### 분류
- 탐욕

## 풀이

### 문제 파악

- 예상순위 오름차순순으로 실제 순위를 매겨서 그 차이를 계산 하면 불만도가 가장 낮게 됨

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2012/Main.java)


- 예상순의 오름차순 정렬
- 실제 등수 - 예상 순위 절대값을 다 더 해주기
- 결과값은  long으로 선언 (int형 선언시 실패함  500,000  *  500,000  = 250,000,000,000 으로 int[^1] 초과 함)

```java       
Arrays.sort(arr);
long result = 0;
for (int i = 1; i < arr.length; i++) {
    long gap = Math.abs(i-arr[i]);
    result += gap;
}

System.out.println(result);
```

---
#### references
<https://www.acmicpc.net/problem/2012>


---
#### 주석
[^1]: int (4byte) -2,147,483,648 ~ 2,147,483,647
