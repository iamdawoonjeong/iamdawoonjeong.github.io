---
layout: single
title: "[Problem Solving - Baekjoon] 1920 수찾기 "
date: 2020-10-15 23:23:00.000000000 +09:00
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
- set
- baekjoon
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1920/"
---
# [Baekjoon Online Judge] 1920 수찾기

## 문제
N개의 정수 A[1], A[2], …, A[N]이 주어져 있을 때, 이 안에 X라는 정수가 존재하는지 알아내는 프로그램을 작성하시오.

### 입력
첫째 줄에 자연수 N(1≤N≤100,000)이 주어진다. 다음 줄에는 N개의 정수 A[1], A[2], …, A[N]이 주어진다. 다음 줄에는 M(1≤M≤100,000)이 주어진다. 다음 줄에는 M개의 수들이 주어지는데, 이 수들이 A안에 존재하는지 알아내면 된다. 모든 정수의 범위는 -231 보다 크거나 같고 231보다 작다.

### 출력
M개의 줄에 답을 출력한다. 존재하면 1을, 존재하지 않으면 0을 출력한다.

### 예제
- input
```java
5
4 1 5 2 3
5
1 3 7 9 5
```

- output
```java
1
1
0
0
1
```

### 분류
- 이분 탐색

## 풀이

### 문제 파악
```java
5             // N
4 1 5 2 3     // N개의 수
5             // M
1 3 7 9 5     // M개의 수 : 현재 줄의 수들이 2번째줄에 존재하며 1 미존재시 0 출력
```

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1920/Main.java)


#### set 이용
- set: 순서 없고 중복 안됨
- N의 숫자들을 Set 넣음
- set.contains() 를 이용해서 M의 값이 존재하는지 확인

```java
Set<Integer> set= new HashSet<Integer>();

for (int i = 0; i < N; i++) {
    set.add(Integer.parseInt(temp[i]));
}

int M = Integer.parseInt(br.readLine());
String[] arr= br.readLine().split(" ");

int[] result = new int[M];

for (int i = 0; i < M; i++) {
    if (set.contains(Integer.parseInt(arr[i]))) {
        result[i] = 1;
    }else {
        result[i] = 0;
    }
}

for (int j = 0; j < M; j++) {
    System.out.println(result[j]);
}

```


#### for 이용

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1920/MainFor.java)

- for문 사용해서 체크

```java

for (int i = 0; i < M; i++) {
    arr2[i] = Integer.parseInt(temp2[i]);
    result[i] = solution(arr, arr2[i]);

	for (int j = 0; j < arr.length; j++) {
        if (arr[j] == input ){
		    return[i] = 1
		}else {
		    return[i] = 0;		 
		}
    }


}

private static int solution(int[] arr, int input) {

    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == input )
            return 1;
    }
    return 0;
}
```


### 결론
- 중복없는 수열이라면 set을 사용하는게 간단하고 시간도 빠른 문제

| 항목	   | set | for |
|:--------:|:--------:|:--------:|
|  코드길이(Byte) |  1308    |   1464 	|
|  메모리(KB) 	 |  88996 	|  69268 	|
|  시간(ms) 	     |  1768 	|  3168   	|



---

#### references
<https://www.acmicpc.net/problem/1920>
