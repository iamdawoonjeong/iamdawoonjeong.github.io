---
layout: single
title: "[Problem Solving - Baekjoon] 2110 공유기설치"
date: 2020-10-29 22:00:00.000000000 +09:00
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
- binary search
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-2110/"
---
# [Baekjoon Online Judge] 2110 공유기설치

## 문제
도현이의 집 N개가 수직선 위에 있다. 각각의 집의 좌표는 x1, ..., xN이고, 집 여러개가 같은 좌표를 가지는 일은 없다.

도현이는 언제 어디서나 와이파이를 즐기기 위해서 집에 공유기 C개를 설치하려고 한다. 최대한 많은 곳에서 와이파이를 사용하려고 하기 때문에, 한 집에는 공유기를 하나만 설치할 수 있고, 가장 인접한 두 공유기 사이의 거리를 가능한 크게 하여 설치하려고 한다.

**C개의 공유기를 N개의 집에 적당히 설치해서, 가장 인접한 두 공유기 사이의 거리를 최대로 하는 프로그램을 작성**하시오.

### 입력
첫째 줄에 집의 개수 N (2 ≤ N ≤ 200,000)과 공유기의 개수 C (2 ≤ C ≤ N)이 하나 이상의 빈 칸을 사이에 두고 주어진다. 둘째 줄부터 N개의 줄에는 집의 좌표를 나타내는 xi (1 ≤ xi ≤ 1,000,000,000)가 한 줄에 하나씩 주어진다.

### 출력
첫째 줄에 가장 인접한 두 공유기 사이의 최대 거리를 출력한다.

### 예제

- input

```java
5 3
1
2
8
4
9
```

- output

```java
3
```

### 분류
- 이진탐색

## 풀이

### 문제 파악

- C개의 공유기를 N개에 집에 설치
- 가장 인접한 두 공유기 사이의 거리를 최대로 하는 프로그램을 작성

```java
5 3   //N :집의 갯수, C : 공유기 갯수
1     //집의 좌표
2
8
4
9
```

[참고: 이진검색](http://dawoonjeong.com/algorithm-search/)


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2110/Main.java)

- 집 좌표 오름차순 정렬 해주기

```java
Arrays.sort(arr);
```

- start : 공유기 최소 간격 = 1
- end : 공유기 최대 간격 (9-1) = 8
- 첫번째 집에 공유기 설치 후, 공유기 간격을 (최소간격 + 최대간격)/2 (=mid)로 구해서 설치해보기
- 공유기 설치 갯수(count)가 주어진 공유기 갯수(C) 보다 큰 경우에는 기존간격보다 1큰 값(start=mid+1)을 최소간격으로 주고 구해보기
- 공유기 설치 갯수(count)가 주어진 공유기 갯수(C) 보다 작은경우에는 기존간격보다 1 줄인 값(end=mid-1)을 최대 간격으로 주고 구해보기
- 이것이 바로 이진 탐색

```java
int start  = 1;
int end = arr[N-1]-arr[0];

int result = 0;

while(start <= end ) {
    int value = arr[0];
    int count = 1;
    int mid = (start+end)/2;

    for (int i = 1; i < N; i++) {
        if (arr[i] >= value + mid) {
            value= arr[i];
            count++;
        }
    }

    if (count >= C ) {
        start = mid + 1;
        result = mid;
    }else{
        end = mid-1;
    }
}
```

---

#### references
<https://www.acmicpc.net/problem/2110>
