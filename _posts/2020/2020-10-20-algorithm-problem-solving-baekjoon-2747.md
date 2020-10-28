---
layout: single
title: "[Problem Solving - Baekjoon] 2747 피보나치 수"
date: 2020-10-20 22:05:00.000000000 +09:00
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
- fibonacci
- recursion
- dynamic
- baekjoon
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-2747/"
---
# [Baekjoon Online Judge] 2747 피보나치 수

## 문제
피보나치 수는 0과 1로 시작한다. 0번째 피보나치 수는 0이고, 1번째 피보나치 수는 1이다. 그 다음 2번째 부터는 바로 앞 두 피보나치 수의 합이 된다.

이를 식으로 써보면 Fn = Fn-1 + Fn-2 (n>=2)가 된다.

n=17일때 까지 피보나치 수를 써보면 다음과 같다.

0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, 1597

n이 주어졌을 때, n번째 피보나치 수를 구하는 프로그램을 작성하시오.

### 입력
첫째 줄에 n이 주어진다. n은 45보다 작거나 같은 자연수이다.

### 출력
첫째 줄에 n번째 피보나치 수를 출력한다.

### 예제
- input
```java
10
```

- output
```java
55
```

### 분류
- 구현
- 동적프로그래밍
- 재귀적함수


## 풀이

### 문제 파악
1. 피보나치 수열을 풀면 됨 (아래 두개의 조건은 기본)
	```java
	F(0)=0, F(1)=1
	Fn = Fn-1 + Fn-2 (n>=2)
	```
2. 동적프로그래밍(구현 간단)으로 풀기로 함
[참고:동적프로그래밍](http://dawoonjeong.com/algorithm-dynamic/)

3. 재귀함수도 풀어 봄
[참고:재귀함수](http://dawoonjeong.com/algorithm-recursion/)


### 구현

#### Dynamic 이용
- 간단하게 dynamic programming을 이용하여 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2747/Main.java)

```java
private static int fibonacci(int n) {
    int[] f = new int[n+1];
    f[0] = 0;
    f[1] = 1;
    int i;

    for (i = 2; i <= n; i++) {
        f[i] = f[i-1] + f[i-2];
    }
    return f[n];
}
```


#### Recursion을 이용
- 피보나치 수열 재귀적 함수도 많이 이용
- 그러나 재귀적 함수로 구현해서 제출 했을 경우 **시간초과**

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2747/MainRecursion.java)

```java
private static int fibonacci(int n) {

    if (n == 0) {
        return 0;
    } else if ( n == 1) {
        return 1;
    }
    return fibonacci(n-1) + fibonacci(n-2);
}
```

### 결론
- 알고리즘을 배울때는 recursion을 필수로 배우긴 하나, 숫자가 커지면 호출 횟수가 증가해서 시간초과가 될 수 있음
- 문제를 보고 잘 판단해서 다른 알고리즘을 이용


| 항목	   | Dynamic |  Recursion |
|:--------:|:--------:|:--------:|
|  코드길이(Byte) |  747    |   - 	|
|  메모리(KB) 	 |  12976 	|  - 	|
|  시간(ms) 	     |  80	|  -   	|


---

#### references
<https://www.acmicpc.net/problem/2747>
