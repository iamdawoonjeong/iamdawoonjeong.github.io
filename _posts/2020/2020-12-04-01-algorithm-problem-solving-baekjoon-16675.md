---
layout: single
title: "[Problem Solving - Baekjoon] 16675 두 개의 손"
date: 2020-12-04 19:30:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-16675/"
---
# [Baekjoon Online Judge] 16675 두 개의 손

## 문제
민성이와 태경이는 고려대학교에서 알아주는 가위바위보의 최고수들이다. 이들은 기존의 가위바위보에 질린 나머지, 2개의 손을 모두 이용하여 가위바위보를 즐기는 경지에 이르렀다.

먼저, 둘이 동시에 “가위, 바위, 보”를 외치며 두 개의 손을 각각 가위, 바위, 보 중 하나로 설정하여 공개한다. 그 자리에서 서로 3초간 호흡을 가다듬은 후, 동시에 왼손을 낼지 오른손을 낼지를 결정한다. 민성이와 태경이는 최고수들끼리의 대결이라는 압박감에 의해 가끔 판단력이 흐려질 때가 있어서, 실수로 왼손과 오른손에 같은 동작을 취할 수도 있다.

당신은 민성이와 태경이의 왼손과 오른손의 상태가 주어졌을 때, 민성이 또는 태경이가 적절히 왼손 또는 오른손을 선택하여 가위바위보에서 무조건 이기는 방법이 있는지 없는지를 알려고 한다.

### 입력
첫 번째 줄에 차례로 ML, MR, TL, TR이 공백으로 구분되어 주어진다. 차례대로 민성이의 왼손과 오른손, 태경이의 왼손과 오른손의 상태를 나타낸다.

위 4개의 값들은 “S”, “R”, “P” 중 하나이며, 각각 가위, 바위, 보를 의미한다.

### 출력
첫 번째 줄에 민성이가 무조건 이길 수 있다면 “MS”, 태경이가 무조건 이길 수 있다면 “TK”, 누가 이길 지 확답할 수 없다면 “?”를 쌍따옴표를 제외하고 출력한다.

가위바위보에서 가위는 보를 이기고, 바위는 가위를 이기며, 보는 바위를 이긴다. 같은 손동작끼리는 승부가 나지 않는다 (비긴다).

### 예제1

- input

```java
R S P R
```

- output

```java
?
```

### 예제2

- input

```java
R R S S
```

- output

```java
MS
```

### 예제3

- input

```java
P P S R
```

- output

```java
TK
```

### 분류


## 풀이

### 문제 파악

- 가위바위보 하나빼기 문제
- 가위 0 보 1 바위 2 로 치환후 모듈러연산활용
- 가위일때 이기는 것은 보 : (0+2)%3 = 2
- 보일때 이기는 것은 가위 : (1+2)%3 = 0
- 바위일때 이기는 것은 보 : (2+2)%3 = 1



### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem16675/Main.java)


- 가위바위보 문자를 각 0,1,2로 치환

```java
input = input.replace("S", "0"); //S 가위
input = input.replace("P", "1"); //P 보
input = input.replace("R", "2"); //R 바위
```

-  모듈러 연산으로 구하기

```java
//모듈러연산 이용
if (ml == mr && ((ml+2)%3 == tl || (ml+2)%3 == tr)) {
    //민성이가 같은걸 동시에 낸 상태에서 태성이가 이기는 경우
    System.out.println("TK");

}else if (tl == tr && ( (tl+2)%3 == ml || (tl+2)%3 == mr)) {
    //태성이가 같은걸 동시에 낸 상태에서민성이가 이기는 경우
    System.out.println("MS");
}else {
    System.out.println("?");
}    
```

---

#### references
<https://www.acmicpc.net/problem/16675>
