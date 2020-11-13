---
layout: single
title: "[Problem Solving - Baekjoon] 1439 뒤집기"
date: 2020-11-13 22:00:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-1439/"
---
# [Baekjoon Online Judge] 1439 뒤집기

## 문제
다솜이는 0과 1로만 이루어진 문자열 S를 가지고 있다. 다솜이는 이 문자열 S에 있는 모든 숫자를 전부 같게 만들려고 한다. 다솜이가 할 수 있는 행동은 S에서 연속된 하나 이상의 숫자를 잡고 모두 뒤집는 것이다. 뒤집는 것은 1을 0으로, 0을 1로 바꾸는 것을 의미한다.

예를 들어 S=0001100 일 때,

1. 전체를 뒤집으면 1110011이 된다.
2. 4번째 문자부터 5번째 문자까지 뒤집으면 1111111이 되어서 2번 만에 모두 같은 숫자로 만들 수 있다.

하지만, 처음부터 4번째 문자부터 5번째 문자까지 문자를 뒤집으면 한 번에 0000000이 되어서 1번 만에 모두 같은 숫자로 만들 수 있다.

문자열 S가 주어졌을 때, 다솜이가 해야하는 행동의 최소 횟수를 출력하시오.

### 입력
첫째 줄에 문자열 S가 주어진다. S의 길이는 100만보다 작다.

### 출력
첫째 줄에 다솜이가 해야하는 행동의 최소 횟수를 출력한다.

### 예제

- input

```java
0001100
```

- output

```java
1
```

### 분류
- 그리디 알고리즘

## 풀이

### 문제 파악
- 뒤집는 것은 1을 0으로, 0을 1로 바꾸어 모두 같은 숫자를 만들때 최소 횟수구하기


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1439/Main.java)

- 처음 숫자를 기준으로 모두 0을 만들 경우(count0) 횟수 구하기
- 처음 숫자를 기준으로 모두 1로 만들 경우(count1) 횟수 구하기
- 더 작은 횟수 출력

```java     
int count0 = 0;
int count1 = 0;

if (arr[0] == 1) {
    count0 += 1;  //첫 배열의 숫자가 1인경우 모두 0로 만들기 위해 1횟수 추가
}else {
    count1 += 1; //첫 배열의 숫자가 0인경우 모두 1로 만들기 위해 1횟수 추가
}

for (int i = 0; i < arr.length-1; i++) {

    if (arr[i] != arr[i+1]) {
		// 다음수에서 1로 바뀌는 경우
        if(arr[i+1] == 1 ) {
            count0 += 1;

        // 다음수에서 0으로 바뀌는 경우
        }else {
            count1 += 1;
        }
    }
}

int result = Math.min(count0, count1);
```


---

#### references
<https://www.acmicpc.net/problem/1439>
