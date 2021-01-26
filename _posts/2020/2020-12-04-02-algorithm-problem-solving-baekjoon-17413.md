---
layout: single
title: "[Problem Solving - Baekjoon] 17413 단어 뒤집기 2"
date: 2020-12-04 19:40:00.000000000 +09:00
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
- implementation
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-17413/"
---
# [Baekjoon Online Judge] 17413 단어 뒤집기 2

## 문제
문자열 S가 주어졌을 때, 이 문자열에서 단어만 뒤집으려고 한다.

먼저, 문자열 S는 아래와과 같은 규칙을 지킨다.

1. 알파벳 소문자('a'-'z'), 숫자('0'-'9'), 공백(' '), 특수 문자('<', '>')로만 이루어져 있다.
2. 문자열의 시작과 끝은 공백이 아니다.
3. '<'와 '>'가 문자열에 있는 경우 번갈아가면서 등장하며, '<'이 먼저 등장한다. 또, 두 문자의 개수는 같다.

태그는 '<'로 시작해서 '>'로 끝나는 길이가 3 이상인 부분 문자열이고, '<'와 '>' 사이에는 알파벳 소문자와 공백만 있다. 단어는 알파벳 소문자와 숫자로 이루어진 부분 문자열이고, 연속하는 두 단어는 공백 하나로 구분한다. 태그는 단어가 아니며, 태그와 단어 사이에는 공백이 없다.

### 입력
첫째 줄에 문자열 S가 주어진다. S의 길이는 100,000 이하이다.

### 출력
첫째 줄에 문자열 S의 단어를 뒤집어서 출력한다.


### 예제

- input

```java
baekjoon online judge
```

- output

```java
noojkeab enilno egduj
```

### 분류
- 구현

## 풀이

### 문제 파악
- <>안에 문자를 제외하고 공백을 기준으로 뒤집어서 출력
- [키로거](http://dawoonjeong.com/algorithm-problem-solving-baekjoon-5397/) 문제처럼 stack 을 활용


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem17413/Main.java)


- 뒤집어서 출력될 필요없는 문자는 StringBuilder 에 바로 붙여줌
- 뒤집어서 출력될 문자는 stack에 push 해주다가 공백기준으로 pop / < 만났을때 pop / swich 다 돌고 남아있을 수 있으니 마지막에 pop   

```java
boolean isTag = false;
Stack<Character> stack = new Stack<Character>();
StringBuilder sb = new StringBuilder();

for (char ch : input) {
    switch (ch) {
    case ' ': {
        if (!isTag) {
            while(!stack.isEmpty()) {
                sb.append(stack.pop());
            }
            sb.append(ch);
        }else {
            sb.append(ch);
        }
        break;

    } case '<': {
        while(!stack.isEmpty()) {
            sb.append(stack.pop());
        }
        isTag = true;
        sb.append(ch);
        break;

    } case '>': {
        isTag = false;
        sb.append(ch);
        break;

    } default:
        if (!isTag) {
            stack.push(ch);
        }else {
            sb.append(ch);
        }
        break;
    }
}

while(!stack.isEmpty()) {
    sb.append(stack.pop());
}

System.out.println(sb.toString());
```


---

#### references
<https://www.acmicpc.net/problem/17413>
