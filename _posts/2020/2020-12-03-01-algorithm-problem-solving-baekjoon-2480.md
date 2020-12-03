---
layout: single
title: "[Problem Solving - Baekjoon] 2480 주사위 세개"
date: 2020-12-03 23:10:00.000000000 +09:00
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
- implementation
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-2480/"
---
# [Baekjoon Online Judge] 2480 주사위 세개

## 문제
1에서부터 6까지의 눈을 가진 3개의 주사위를 던져서 다음과 같은 규칙에 따라 상금을 받는 게임이 있다.

같은 눈이 3개가 나오면 10,000원+(같은 눈)*1,000원의 상금을 받게 된다.
같은 눈이 2개만 나오는 경우에는 1,000원+(같은 눈)*100원의 상금을 받게 된다.
모두 다른 눈이 나오는 경우에는 (그 중 가장 큰 눈)*100원의 상금을 받게 된다.  
예를 들어, 3개의 눈 3, 3, 6이 주어지면 상금은 1,000+3*100으로 계산되어 1,300원을 받게 된다. 또 3개의 눈이 2, 2, 2로 주어지면 10,000+2*1,000 으로 계산되어 12,000원을 받게 된다. 3개의 눈이 6, 2, 5로 주어지면 그중 가장 큰 값이 6이므로 6*100으로 계산되어 600원을 상금으로 받게 된다.

3개 주사위의 나온 눈이 주어질 때, 상금을 계산하는 프로그램을 작성 하시오.

### 입력
첫째 줄에 3개의 눈이 빈칸을 사이에 두고 각각 주어진다.

### 출력
첫째 줄에 게임의 상금을 출력 한다.  

### 예제
- input

```java
3 3 6
```

- output

```java
1300
```

### 분류
- 구현

## 풀이

### 문제 파악
- 주사위를 던져서 나오는 숫자의 중복 갯수 별 상금을 구하는 문제
- 중복 갯수마다 상금계산법이 달라서 이부분을 어떻게 푸느냐 인데 제일 간단한 배열로 구현
- set으로 구하는 방법도 있으나 범위가 크지 않아서 그냥 배열로 진행함

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2480/Main.java)

- 주사위의 눈을 배열의 index에 담아주고 나온 횟수를 배열의 값을 담음

```java
for (int i = 0; i < 3; i++) {
	arr[Integer.parseInt(st.nextToken())] += 1 ;
}

int reward = 0;
int max = 0;
```

- 각 배열의 값이 중복된 횟수
- 3번 던지기 때문에 최대 3번 같을 수 있어 제일 먼저 계산한 후, 나머지 2번 1번 계산
- 1번은 여러번 나올 수 있으므로 max값 따로 관리해주기

```java
for (int i = 1; i < 7; i++) {

    if (arr[i] == 3) {
        // 10,000원+(같은 눈)*1,000원
        reward = 10000 + (i*1000);
        break;

    }else if (arr[i] == 2) {
        //1,000원+(같은 눈)*100원
        reward = 1000 + (i*100);
        break;

    }else if (arr[i] == 1) {
        //(그 중 가장 큰 눈)*100원의 상금
        max = Math.max(i, max);
        reward = max*100;
    }
}

System.out.println(reward);
```


---


#### references
<https://www.acmicpc.net/problem/2480>
