---
layout: single
title: "[Problem Solving - Baekjoon] 10814 나이순정렬"
date: 2020-10-19 18:26:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-10814/"
---
# [Baekjoon Online Judge] 10814 나이순정렬

## 문제
온라인 저지에 가입한 사람들의 나이와 이름이 가입한 순서대로 주어진다. 이때, 회원들을 나이가 증가하는 순으로, 나이가 같으면 먼저 가입한 사람이 앞에 오는 순서로 정렬하는 프로그램을 작성하시오.

### 입력
첫째 줄에 온라인 저지 회원의 수 N이 주어진다. (1 ≤ N ≤ 100,000)

둘째 줄부터 N개의 줄에는 각 회원의 나이와 이름이 공백으로 구분되어 주어진다. 나이는 1보다 크거나 같으며, 200보다 작거나 같은 정수이고, 이름은 알파벳 대소문자로 이루어져 있고, 길이가 100보다 작거나 같은 문자열이다. 입력은 가입한 순서로 주어진다.

### 출력
첫째 줄부터 총 N개의 줄에 걸쳐 온라인 저지 회원을 나이 순, 나이가 같으면 가입한 순으로 한 줄에 한 명씩 나이와 이름을 공백으로 구분해 출력한다.

### 예제
- input

```java
3
21 Junkyu
21 Dohyun
20 Sunyoung
```

- output

```java
20 Sunyoung
21 Junkyu
21 Dohyun
```

### 분류
- 정렬

## 풀이

### 문제 파악

- 나이순, 가입한순으로 정렬

```java
3          //회원수
21 Junkyu  //나이 이름
21 Dohyun
20 Sunyoung
```


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem10814/Main.java)

- Arrays.sort() 를 이용하여 1번째 인덱스를 정렬

```java
Arrays.sort(arr, new Comparator<String[]>() {

    @Override
    public int compare(String[] o1, String[] o2) {
        return Integer.compare(Integer.parseInt(o1[0]), Integer.parseInt(o2[0]));
    }
});
```

---

#### references
<https://www.acmicpc.net/problem/10814>
