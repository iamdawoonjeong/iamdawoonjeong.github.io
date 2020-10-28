---
layout: single
title: "[Problem Solving - Baekjoon] 11650 좌표 정렬하기"
date: 2020-10-19 18:31:00.000000000 +09:00
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
- sort
- baekjoon
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-11650/"
---
# [Baekjoon Online Judge] 11650 좌표 정렬하기

## 문제
- 2차원 평면 위의 점 N개가 주어진다. 좌표를 x좌표가 증가하는 순으로, x좌표가 같으면 y좌표가 증가하는 순서로 정렬한 다음 출력하는 프로그램을 작성하시오.

### 입력
- 첫째 줄에 점의 개수 N (1 ≤ N ≤ 100,000)이 주어진다. 둘째 줄부터 N개의 줄에는 i번점의 위치 xi와 yi가 주어진다. (-100,000 ≤ xi, yi ≤ 100,000) 좌표는 항상 정수이고, 위치가 같은 두 점은 없다.

### 출력
- 첫째 줄부터 N개의 줄에 점을 정렬한 결과를 출력한다.

### 예제
- input
```java
5
3 4
1 1
1 -1
2 2
3 3
```

- output
```java
1 -1
1 1
2 2
3 3
3 4
```

### 분류
- 정렬

## 풀이

### 문제 파악
- (x,y)의 좌표를 정렬하는데 1순위는 x좌표 오름차순, 2순위는 y좌표 오름차순 순

```java
5   // 좌표수의 갯수
3 4 // 좌표
1 1
1 -1
2 2
3 3
```

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem11650/Main.java)

```java
Arrays.sort(arr, new Comparator<int[]>() {
    @Override
    public int compare(int[] o1, int[] o2) {
		//x좌표 값이  같다면 (0번째 인덱스의 값이  같다면)
        if (o1[0] == o2[0]) {
			//y좌표를 비교해서 정렬 (1번째 인덱스의 값을 비교)
            return  Integer.compare(o1[1], o2[1]);
        }else
			//x좌표 값이 같지 않다면 x좌표 정렬  
            return Integer.compare(o1[0], o2[0]);
        }
});
```

---

#### references
<https://www.acmicpc.net/problem/11650>
