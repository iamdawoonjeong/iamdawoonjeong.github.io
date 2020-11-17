---
layout: single
title: "[Problem Solving - Baekjoon] 1781 컵라면"
date: 2020-11-18 00:17:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-1781/"
---
# [Baekjoon Online Judge] 1781 컵라면

## 문제
상욱 조교는 동호에게 N개의 문제를 주고서, 각각의 문제를 풀었을 때 컵라면을 몇 개 줄 것인지 제시 하였다. 하지만 동호의 찌를듯한 자신감에 소심한 상욱 조교는 각각의 문제에 대해 데드라인을 정하였다.

| 문제 번호 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|:----:|:----:|:----:|:-----:|:-----:|:-----:|
| 데드라인 | 1 | 1 | 3 | 3 | 2 | 2 | 6 |
| 컵라면 수 | 6 | 7 | 2 | 1 | 4 | 5 | 1 |

위와 같은 상황에서 동호가 2, 6, 3, 1, 7, 5, 4 순으로 숙제를 한다면 2, 6, 3, 7번 문제를 시간 내에 풀어 총 15개의 컵라면을 받을 수 있다.

문제는 동호가 받을 수 있는 최대 컵라면 수를 구하는 것이다. 위의 예에서는 15가 최대이다.

문제를 푸는데는 단위 시간 1이 걸리며, 각 문제의 데드라인은 N 이하이다. 또, 각 문제를 풀 때 받을 수 있는 컵라면 수와 최대로 받을 수 있는 컵라면 수는 모두 32비트 정수형 범위 이내이다.


### 입력
첫 줄에 숙제의 개수 N (1<=N<=200,000)이 들어온다. 다음 줄부터 N+1번째 줄까지 i+1번째 줄에 i번째 문제에 대한 데드라인과 풀면 받을 수 있는 컵라면 수가 공백으로 구분되어 입력된다.

### 출력
첫 줄에 동호가 받을 수 있는 최대 컵라면 수를 출력한다.

### 예제
- input

```java
7
1 6
1 7
3 2
3 1
2 4
2 5
6 1
```

- output

```java
15
```

### 분류
- 탐욕알고리즘

## 풀이

### 문제 파악

- 각 데드라인별 더 큰 컵라면 수를 취득하는 탐욕 알고리즘
- 우선순위 큐를 이용하여 최소힙은 제거

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1781/Main.java)

- 입력받은 데드라인과 컵라면을 정렬
- 데드라인이 같을 경우 컵라면 오름차순으로 정렬 해주기

```java
Arrays.sort(arr, new Comparator<int[]>() {

    @Override
    public int compare(int[] o1, int[] o2) {
        if ( o1[0] == o2[0] ) {
            return Integer.compare(o1[1], o2[1]);
        }else {
            return Integer.compare(o1[0], o2[0]);
        }
    }
});
```

- 정렬 후 배열 상황

```java
1 6
1 7
2 4
2 5
3 1
3 2
6 1
```

- 우선순위 큐를 이용하면 큐에 1 : 7,  2 : 4, 2 : 5  이런 상황에서 최소인 데드라인 2의  컵라면 4 를 제거해 줌  

```java
PriorityQueue<Integer> queue = new PriorityQueue<Integer>();

for (int i = 0; i < arr.length; i++) {
    int deadline = arr[i][0];  //데드라인
    queue.add(arr[i][1]); //컵라면 갯수
    if (deadline < queue.size()) {
        queue.poll();
    }
}     
```


---

#### references
<https://www.acmicpc.net/problem/1781>
