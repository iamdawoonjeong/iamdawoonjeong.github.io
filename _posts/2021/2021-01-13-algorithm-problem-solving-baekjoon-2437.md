---
layout: single
title: "[Problem Solving - Baekjoon] 2437 저울"
date: 2021-01-13 22:30:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-2437/"
---
# [Baekjoon Online Judge] 2437 저울

## 문제
하나의 양팔 저울을 이용하여 물건의 무게를 측정하려고 한다. 이 저울의 양 팔의 끝에는 물건이나 추를 올려놓는 접시가 달려 있고, 양팔의 길이는 같다. 또한, 저울의 한쪽에는 저울추들만 놓을 수 있고, 다른 쪽에는 무게를 측정하려는 물건만 올려놓을 수 있다.

무게가 양의 정수인 N개의 저울추가 주어질 때, 이 추들을 사용하여 측정할 수 없는 양의 정수 무게 중 최솟값을 구하는 프로그램을 작성하시오.

예를 들어, 무게가 각각 3, 1, 6, 2, 7, 30, 1인 7개의 저울추가 주어졌을 때, 이 추들로 측정할 수 없는 양의 정수 무게 중 최솟값은 21이다.

### 입력
첫 째 줄에는 저울추의 개수를 나타내는 양의 정수 N이 주어진다. N은 1 이상 1,000 이하이다. 둘째 줄에는 저울추의 무게를 나타내는 N개의 양의 정수가 빈칸을 사이에 두고 주어진다. 각 추의 무게는 1이상 1,000,000 이하이다.

### 출력
첫째 줄에 주어진 추들로 측정할 수 없는 양의 정수 무게 중 최솟값을 출력한다.

### 예제

- input

```java
7
3 1 6 2 7 30 1
```

- output

```java
21
```

### 분류
- greedy

## 풀이

### 문제 파악

- 입력한 숫자 정렬

```java
1 1 2 3 6 7 30
```

- 무게가 1씩 증가할 때 마다
- 이전 상태까지 만들수 있는 무게 >= 무게추(N)+1 쌓아나갈수 있다  


| 무게 | 추(N) |
|:----:|:----:|
|    1 |    1 |
|    2 |    2 |
|    3 |    3 |
|    4 |  1+3 |
|    5 |  2+3 |
|    6 |    6 |
|    7 |    7 |
|    8 |  7+1 |
|    9 |  2+8 |


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2437/Main.java)


```java
Arrays.sort(arr);

int result = 0; //구할 수 없는 최소 정수값

for (int i = 0; i < n; i++) {

    //result+1 반드시 1 필요함
    //추의무게가 <= 구할 무게보다 같거나 작아야 구할수있음  
    if (arr[i] <= result+1) {
        result += arr[i];
    }else {
        break;
    }
}

System.out.println(result+1);
```

- arr[i] <= result+1  : result += arr[i]
- 1 <= 1    : 0+1 = 1
- 1 <= 2    : 1+1 = 2
- 2 <= 3    : 2+2 = 4
- 3 <= 5    : 4+3 = 7
- 6 <= 8    : 7+6 = 13
- 7 <= 14   : 13+7 = 20
- 20까지 만들수 있음


---

#### references
<https://www.acmicpc.net/problem/2437>
