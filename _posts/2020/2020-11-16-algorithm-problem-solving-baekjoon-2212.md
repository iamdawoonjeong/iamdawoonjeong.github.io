---
layout: single
title: "[Problem Solving - Baekjoon] 2212 센서"
date: 2020-11-16 18:30:00.000000000 +09:00
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
- baekjooon
- greedy
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-2212/"
---
# [Baekjoon Online Judge] 2212 센서

## 문제
한국도로공사는 고속도로의 유비쿼터스화를 위해 고속도로 위에 N개의 센서를 설치하였다. 문제는 이 센서들이 수집한 자료들을 모으고 분석할 몇 개의 집중국을 세우는 일인데, 예산상의 문제로, 고속도로 위에 최대 K개의 집중국을 세울 수 있다고 한다.

각 집중국은 센서의 수신 가능 영역을 조절할 수 있다. 집중국의 수신 가능 영역은 고속도로 상에서 연결된 구간으로 나타나게 된다. N개의 센서가 적어도 하나의 집중국과는 통신이 가능해야 하며, 집중국의 유지비 문제로 인해 각 집중국의 수신 가능 영역의 길이의 합을 최소화해야 한다.

편의를 위해 고속도로는 평면상의 직선이라고 가정하고, 센서들은 이 직선 위의 한 기점인 원점으로부터의 정수 거리의 위치에 놓여 있다고 하자. 따라서, 각 센서의 좌표는 정수 하나로 표현된다. 이 상황에서 각 집중국의 수신 가능영역의 거리의 합의 최솟값을 구하는 프로그램을 작성하시오. 단, 집중국의 수신 가능영역의 길이는 0 이상이며 모든 센서의 좌표가 다를 필요는 없다.

### 입력
첫째 줄에 센서의 개수 N(1<=N<=10,000), 둘째 줄에 집중국의 개수 K(1<=K<=1000)가 주어진다. 셋째 줄에는 N개의 센서의 좌표가 한 개의 정수로 N개 주어진다. 각 좌표 사이에는 빈 칸이 하나 이상 있으며, 좌표의 절댓값은 1,000,000 이하이다.

### 출력
첫째 줄에 문제에서 설명한 최대 K개의 집중국의 수신 가능 영역의 길이의 합의 최솟값을 출력한다.

### 예제

- input

```java
6
2
1 6 9 3 6 7
```

- output

```java
5
```

### 분류
- 탐욕알고리즘

## 풀이

### 문제 파악
- n개의 집중국에 k개의 센서를 놓았을 때, 센서간의 거리의 최소합을 구하는 문제

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2212/Main.java)

- 집중국의 갯수가 센서의 갯수보다 크거나 같으면 센서간의 거리가 0이 됨으로, 0 출력하고 종료

```java
if (k >= n) {
    System.out.println(0);
    return;
}
```

- 집중국의 좌표를 구하고 오름차순으로 정렬

```java
int[] arr = new int[n];
for (int i = 0; i < n; i++) {
    arr[i] = Integer.parseInt(st.nextToken());
}

Arrays.sort(arr);
```

- 집중국 간의 거리를 입력받은 변수는 내림차순 정렬하여 가장 먼 거리를 쉽게 구할 수 있게 함 

```java
Integer[] distances = new Integer[n-1];
for (int i = 0; i < arr.length-1; i++) {
    distances[i] = arr[i+1] - arr[i] ;
}

Arrays.sort(distances, new Comparator<Integer>() {

    @Override
    public int compare(Integer o1, Integer o2) {
        return Integer.compare(o2, o1);
    }
});
```

-  집중국 간의 거리 중 가장 긴 거리 k-1 개를 0으로 셋팅 하면 가장 먼거리를 날려 버리고 센서를 설치 할 수 있음

```java 
for (int i = 0; i < k-1; i++) {
    distances [i]=0;
}
```

- 센서간의 거리 합 계산

```java
int sum = 0;
for (Integer integer : distances) {
    sum+=integer;
}
System.out.println(sum);
```

---
#### references
<https://www.acmicpc.net/problem/2212>