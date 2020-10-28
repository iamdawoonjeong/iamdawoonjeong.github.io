---
layout: single
title: "[Problem Solving - Baekjoon] 10930 SHA-256"
date: 2020-10-13 20:42:00.000000000 +09:00
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
- hash
- baekjoon
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-10930/"
---
# [Baekjoon Online Judge] 10930 SHA-256

## 문제
문자열 S가 주어졌을 때, SHA-256 해시값을 구하는 프로그램을 작성하시오.

### 입력
첫째 줄에 문자열 S가 주어진다. S는 알파벳 대문자와 소문자, 그리고 숫자로만 이루어져 있으며, 길이는 최대 50이다.

### 출력
첫째 줄에 S의 SHA-256 해시값을 출력한다.

### 예제

- input
```java
Baekjoon
```

- output
```java
9944e1862efbb2a4e2486392dc6701896416b251eccdecb8332deb7f4cf2a857
```

### 분류
- 해시

## 풀이

### 문제 파악
- 문제에서 나왔듯이 해싱알고리즘은 SHA-256를 이용하여 해시값을 구함

[참고:해시](http://dawoonjeong.com/algorithm-hash/)

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem10930/Main.java)

- 해시알고리즘을 이용하여  구하기

```java
MessageDigest digest = MessageDigest.getInstance("SHA-256");
byte[] hash = digest.digest(S.getBytes("UTF-8"));
StringBuffer hexString = new StringBuffer();

for (int i = 0; i < hash.length; i++) {
    String hex = Integer.toHexString(0xff&hash[i]);
    if(hex.length() == 1 ) {
        hexString.append('0');
    }
    hexString.append(hex);
}

result = hexString.toString();
```

---

#### references
<https://www.acmicpc.net/problem/10930>
