---
layout: single
title: "[Problem Solving - Baekjoon] 16768 Mooyo Mooyo"
date: 2021-01-25 21:10:00.000000000 +09:00
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
- bfs
- dfs
- flood fill
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-16768/"
---
# [Baekjoon Online Judge] 16768 Mooyo Mooyo

## 문제
With plenty of free time on their hands (or rather, hooves), the cows on Farmer John's farm often pass the time by playing video games. One of their favorites is based on a popular human video game called Puyo Puyo; the cow version is of course called Mooyo Mooyo.

The game of Mooyo Mooyo is played on a tall narrow grid N cells tall and 10 cells wide. Here is an example with :

0000000000
0000000300
0054000300
1054502230
2211122220
1111111223

Each cell is either empty (indicated by a 0), or a haybale in one of nine different colors (indicated by characters 1..9). Gravity causes haybales to fall downward, so there is never a 0 cell below a haybale.

Two cells belong to the same connected region if they are directly adjacent either horizontally or vertically, and they have the same nonzero color. Any time a connected region exists with at least K cells, its haybales all disappear, turning into zeros. If multiple such connected regions exist at the same time, they all disappear simultaneously. Afterwards, gravity might cause haybales to fall downward to fill some of the resulting cells that became zeros. In the resulting configuration, there may again be connected regions of size at least K cells. If so, they also disappear (simultaneously, if there are multiple such regions), then gravity pulls the remaining cells downward, and the process repeats until no connected regions of size at least K exist.

Given the state of a Mooyo Mooyo board, please output a final picture of the board after these operations have occurred.

### 입력
The first line of input contains N and K. The remaining N lines specify the initial state of the board.

### 출력
Please output N lines, describing a picture of the final board state.

### 예제

- input

```java
6 3
0000000000
0000000300
0054000300
1054502230
2211122220
1111111223
```

- output

```java
0000000000
0000000000
0000000000
0000000000
1054000000
2254500000
```

### 분류
- DFS
- BFS

## 풀이

### 문제 파악

- 뿌요뿌요 문제
- n개의 row
- 같은 숫자가 k개 이상인 경우 제거됨 (숫자 0은 제외)  

```java
6 3  // n , k
0000000000 //n gird
0000000300
0054000300
1054502230
2211122220
1111111223
```

- [1] DFS로 탐색하여 같은 숫자가 K 개 이상인 숫자를 찾음 : dfs()
- arr[3] [6] = 2 는 8개
- arr[4] [2] = 1 은 10 개  

- [2] K개 이상인 숫자는 DFS로 다시 탐색하여 0으로 바꿔줌 : dfs2()
```java
0000000000  
0000000300
0054000300
1054500030
2200000000
0000000003
```

- [3] 0인것들을 down 시켜 없애줌

```java
0000000000  
0000000000
0000000000
0000000000
1054000300
2254500333
```

- [4] while 반복 하여 1. 부터 반복
- [5] (반복)[1] DFS로 탐색하여 같은 숫자가 K 개 이상인 숫자를 찾음 : dfs()
- arr[4] [7] = 3 이 4개

- [6] [1] K개 이상인 숫자는 DFS로 다시 탐색하여 0으로 바꿔줌 : dfs2()

```java
0000000000  
0000000000
0000000000
0000000000
1054000000
2254500000
```

- [7] 0인것들을 down 시켜 없애줌

```java
0000000000  
0000000000
0000000000
0000000000
1054000000
2254500000
```
### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem16768/Main.java)

```java
while(true) {
    boolean isExist = false;  //바뀌는게 존재 할때까지

    visited = new boolean[n][10];
    removed = new boolean[n][10]; // 지워도 되는가?

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < 10; j++) {

            if (arr[i][j] == 0 || visited[i][j]) {
                //넘어감
                continue;
            }

            int result = dfs(i, j); // dfs가 맞으면 갯수세기

            if (result >= k ) {
                dfs2(i, j, arr[i][j]); //같은수 remove
                isExist = true; //바뀜
            }

        }
    }

    //바뀌는게 없을때까지
    if (!isExist) {
        break;
    }

    down(); //내리기
}
```

- dfs 탐색으로 같은숫자가 3개이상인 것 찾아내기  

```java
public static int dfs(int i, int j) {

    //방향벡터
    int[] dx = new int[] {0, 1, 0, -1};
    int[] dy = new int[] {1, 0, -1, 0};

    visited[i][j] = true;
    int result = 1;

    for (int k = 0; k < 4; k++) {
        int nextX = i + dx[k];
        int nextY = j + dy[k];

        //구간내 있는지 체크
        if ( nextX < 0 || nextX >= n || nextY < 0 || nextY >= 10 ) {
            continue;
        }

        //지금숫자와 다음숫자가 다르거나, 방문 이력이 여부 체크
        if ((arr[nextX][nextY] != arr[i][j] )  || (visited[nextX][nextY])) {
            continue;
        }
        result += dfs(nextX, nextY);

    }

    return result ;

}
```

- 다시 dfs로 탐색하여 찾아낸 숫자 value 를 0으로 지우기  

```java
    public static void dfs2(int i, int j, int  value) {

        int[] dx = new int[]{0, 1, 0, -1};
        int[] dy = new int[]{1, 0, -1, 0};

        arr[i][j] = 0;
        removed[i][j] = true;

        for (int k = 0; k < 4; k++) {
            int nextX = i + dx[k];
            int nextY = j + dy[k];

            if ( nextX < 0 || nextX >= n || nextY < 0 || nextY>= 10) {
                continue;
            }

            if ((value != arr[nextX][nextY]) || removed[nextX][nextY] ) {
                continue;
            }
            dfs2(nextX, nextY, value);
        }

    }
```

- 중간에 끼인 0 을 다운 시켜 주기

```java
public static void down() {
    for (int i = 0; i < 10; i++) {
        ArrayList<Integer> temp = new ArrayList<Integer>();
        for (int j = 0; j < n; j++) {
            if ( arr[j][i] != 0 ) {
                temp.add(arr[j][i]);
            }
        }
        for (int j = 0; j < n-temp.size(); j++) {
            arr[j][i] = 0 ;
        }
        for (int j = n-temp.size(); j < n ; j++) {
            arr[j][i] = temp.get(j - (n - temp.size()));
        }
    }

}
```

---

#### references
<https://www.acmicpc.net/problem/16768>
