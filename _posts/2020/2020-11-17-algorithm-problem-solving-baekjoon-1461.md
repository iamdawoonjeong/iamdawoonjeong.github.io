---
layout: single
title: "[Problem Solving - Baekjoon] 1461 도서관"
date: 2020-11-17 21:30:00.000000000 +09:00
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
- greedy
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1461/"
---
# [Baekjoon Online Judge] 1461 도서관

## 문제
세준이는 도서관에서 일한다. 도서관의 개방시간이 끝나서 세준이는 사람들이 마구 놓은 책을 다시 가져다 놓아야 한다. 세준이는 현재 0에 있고, 사람들이 마구 놓은 책도 전부 0에 있다. 각 책들의 원래 위치가 주어질 때, 책을 모두 제자리에 놔둘 때 드는 최소 걸음 수를 계산하는 프로그램을 작성하시오. 세준이는 한 걸음에 좌표 1칸씩 가며, 책의 원래 위치는 정수 좌표이다. 책을 모두 제자리에 놔둔 후에는 다시 0으로 돌아올 필요는 없다. 그리고 세준이는 한 번에 최대 M권의 책을 들 수 있다.

### 입력
첫째 줄에 책의 개수 N과, 세준이가 한 번에 들 수 있는 책의 개수 M이 주어진다. 둘째 줄에는 책의 위치가 주어진다. N은 10,000보다 작거나 같은 자연수이고, M은 10,000보다 작거나 같다. 책의 위치는 0이 아니며, 그 절댓값이 10,000보다 작거나 같다.

### 출력
첫째 줄에 정답을 출력한다.

### 예제

- input

```java
7 2
-37 2 -6 -39 -29 11 -28
```

- output

```java
131
```

### 분류
- 탐욕알고리즘


## 풀이

### 문제 파악
- 총 n개의 책을 m권씩 가져다 놓고 오는 걸음 수 구하는 문제(거리*2)
- 음수 위치의 책, 양수 위치의 책이 따로 있어서 따로 관리 해줌
- 마지막은 책을 가져다 놓고 안돌아와도 됨 (거리 *1 )
- PriorityQueue 를 이용하는 문제 (Queue 와 stack  이용했더니 렌타임 에러 뜸)
- PriorityQueue 는 최소힙 구조로 음수일 경우 -39가 먼저 나옴
- 양수을 경우 2가 먼저 나오기 때문에, 음수로 변환해서 넣어주면 -11 이 나오게됨  


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1461/Main.java)

- 입력받은 책의 위치를 오름차순으로 정렬 해 줌 :  -39  -37  -29 -28 -6  2  11

```java
Arrays.sort(arr);
```


- PriorityQueue 를 이용하여 음수, 양수를 따로 넣어줌
- 양수는 음수로 바꾸어서 넣어 주는데, 이는 나중에 peek 할 때 큰 값을 구하기 위함
- 가장 먼 거리를 구하기 위해 max를 따로 계산해 줌

```java
PriorityQueue<Integer> negative = new PriorityQueue<Integer>();
PriorityQueue<Integer> positive = new PriorityQueue<Integer>();

int max = 0;
for (int i : arr) {
    if (i > 0 ) {
        positive.add(-i);
        max = Math.max(max, i);
    }else {
        negative.add(i);
        max = Math.max(max, -i);
    }
}
```

- 각 다음 queue에 책들을 m 만큼 옮겨서 거리 계산 해줌

```java
int result  = 0;
while ( !negative.isEmpty()) {
    result += negative.peek();
    for (int i = 0; i < m; i++) {
        negative.poll();
    }
}

while( !positive.isEmpty()) {
    result += positive.peek();
    for (int i = 0; i < m; i++) {
        positive.poll();
    }
}

```


- 양수를 음스로 넣었으니 -를 붙여주고, 왕복거리이니 -2를 곱해준 다음, 가장 먼 거리는 마지막에 갔다가 돌아오지 않는걸로 해서 빼줌

```java
result = (-result * 2 ) - max;
System.out.println(result);
```

---

#### references
<https://www.acmicpc.net/problem/1461>
