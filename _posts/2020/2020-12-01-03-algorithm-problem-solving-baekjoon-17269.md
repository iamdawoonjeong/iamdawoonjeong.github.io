---
layout: single
title: "[Problem Solving - Baekjoon] 17269 이름궁합 테스트"
date: 2020-12-01 21:30:00.000000000 +09:00
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
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-17269/"
---
# [Baekjoon Online Judge] 17269 이름궁합 테스트

## 문제
시윤이는 좋아하는 이성이 생기면 가장 먼저 이름궁합부터 본다. 이름궁합을 보는 방법은 간단하다. 먼저 이름을 알파벳 대문자로 적는다. 각 알파벳 대문자에는 다음과 같이 알파벳을 적는데 필요한 획수가 주어진다. 예를 들어, 두 사람의 이름인 LEESIYUN, MIYAWAKISAKURA 를 같이 표현했을 때 다음과 같이 먼저 주어진 이름부터 한 글자씩 적는다.


두 사람의 이름을 알파벳 대문자로 표현한 뒤, 한 글자씩 번갈아가며 적는다.

예시 :  L M E I E Y S A I W Y A U K N I S A K U R A

예시처럼 이름이 남을 경우엔 뒤에 남은 글자인 S A K U R A를 맨 뒤에 적는다. 그러고 나서 알파벳을 대응하는 숫자로 바꾸고 각 숫자와 그 숫자의 오른쪽 숫자와 더한 것을 밑에 적는다. 더한 숫자가 10이 넘을 경우엔 일의 자리 수만 남긴다. 이 과정을 반복하여 숫자가 2개만 남았을 때 남은 숫자가 두 사람의 궁합이 좋을 확률이 된다.

### 입력
첫 번째 줄에 이름의 길이 N과 M을 받는다. (2 ≤ N, M ≤ 100)

다음 줄에 이름 A와 B를 입력받는다. 이름은 반드시 알파벳 대문자만 주어진다.

### 출력
A와 B의 이름궁합이 좋을 확률을 %로 출력한다. 단, 십의 자리가 0일 경우엔 일의 자리만 출력한다.

### 예제1
- input

```java
8 14
LEESIYUN MIYAWAKISAKURA
```

- output

```java
27%
```

### 예제2
- input

```java
2 2
AB CD
```

- output

```java
77%
```

- output

```java
27%
```

### 예제3
- input

```java
3 2
BOJ IN
```

- output

```java
1%
```

### 분류
- 구현

## 풀이

### 문제 파악

- 알파벳순으로 정해진 값으로 매칭하여 i + (i+1) 의 수를 합해서 다음수를 만들고
- 2자리가 될때까지 반복

### 구현

#### hash map을 이용하여 풀기

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem17269/Main.java)

- 알파벳에 횟수를 hashmap 에 넣어줌 (key 값 중복 불가)
- 배열로 해서 ascll코드를 이용하는 방법도 있음

```java
HashMap<String, Integer> map = new HashMap<>();

map.put("A", 3);
map.put("B", 2);
map.put("C", 1);
map.put("D", 2);
map.put("E", 4);
map.put("F", 3);
map.put("G", 1);
map.put("H", 3);
map.put("I", 1);
map.put("J", 1);
map.put("K", 3);
map.put("L", 1);
map.put("M", 3);
map.put("N", 2);
map.put("O", 1);
map.put("P", 2);
map.put("Q", 2);
map.put("R", 2);
map.put("S", 1);
map.put("T", 2);
map.put("U", 1);
map.put("V", 1);
map.put("W", 1);
map.put("X", 2);
map.put("Y", 2);
map.put("Z", 1);
```

- 두 이름에서 한 글자씩 가지고 오기

```java
String[] names= new String[N+M];
int i = 0;
int j = 0;
int index = 0;

while(i < N || j < M) {

    if (i < N) {
        names[index] = A[i];
        index++;
        i++;
    }

    if ( j < M) {
        names[index] = B[j];
        index++;
        j++;
    }
}
```

- 계산하는 부분
- 더한 수가 10이 넘을때는 1의 자리만 가지고 오기 (input%=10)
- 결과의 10의자리가 0일때는 제외 (int)result.get(0)%10*10

```java
public static void solution(ArrayList list) {

    ArrayList<Integer> result = new ArrayList<>();

    for (int i = 0; i < list.size()-1; i++) {
        int sum = (int) list.get(i) + (int) list.get(i+1);
        int input = sum;
        if (sum >= 10) {
            input %= 10;
        }
        result.add(input);
    }


    if (result.size() != 2 ) {
        solution(result);
    }else {

        System.out.println(String.format("%s", (int)result.get(0)%10*10 + result.get(1)%10) + "%");  
    }

}

```

#### 배열만 사용해서 풀기

---

#### references
<https://www.acmicpc.net/problem/17269>
