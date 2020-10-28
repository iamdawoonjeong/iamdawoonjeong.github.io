---
layout: single
title: "[Problem Solving - Baekjoon] 1668 트로피 진열"
date: 2020-10-28 22:25:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-1668/"
---
# [Baekjoon Online Judge] 1668 트로피 진열

## 문제
민식이는 “오민식”이라는 팀이름으로 수없이 많은 로봇대회를 우승했다. 따라서 민식이의 집에는 트로피가 많다. 민식이는 트로피를 어떤 선반 위에 올려놨다. 이 선반은 민식이의 방문을 열고 들어가자마자 선반의 왼쪽이 보인다. 다른말로 하자면, 뒤의 트로피가 앞의 트로피에 가려져 있다는 말이다.

안타깝게도, 높이가 큰 트로피가 높이가 작은 트로피의 왼쪽에 있다면, 높이가 작은 트로피는 큰 트로피에 가려서 보이지 않게 된다. 트로피는 자기의 앞에 (보는 사람의 관점에서) 자기보다 높이가 작은 트로피가 있을 때만 보이게 된다. 민식이는 선반을 180도 회전시켜서 트로피가 보이는 개수를 변하게 할 수도 있다.

### 입력
첫째 줄에 트로피의 개수 N (1 ≤ N ≤ 50)이 주어진다. 둘째 줄부터 N개의 줄에 왼쪽의 트로피부터 차례대로 높이가 주어진다. 트로피의 높이는 100보다 작거나 같은 자연수이다.

### 출력
첫째 줄에 왼쪽에서 봤을 때 보이는 개수, 둘째 줄에 오른쪽에서 봤을 때 보이는 개수를 출력한다.

### 예제
- input

```java
5
1
2
3
4
5
```

- output

```java
5
1
```

## 풀이

### 문제 파악

- 왼쪽에서 보이는 트로피 갯수 구하기
- 오른쪽에서 보이는 트로피 갯수 구하기
- 뒤에 있는 트로피(i+1)가 앞에 있는 트로피(i) 보다 커야 보임  

```java
5 // 트로피갯수 n
1 // 왼쪽부터 트로피 크기
2
3
4
5
```

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1688/Main.java)

- 배열에 입력된 1~끝까지 last에 입력된 수가 비교하는 수보다 작아야 보임

```java
int left = 1;
int lastL = arr[0];

for (int i = 1; i < arr.length; i++) {
    if ( lastL < arr[i]) {
        lastL = arr[i];
        left++;
    }
}

System.out.println(left);
```

- 배열에 입력된 n-1 ~ 0째 까지  last에 입력된 수가 비교하는 수보다 작아야 보임

```java
int right = 1;
int lastR = arr[n-1];

for (int j = n-2; j >= 0; j--) {
    if ( lastR < arr[j]) {
        lastR = arr[j];
        right++;
    }
}

System.out.println(right);
```


---

#### references
<https://www.acmicpc.net/problem/1668>
