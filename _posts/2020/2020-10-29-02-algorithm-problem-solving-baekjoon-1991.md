---
layout: single
title: "[Problem Solving - Baekjoon] 1991 트리 순회"
date: 2020-10-29 22:10:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-1991/"
---
# [Baekjoon Online Judge] 1991 트리 순회

## 문제
이진 트리를 입력받아 전위 순회(preorder traversal), 중위 순회(inorder traversal), 후위 순회(postorder traversal)한 결과를 출력하는 프로그램을 작성하시오.

### 입력
첫째 줄에는 이진 트리의 노드의 개수 N(1≤N≤26)이 주어진다. 둘째 줄부터 N개의 줄에 걸쳐 각 노드와 그의 왼쪽 자식 노드, 오른쪽 자식 노드가 주어진다. 노드의 이름은 A부터 차례대로 영문자 대문자로 매겨지며, 항상 A가 루트 노드가 된다. 자식 노드가 없는 경우에는 .으로 표현된다.

### 출력
첫째 줄에 전위 순회, 둘째 줄에 중위 순회, 셋째 줄에 후위 순회한 결과를 출력한다. 각 줄에 N개의 알파벳을 공백 없이 출력하면 된다.

### 예제
- input

```java
7
A B C
B D .
C E F
E . .
F . G
D . .
G . .
```

- output

```java
ABDCEFG
DBAECFG
DBEGFCA
```

### 분류
- 트리
- 재귀

## 풀이

### 문제 파악

```java
7     //7개의 노드
A B C // root - 왼쪽자식-오른쪽자식
B D . // . 자식이 없는 경우 (단말노드)
C E F
E . .
F . G
D . .
G . .
```

### 구현

- 가장 기본적인 트리순회를 묻는 문제로 몇 번 풀어봐도 좋을(?)문제

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1991/Main.java)

- 트리에 사용될 노드를 생성

```java
class Node{

    public char data;
    public Node left;
    public Node right;

    public Node(char input) {
        this.data = input;
    }
}
```

- 입력받은 값을 노드에 넣어줌

```java
public void add(char data, char left, char right) {

    // root가 비었을 경우
    if (null == root) {

        // 자식이 없는 경우를 제외하고 각 노드에 값 넣어주어 root 만들기
        if('.' != data ) {
            root = new Node(data);
        }
        if ('.' != left) {
            root.left = new Node(left);
        }
        if ( '.' != right) {
            root.right = new Node(right);
        }
    }else {

        // root 가 있을 경우
        search(root, data, left, right);
    }
}
```

- 현재 data의 node가 부모노드라면 left, right값을 넣어줌
- 부모 node가 아니라면 재귀호출을 통해 부모 위치를 찾아서 값을 넣어주게 됨

```java
public void search(Node root, char data, char left, char right) {

    // root 가 비었을 경우
    if(null == root) {
        return;
    }else if(root.data == data) {

        //입력된 데이터가 부모데이터일 경우 자식노드 값 넣어주기
        if ('.' != left) {
            root.left = new Node(left);
        }
        if('.' != right) {
            root.right = new Node(right);
        }
    }else {

        // 입력된 데이터가 root가 아닌 자식 노드에 있을 경우 재귀함수를 이용하여 부모위치 찾기
        search(root.left, data, left, right);
        search(root.right, data, left, right);
    }

}
```


- 순회

```java
/**
 * 전위 순회
 * @param root
 */
public void preorder(Node root) {

    System.out.print(root.data);

    if (null != root.left) {
        preorder(root.left);
    }

    if (null != root.right) {
        preorder(root.right);
    }
}

/**
 * 중위 순회
 * @param root
 */
public void inorder(Node root) {

    if (null != root.left) {
        inorder(root.left);
    }

    System.out.print(root.data);

    if (null != root.right) {
        inorder(root.right);
    }
}

/**
 * 후위 순회
 * @param root
 */
public void postorder(Node root) {

    if (null != root.left) {
        postorder(root.left);
    }

    if (null != root.right) {
        postorder(root.right);
    }

    System.out.print(root.data);
}
```

---

#### references
<https://www.acmicpc.net/problem/1991>  
<https://m.blog.naver.com/PostView.nhn?blogId=occidere&logNo=220899936160&proxyReferer=https:%2F%2Fwww.google.com%2F>
