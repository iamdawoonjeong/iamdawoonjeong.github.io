---
layout: single
title: "[Problem Solving - Baekjoon] 1302 베스트셀러"
date: 2020-10-26 23:45:00.000000000 +09:00
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
- hashmap
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1302/"
---
# [Baekjoon Online Judge] 1302 베스트셀러

## 문제
김형택은 탑문고의 직원이다. 김형택은 계산대에서 계산을 하는 직원이다. 김형택은 그날 근무가 끝난 후에, 오늘 판매한 책의 제목을 보면서 가장 많이 팔린 책의 제목을 칠판에 써놓는 일도 같이 하고 있다.

오늘 하루 동안 팔린 책의 제목이 입력으로 들어왔을 때, 가장 많이 팔린 책의 제목을 출력하는 프로그램을 작성하시오.

### 입력
첫째 줄에 오늘 하루 동안 팔린 책의 개수 N이 주어진다. 이 값은 1,000보다 작거나 같은 자연수이다. 둘째부터 N개의 줄에 책의 제목이 입력으로 들어온다. 책의 제목의 길이는 50보다 작거나 같고, 알파벳 소문자로만 이루어져 있다.

### 출력
첫째 줄에 가장 많이 팔린 책의 제목을 출력한다. 만약 가장 많이 팔린 책이 여러 개일 경우에는 사전 순으로 가장 앞서는 제목을 출력한다.

### 예제
- input

```java
5
top
top
top
top
kimtop
```

- output

```java
top
```

### 분류


## 풀이

### 문제 파악
- 가장 많이 팔린 베스트셀러를 찾아 책 제목을 출력하되, 동일 제목이 있으면 사전순 출력

```java
5    // 팔린 책의 개수 N
top  // 팔린책 제목
top
top
top
kimtop
```

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1302/Main.java)

- 갯수와 제목을 담을 수 있는 HashMap함수 이용

```java
HashMap<String, Integer> map = new HashMap<String, Integer>();
```

- 제목이 담겨있으면 갯수 증가시켜주기

```java
for (int i = 0; i < n; i++) {
    String name = br.readLine();

    if ( map.containsKey(name)){
        map.replace(name,  map.get(name)+1);
    }else{
        map.put(name, 1);
    }

```

- hashmap의 max값을 찾으려고 value를 하나하나 확인
- 팔린 갯수가 같은 경우에는 compareTo를 이용하여 확인
    * 기준값.compareTo(비교대상)
    * 기준값 = 비교대상 : 0
    * 기준값 > 비교대상 : 양수
    * 기준값 < 비교대상 : 음수
- maxName이 key보다 사전순으로 뒤에 갈 경우, key보다 큰 값 이 매겨져서 maxName - key > 0 으로 음수가 나오는 경우가 key가 사전적으로 앞에 있는 경우가 됨

```java
int max = 0;
String maxName = "";
for (String key : map.keySet()) {
    int value = map.get(key);
    if (value > max) {
        max = value;
        maxName = key;
    }else if ((value == max) && ( maxName.compareTo(key) > 0)){
        max = value;
        maxName = key;
    }
}
```

---

#### references
<https://www.acmicpc.net/problem/1302>
