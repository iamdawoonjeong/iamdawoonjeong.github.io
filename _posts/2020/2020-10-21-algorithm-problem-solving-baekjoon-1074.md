---
layout: single
title: "[Problem Solving - Baekjoon] 1074 Z"
date: 2020-10-21 21:58:00.000000000 +09:00
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
- recursive
- recursion
- baekjoon
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1074/"
---
# [Baekjoon Online Judge] 1074 Z

## 문제
한수는 2차원 배열 (항상 2^N * 2^N 크기이다)을 Z모양으로 탐색하려고 한다. 예를 들어, 2*2배열을 왼쪽 위칸, 오른쪽 위칸, 왼쪽 아래칸, 오른쪽 아래칸 순서대로 방문하면 Z모양이다.


만약, 2차원 배열의 크기가 2^N * 2^N라서 왼쪽 위에 있는 칸이 하나가 아니라면, 배열을 4등분 한 후에 (크기가 같은 2^(N-1)로) 재귀적으로 순서대로 방문한다.
다음 예는 2^2 * 2^2 크기의 배열을 방문한 순서이다.

N이 주어졌을 때, (r, c)를 몇 번째로 방문하는지 출력하는 프로그램을 작성하시오.
다음 그림은 N=3일 때의 예이다.

### 입력
첫째 줄에 N r c가 주어진다. N은 15보다 작거나 같은 자연수이고, r과 c는 0보다 크거나 같고, 2^N-1보다 작거나 같은 정수이다

### 출력
첫째 줄에 문제의 정답을 출력한다.


### 예제1

- input
```java
2 3 1
```

- output
```java
11
```

### 예제2

- input
```java
3 7 7
```

- output
```java
63
```

### 분류
- 재귀

## 풀이

### 문제 파악
```java
2 3 1
```
- 2<sup>2<sup> 행렬의 (3,1)의 몇 번째로 방문하는지 구하기
- (0,0) 부터 시작
- (0,0)-> (0,1) -> (1,0) -> (1,1) 순으로 방문함 (Z모양)


### 구현

#### 2*2 행렬 될 때까지 재귀적 용법으로 구하는 방법

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1074/Main.java)

- **2*2 행렬일 때 방문순서 ((0,0)-> (0,1) -> (1,0) -> (1,1)) 순으로 방문하고, 방문횟수 증가 (count++)**
- **방문횟수 찾았을경우 바로 출력 후 return 으로 해당 함수 종료 시켜주기**

```java
private static void recursion(int n, int x, int y) {

    //n=2 가 될때까지 (2*2 사각형 될때 까지 쪼개기)
    if (n == 2) {
        //(0,0)
        if (x == r && y == c) {
            System.out.println(count);
            return;
        }
        count++;

        //(0,1)
        if (x == r && y+1 == c ) {
            System.out.println(count);
            return;
        }
        count++;

       //(1,0)
        if (x+1 == r && y == c) {
            System.out.println(count);
            return;
        }
        count++;

        //(1,1)
        if (x+1 == r && y+1 == c) {
            System.out.println(count);
            return;
        }
        count++;
        return;
    }

    recursion(n/2 , x, y );        // 1사분면 탐색
    recursion(n/2 , x, y+n/2);     // 2사분면 탐색
    recursion(n/2 , x+n/2, y );    // 3사분면 탐색
    recursion(n/2 , x+n/2, y+n/2); // 4사분면 탐색
}
```

#### 1*1 행렬 될 때까지 재귀적 용법으로 구하는 방법

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1074/Main2.java)

-  현재위치 (x,y)와 찾는위치 (r,c) 값이 같을 때 방문횟수 증가 (count++)
-  소스가 매우 간단
-  시간이 오래 걸리는 것이 단점. (재귀함수 호출 횟수가 증가 하기 때문에 오래 걸림)

```java
private static void recursion(int n, int x, int y) {
    if(n == 1) {
        if(x == r && y == c)
            System.out.println(count);
        count++;
        return;
    }

    recursion(n/2 , x, y );        // 1사분면 탐색
    recursion(n/2 , x, y+n/2);     // 2사분면 탐색
    recursion(n/2 , x+n/2, y );    // 3사분면 탐색
    recursion(n/2 , x+n/2, y+n/2); // 4사분면 탐색
}
```


#### 결론
- 2*2 행렬일때 연산을 하는 것 보다 1*1 행렬일때에는 사실상 모든 수를 재귀 함수를 한번 더 호출하기 때문에 시간이 2배정도 걸림
- 재귀함수도 적절히 이용해줘야 함

| 항목	   | 2*2 |  1*1 |
|:--------:|:--------:|:--------:|
|  코드길이(Byte) |  1834    |  1155 	|
|  메모리(KB) 	 |  13808 	|  13524	|
|  시간(ms) 	     |  1344	|  3988   	|


---

#### references
<https://www.acmicpc.net/problem/1074>
