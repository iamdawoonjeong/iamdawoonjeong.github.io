---
layout: single
title: "[Problem Solving - Baekjoon] 2250 트리의 높이와 너비"
date: 2020-11-05 22:47:00.000000000 +09:00
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
- tree
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-2250/"
---
# [Baekjoon Online Judge] 2250 트리의 높이와 너비

## 문제
이진트리를 다음의 규칙에 따라 행과 열에 번호가 붙어있는 격자 모양의 틀 속에 그리려고 한다. 이때 다음의 규칙에 따라 그리려고 한다.

1. 이진트리에서 같은 레벨(level)에 있는 노드는 같은 행에 위치한다.
2. 한 열에는 한 노드만 존재한다.
3. 임의의 노드의 왼쪽 부트리(left subtree)에 있는 노드들은 해당 노드보다 왼쪽의 열에 위치하고, 오른쪽 부트리(right subtree)에 있는 노드들은 해당 노드보다 오른쪽의 열에 위치한다.
4. 노드가 배치된 가장 왼쪽 열과 오른쪽 열 사이엔 아무 노드도 없이 비어있는 열은 없다.

이와 같은 규칙에 따라 이진트리를 그릴 때 각 레벨의 너비는 그 레벨에 할당된 노드 중 가장 오른쪽에 위치한 노드의 열 번호에서 가장 왼쪽에 위치한 노드의 열 번호를 뺀 값 더하기 1로 정의한다. 트리의 레벨은 가장 위쪽에 있는 루트 노드가 1이고 아래로 1씩 증가한다.

아래 그림은 어떤 이진트리를 위의 규칙에 따라 그려 본 것이다. 첫 번째 레벨의 너비는 1, 두 번째 레벨의 너비는 13, 3번째, 4번째 레벨의 너비는 각각 18이고, 5번째 레벨의 너비는 13이며, 그리고 6번째 레벨의 너비는 12이다.

우리는 주어진 이진트리를 위의 규칙에 따라 그릴 때에 너비가 가장 넓은 레벨과 그 레벨의 너비를 계산하려고 한다. 위의 그림의 예에서 너비가 가장 넓은 레벨은 3번째와 4번째로 그 너비는 18이다. 너비가 가장 넓은 레벨이 두 개 이상 있을 때는 번호가 작은 레벨을 답으로 한다. 그러므로 이 예에 대한 답은 레벨은 3이고, 너비는 18이다.

임의의 이진트리가 입력으로 주어질 때 너비가 가장 넓은 레벨과 그 레벨의 너비를 출력하는 프로그램을 작성하시오

### 입력
첫째 줄에 노드의 개수를 나타내는 정수 N(1 ≤ N ≤ 10,000)이 주어진다. 다음 N개의 줄에는 각 줄마다 노드 번호와 해당 노드의 왼쪽 자식 노드와 오른쪽 자식 노드의 번호가 순서대로 주어진다. 노드들의 번호는 1부터 N까지이며, 자식이 없는 경우에는 자식 노드의 번호에 -1이 주어진다.

### 출력
첫째 줄에 너비가 가장 넓은 레벨과 그 레벨의 너비를 순서대로 출력한다. 너비가 가장 넓은 레벨이 두 개 이상 있을 때에는 번호가 작은 레벨을 출력한다.

### 예제
- input

```java
19        //노드의 개수 n (1 ≤ n ≤ 10,000)
1 2 3     //노드번호 , 왼쪽자식, 오른쪽자식
2 4 5
3 6 7
4 8 -1   //자식노드가 없는 경우 -1
5 9 10
6 11 12
7 13 -1
8 -1 -1
9 14 15
10 -1 -1
11 16 -1
12 -1 -1
13 17 -1
14 -1 -1
15 18 -1
16 -1 -1
17 -1 19
18 -1 -1
19 -1 -1
```

- output

```java
3 18    //너비가 가장 넓은 레벨 그 레벨의 너비
```

### 분류
- 트리 (중위순회)

## 풀이

### 문제 파악

| level |      width    |
|:-----:|:-------------:|
|   1   |   1           |
|   2   |  15-3+1 = 13  |
|   3   |  19-2+1 = 18  |
|   4   |  18-1+1 = 18  |
|   5   |  16-4+1 = 13  |
|   6   |  17-6+1 = 12  |

- 너비가 가장 넓은 너비는 18 이고 레벨은 3,4
- 레벨이 더 작은 수 출력
- 답은 3 18 
- 자식이 없는 경우 -1


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2250/Main.java)


- 노드 클래스를 따로 만들어 주어서 관리

```java
class Node{
    public int data;
    public int parent;
    public int left;
    public int right;

    public Node(int input, int left, int right, int parent) {
        this.data = input;
        this.parent = -1;
        this.left = left;
        this.right = right;
    }
}
```

- dfs 기법으로 탐색

```java
public static void dfs(int data, int level) {

    Node node = tree[data];

    levelDepth = Math.max(levelDepth, level);

    if (node.left != -1) {
        dfs(node.left, level+1);
    }

    levelMin[level] = Math.min(levelMin[level], nodeIndex);
    levelMax[level] =  Math.max(levelMax[level], nodeIndex);
    nodeIndex++;

    if(node.right != -1) {
        dfs(node.right, level+1);
    }
}
```


```java
// 노드를 각각 만들어줌
for (int i = 0; i <= n; i++) {
    tree[i] = new Node(i, -1, -1, -1);
    levelMin[i] = n;
    levelMax[i] = 0;
}

for (int i = 1; i <= n; i++) {
   st = new StringTokenizer(br.readLine());
   int data = Integer.parseInt(st.nextToken());
   int left = Integer.parseInt(st.nextToken());
   int right = Integer.parseInt(st.nextToken());

   //입력되 왼쪽, 오른쪽데이터값 저장
   tree[data].left = left;
   tree[data].right = right;

   //자식 노드가 없다면 부모노드 입력
   if( left != -1) {
       tree[left].parent = data;
   }

   //자식 노드가 없다면 부모노드 입력
   if ( right != -1) {
       tree[right].parent = data;
   }
}

for(int i = 1; i <= n; i++) {
    if(tree[i].parent == -1) {
        root = i;
    }
}

dfs(root, 1);

int resultLevel = 1;
int resultWidth = levelMax[1] - levelMin[1] + 1;

for (int i = 2; i <= levelDepth; i++) {
    int width = levelMax[i] - levelMin[i] +1;

    if (resultWidth < width) {
        resultLevel = i;
        resultWidth = width;
    }
}
```

---

#### references
<https://www.acmicpc.net/problem/2250>
