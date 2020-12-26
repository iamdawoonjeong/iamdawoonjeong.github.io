---
layout: single
title: "[Problem Solving - Baekjoon] 14002 가장 긴 증가하는 부분 수열 4"
date: 2020-12-26 14:55:00.000000000 +09:00
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
- DP
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-14002/"
---
# [Baekjoon Online Judge] 14002 가장 긴 증가하는 부분 수열 4

## 문제
수열 A가 주어졌을 때, 가장 긴 증가하는 부분 수열을 구하는 프로그램을 작성하시오.

예를 들어, 수열 A = {10, 20, 10, 30, 20, 50} 인 경우에 가장 긴 증가하는 부분 수열은 A = {10, 20, 10, 30, 20, 50} 이고, 길이는 4이다.

### 입력
첫째 줄에 수열 A의 크기 N (1 ≤ N ≤ 1,000)이 주어진다.

둘째 줄에는 수열 A를 이루고 있는 Ai가 주어진다. (1 ≤ Ai ≤ 1,000)

### 출력
첫째 줄에 수열 A의 가장 긴 증가하는 부분 수열의 길이를 출력한다.

둘째 줄에는 가장 긴 증가하는 부분 수열을 출력한다. 그러한 수열이 여러가지인 경우 아무거나 출력한다.

### 예제

- input

```java
6
10 20 10 30 20 50
```

- output

```java
4
10 20 30 50
```

### 분류
- 다이나믹프로그래밍

## 풀이

### 문제 파악
- [11053 가장 긴 증가하는 부분 수열](http://dawoonjeong.com/algorithm-problem-solving-baekjoon-11053/) 와 유사한 문제
- dp[i] = Math.max(dp[i], dp[j]+1)


|           | (i=0) 10 | (i=1) 20 | (i=2) 10 | (i=3) 30 | (i=4) 20 | (i=5) 50 |
|:---------:|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|
|           |    1     |    1     |   1      |   1      |   1      |   1      |
| (j=0)  10 |    1     |    2     |   1      |   2      |   2      |   2      |
| (j=1)  20 |    -     |    -     |   1      |   3      |   2      |   3      |
| (j=2)  10 |    -     |    -     |  -       |   3      |   2      |   3      |
| (j=3)  30 |    -     |    -     |  -       |  -       |   2      |   4      |
| (j=4)  20 |    -     |    -     |  -       |  -       |  -       |   4      |
| (j=5)  50 |    -     |    -     |  -       |  -       |  -       |  -       |
|

### 구현

- **틀림 (반례케이스를 못 찾음)**

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem14002/Main.java)

- 최대값의 위치도 찾아야함
- 최대값의 위치 : index = 5;

```java
for (int i = 1; i < n; i++) {
    dp[i] = 1;
    for (int j = 0; j < i; j++) {
        if ((arr[j] < arr[i]) && (dp[i] < dp[j]+1) ) {
            dp[i] = dp[j]+1;
            //i를 위해 참조한 인덱스 j저장
            reverse[i] = j;
        }
    }
    //최대값을 가진 dp의 index 구하기
    if (dp[index] < dp[i]) {
        index = i;
    }
}

```

- reverse[] = 0 0 0 1 0 3
- 최대값index 로 찾은  reverse[index] = 3 <-최대값을만들기 위해 참조한  index  
- reverse[3] = 1
- reverse[1] = 0
- 50 30 20 10 이렇게 찾아주기

```java
while(reverse[index] != index) {
   // list.add(arr[index]);
    stack.push(arr[index]);
    index = reverse[index];
}
```

-  ArrayList 로 담아서 역순으로 출력해도 되고

```java
ArrayList<Integer> list = new ArrayList<Integer>();

list.add(arr[index]);

for (int i = list.size()-1 ; i >= 0; i--) {
    sb.append(list.get(i) + " ");
}
```

- stack 에 담아서 pop해도 됨

```java
Stack<Integer> stack =new Stack<Integer>();

stack.push(arr[index]);

while(!stack.isEmpty()) {
    sb.append(stack.pop() + " ");
}
```


---

#### references
<https://www.acmicpc.net/problem/14002>
