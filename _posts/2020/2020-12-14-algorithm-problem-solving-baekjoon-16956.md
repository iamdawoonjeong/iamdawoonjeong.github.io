---
layout: single
title: "[Problem Solving - Baekjoon] 16956 늑대와 양"
date: 2020-12-14 20:40:00.000000000 +09:00
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
- search
- graph
- vector
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-16956/"
---
# [Baekjoon Online Judge] 16956 늑대와 양

## 문제
크기가 R×C인 목장이 있고, 목장은 1×1 크기의 칸으로 나누어져 있다. 각각의 칸에는 비어있거나, 양 또는 늑대가 있다. 양은 이동하지 않고 위치를 지키고 있고, 늑대는 인접한 칸을 자유롭게 이동할 수 있다. 두 칸이 인접하다는 것은 두 칸이 변을 공유하는 경우이다.

목장에 울타리를 설치해 늑대가 양이 있는 칸으로 갈 수 없게 하려고 한다. 늑대는 울타리가 있는 칸으로는 이동할 수 없다. 울타리를 설치해보자.

### 입력
첫째 줄에 목장의 크기 R, C가 주어진다.

둘째 줄부터 R개의 줄에 목장의 상태가 주어진다. '.'는 빈 칸, 'S'는 양, 'W'는 늑대이다.

### 출력
늑대가 양이 있는 칸으로 갈 수 없게 할 수 있다면 첫째 줄에 1을 출력하고, 둘째 줄부터 R개의 줄에 목장의 상태를 출력한다. 울타리는 'D'로 출력한다. 울타리를 어떻게 설치해도 늑대가 양이 있는 칸으로 갈 수 있다면 첫째 줄에 0을 출력한다.

### 예제

- input

```java
6 6
..S...
..S.W.
.S....
..W...
...W..
......
```

- output

```java
1
..SD..
..SDW.
.SD...
.DW...
DD.W..
......
```

### 분류
- 그래프 이론
- 그래프 탐색
- 너비 우선 탐색
- 구성적

### 노트
- 이 문제는 설치해야 하는 울타리의 최소 개수를 구하는 문제가 아니다.

## 풀이

### 문제 파악
- 울타리를 어떻게 설치해도 늑대가 양이 있는 칸으로 갈 수 있는 여부를 체크  
- 최소 울타리를 구하는 문제가 아니기 때문에 양주변을 다 울타리로 막음


### 구현


[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem16956/Main.java)


- 늑대가 이동할 수 있는 위치에 대해서 미리 좌표를 시계방향으로 구하고 체크

```java
//시계방향체크
int[] dx = new int[]{0, 1, 0, -1};
int[] dy = new int[]{1, 0, -1, 0};
```


- 늑대의 위치 W에서 (dx,dy) 를 돌면서 양이 있는지 체크  

```java
boolean check = false;

for (int i = 0; i < r; i++) {
    for (int j = 0; j < c; j++) {
        //늑대의 위치에서
        if ("W".equals(arr[i][j])) {
            //시계방향으로 이동 해보기
            for (int k = 0; k < dx.length; k++) {
                int nextx = i + dx[k];
                int nexty = j + dy[k];

                if (nextx < 0 || nextx == r || nexty < 0 || nexty ==c) {
                    continue;
                }

                //이동했는데 양이 있다면
                if ("S".equals(arr[nextx][nexty])) {
                    //울타리 설치가 무의미
                    check = true;
                }
            }
        }
    }
}
```

- 양이 존재한다면 울타리설치 무의미
- 존재하지 않다면 모두다 울타리 설치 D 후 출력

```java
if (check){
    //울타리 설치 무의미한 경우 0출력
    System.out.println(0);
}else {
    //울타리를 설치할 수 있는 경우 1출력
    System.out.println(1);
    //최소 울타리갯수를 구하는게 아니므로
    for (int i = 0; i < r; i++) {
        for (int j = 0; j < c; j++) {
            if ( !(arr[i][j].equals("W")) &&  !(arr[i][j].equals("S"))) {
                //모두 자리에 울타리 설치
                arr[i][j] = "D";
            }
        }
    }

    //출력
    for (int i = 0; i < r; i++) {
        for (int j = 0; j < c; j++) {
            System.out.print(arr[i][j]);
        }
        System.out.println();
    }
}

```

- output : 출력결과과 예시출력과 다르나 채점 결과는 맞음. 이 문제는 최소 울타리를 구하는 문제가 아니기 때문에 빈 공간을 모두 울타리를 넣어주어도 맞게 됨

```java
DDSDDD
DDSDWD
DSDDDD
DDWDDD
DDDWDD
DDDDDD

```


### 벡터문제 방향문제 만났을때

- 시계방향

```java
dx = {0,1,0,-1}
dy = {1,0,-1,0}
```

-  반시계방향

```java
dx = {0,-1,0,1}
dy = {1,0,-1,0}
```

- 이차원 배열로 사용

```java
int[][] directions = new int[][] { { -1 , 0 }, { 1 , 0 }, { 0 , -1 }, { 0 , 1 } } ;
```

---

#### references
<https://www.acmicpc.net/problem/16956>
