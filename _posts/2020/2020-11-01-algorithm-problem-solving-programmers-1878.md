---
layout: single
title: "[Problem Solving - Programmers] 1878 나머지 한 점"
date: 2020-11-01 22:48:00.000000000 +09:00
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
- programmers
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-programmers-1878/"
---
# [Programmers] 1878 나머지 한 점

## 문제
직사각형을 만드는 데 필요한 4개의 점 중 3개의 좌표가 주어질 때, 나머지 한 점의 좌표를 구하려고 합니다. 점 3개의 좌표가 들어있는 배열 v가 매개변수로 주어질 때, 직사각형을 만드는 데 필요한 나머지 한 점의 좌표를 return 하도록 solution 함수를 완성해주세요. 단, 직사각형의 각 변은 x축, y축에 평행하며, 반드시 직사각형을 만들 수 있는 경우만 입력으로 주어집니다.


### 제한사항
v는 세 점의 좌표가 들어있는 2차원 배열입니다.
v의 각 원소는 점의 좌표를 나타내며, 좌표는 [x축 좌표, y축 좌표] 순으로 주어집니다.
좌표값은 1 이상 10억 이하의 자연수입니다.
직사각형을 만드는 데 필요한 나머지 한 점의 좌표를 [x축 좌표, y축 좌표] 순으로 담아 return 해주세요.


### 입출력 예

| v   | result |
|:--------:|:--------:|
|  [[1, 4], [3, 4], [3, 10]] | [1, 10] |
|  [[1, 1], [2, 2], [1, 2]]  | [2, 1] |

### 입출력 예 설명
입출력 예 #1
세 점이 [1, 4], [3, 4], [3, 10] 위치에 있을 때, [1, 10]에 점이 위치하면 직사각형이 됩니다.

입출력 예 #2
세 점이 [1, 1], [2, 2], [1, 2] 위치에 있을 때, [2, 1]에 점이 위치하면 직사각형이 됩니다.


## 풀이

### 문제 파악
- 직사각형을 만드는데 세 점을 이용하여 나머지 한 점 알기

```java
 [[1, 4], [3, 4], [3, 10]]
```

- 2개의 점의 x좌표가 같음
- 2개의 점의 y좌표가 같음
- 위의 두개의 조건을 이용하여 x, y 좌표가 각각 한 개인 것들을 구해주면 됨

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/programmers/lessons1878/Solution.java)

- hash set을 이용하여 각 x, y좌표의 수를 담음

```java
HashMap<Integer, Integer> xMap = new HashMap<>();
HashMap<Integer, Integer> yMap = new HashMap<>();

for (int i = 0 ; i < v.length ; i++){

    if (xMap.containsKey(v[i][0])){
        xMap.replace(v[i][0], xMap.get(v[i][0]) + 1);
    }else {
        xMap.put(v[i][0], 1);
    }
}

for (int i = 0 ; i < v.length ; i++){

    if (yMap.containsKey(v[i][1])){
        yMap.replace(v[i][1], yMap.get(v[i][1]) + 1);
    }else {
        yMap.put(v[i][1], 1);
    }
}
```

- 좌표의 갯수가 한개씩인 것들이 나머지 한 점이 됨

```java
for (int key : xMap.keySet()){

    int value = xMap.get(key);
    if (value == 1 ){
        answer[0]  = key;
    }
}

for (int key : yMap.keySet()){
    int value = yMap.get(key);
    if (value == 1 ){
        answer[1] = key;
    }
}
```

---

#### references
<https://www.acmicpc.net/problem/10989>
