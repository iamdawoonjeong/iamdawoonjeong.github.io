---
layout: single
title: "[Problem Solving - Baekjoon] 1987 알파벳"
date: 2020-11-28 14:25:00.000000000 +09:00
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
- backtracking
- n-queen
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1987/"
---
# [Baekjoon Online Judge] 1987

## 문제
세로 R칸, 가로 C칸으로 된 표 모양의 보드가 있다. 보드의 각 칸에는 대문자 알파벳이 하나씩 적혀 있고, 좌측 상단 칸 (1행 1열) 에는 말이 놓여 있다.

말은 상하좌우로 인접한 네 칸 중의 한 칸으로 이동할 수 있는데, 새로 이동한 칸에 적혀 있는 알파벳은 지금까지 지나온 모든 칸에 적혀 있는 알파벳과는 달라야 한다. 즉, 같은 알파벳이 적힌 칸을 두 번 지날 수 없다.

좌측 상단에서 시작해서, 말이 최대한 몇 칸을 지날 수 있는지를 구하는 프로그램을 작성하시오. 말이 지나는 칸은 좌측 상단의 칸도 포함된다.

### 입력
첫째 줄에 R과 C가 빈칸을 사이에 두고 주어진다. (1 ≤ R,C ≤ 20) 둘째 줄부터 R개의 줄에 걸쳐서 보드에 적혀 있는 C개의 대문자 알파벳들이 빈칸 없이 주어진다.

### 출력
첫째 줄에 말이 지날 수 있는 최대의 칸 수를 출력한다.

### 예제

- input

```java
2 4
CAAB
ADCB
```

- output

```java
3
```

### 분류
- 백트래킹

## 풀이

### 문제 파악
- 말은 상하좌우로 이동 가능
- 지금 까지 지나온 모든 알파벳과는 달라야 함  


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1987/Main.java)

- 상, 하, 좌, 우 이동좌표를 미리 만들어 놓고 한 좌표에서 모두다 체크

```java
dx = new int[]{-1, 1, 0, 0};
dy = new int[]{0, 0, -1, 1};
```

- 입력받은 알파벳을 int형으로 바꾸어 체크

```java
for (int i = 0; i < r; i++) {
    String str = br.readLine();
    for (int j = 0; j < c; j++) {
        arr[i][j] = str.charAt(j)- 'A';
    }
}
```

- bfs기법 확인

```java
public static void bfs(int x, int y, int depth) {
    if (visited[arr[x][y]]) {
        result = Math.max(result, depth);
        return;
    }else {
        visited[arr[x][y]] = true;
        for (int i = 0; i < 4; i++) {
            int nx = x + dx[i];
            int ny = y + dy[i];
            if(nx >= 0 && nx < r && ny >= 0 && ny < c) {
                bfs(nx, ny, depth+1);
            }
        }
        visited[arr[x][y]] = false;
    }
}
```

---

#### references
<https://www.acmicpc.net/problem/1987>
