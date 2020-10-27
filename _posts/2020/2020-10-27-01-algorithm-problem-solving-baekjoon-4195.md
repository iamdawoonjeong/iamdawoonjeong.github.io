---
layout: single
title: "[Problem Solving - Baekjoon] 4195 친구네트워크"
date: 2020-10-27 22:40:00.000000000 +09:00
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
- union-find
- recursive
- recursion
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-4195/"
---
# [Baekjoon Online Judge] 4195 친구네트워크

## 문제
민혁이는 소셜 네트워크 사이트에서 친구를 만드는 것을 좋아하는 친구이다. 우표를 모으는 취미가 있듯이, 민혁이는 소셜 네트워크 사이트에서 친구를 모으는 것이 취미이다.

어떤 사이트의 친구 관계가 생긴 순서대로 주어졌을 때, 두 사람의 친구 네트워크에 몇 명이 있는지 구하는 프로그램을 작성하시오.

친구 네트워크란 친구 관계만으로 이동할 수 있는 사이를 말한다.

### 입력
첫째 줄에 테스트 케이스의 개수가 주어진다. 각 테스트 케이스의 첫째 줄에는 친구 관계의 수 F가 주어지며, 이 값은 100,000을 넘지 않는다. 다음 F개의 줄에는 친구 관계가 생긴 순서대로 주어진다. 친구 관계는 두 사용자의 아이디로 이루어져 있으며, 알파벳 대문자 또는 소문자로만 이루어진 길이 20 이하의 문자열이다.

### 출력
친구 관계가 생길 때마다, 두 사람의 친구 네트워크에 몇 명이 있는지 구하는 프로그램을 작성하시오.

### 예제
- input

```java
2
3
Fred Barney
Barney Betty
Betty Wilma
3
Fred Barney
Betty Wilma
Barney Betty
```

- output

```java
2
3
4
2
2
4
```

### 분류
- 자료 구조
- 분리 집합
- 해시를 사용한 집합과 맵

## 풀이

### 문제 파악
- 해시활용
- Union-Find 알고리즘 이용 (합집합 찾기)

```java
2     // testCase
3     // F 친구 관계수
Fred Barney  // 친구관계 연결
Barney Betty
Betty Wilma
3
Fred Barney
Betty Wilma
Barney Betty
```

- 네트워크 연결되는 순서

![problem-solving-4195-01]({{ site.baseurl }}/assets/images/posts/2020/problem-solving-4195-01.png)


![problem-solving-4195-02]({{ site.baseurl }}/assets/images/posts/2020/problem-solving-4195-02.png)



### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/friendNetwork4195/Main.java)


- HashMap 이름을 담을 LIST를 만들고 이름을 넣음

```java
for (int i = 0; i < testCase; i++) {
    int F = Integer.parseInt(br.readLine());
    int index = 0;

    LIST = new HashMap<>();
    PARENT = new int[MAX];
    RANK = new int[MAX];
    RELATION = new int[MAX];

    Arrays.fill(RELATION, 1);

    for (int j = 0; j < F; j++) {
        StringTokenizer st = new StringTokenizer(br.readLine());
        String name1 = st.nextToken();
        String name2 = st.nextToken();

        if (!LIST.containsKey(name1)) {
            LIST.put(name1, index);
            PARENT[index] = index++;
        }

        if(!LIST.containsKey(name2)) {
            LIST.put(name2, index);
            PARENT[index] = index++;
        }

        union(LIST.get(name1), LIST.get(name2));

        bw.write(RELATION[find(LIST.get(name1))] + "\n");
    }
}
```

- 재귀용법으로 부모를 찾아서 부모 값을 반환 (find : 자기가 속한 집합을 찾음)

```java
public static int find(int u) {
    if (PARENT[u] == u ) {
        return u;
    }
    return (PARENT[u] = find(PARENT[u]));
}
```

- 찾은 부모끼리 비교해서 연산하여 연결 (union : 집합끼리를 합쳐 줌)

```java
public static void union(int u, int v) {
    int uR = find(u);
    int vR = find(v);

    if (uR == vR) {
        return;
    }

    if(RANK[uR] > RANK[vR]) {
        swap(uR, vR);
    }

    PARENT[uR] = vR;
    RELATION[vR] += RELATION[uR];

    if(RANK[uR] == RANK[vR]) {
        RANK[vR]++;
    }
}
```



---

#### references
<https://www.acmicpc.net/problem/4195>
<https://soobarkbar.tistory.com/180>
