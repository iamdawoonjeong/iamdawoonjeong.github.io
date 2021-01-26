---
layout: single
title: "[Problem Solving - Baekjoon] 16769 Mixing Milk"
date: 2020-12-02 22:40:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-16769/"
---
# [Baekjoon Online Judge] 16769 Mixing Milk

## 문제
Farming is competitive business -- particularly milk production. Farmer John figures that if he doesn't innovate in his milk production methods, his dairy business could get creamed!

Fortunately, Farmer John has a good idea. His three prize dairy cows Bessie, Elsie, and Mildred each produce milk with a slightly different taste, and he plans to mix these together to get the perfect blend of flavors.

To mix the three different milks, he takes three buckets containing milk from the three cows. The buckets may have different sizes, and may not be completely full. He then pours bucket 1 into bucket 2, then bucket 2 into bucket 3, then bucket 3 into bucket 1, then bucket 1 into bucket 2, and so on in a cyclic fashion, for a total of 100 pour operations (so the 100th pour would be from bucket 1 into bucket 2). When Farmer John pours from bucket  into bucket , he pours as much milk as possible until either bucket  becomes empty or bucket  becomes full.

Please tell Farmer John how much milk will be in each bucket after he finishes all 100 pours.

### 입력
The first line of the input file contains two space-separated integers: the capacity  of the first bucket, and the amount of milk  in the first bucket. Both  and  are positive and at most 1 billion, with . The second and third lines are similar, containing capacities and milk amounts for the second and third buckets.

### 출력
Please print three lines of output, giving the final amount of milk in each bucket, after 100 pour operations.

### 예제
- input

```java
10 3
11 4
12 5
```

- output

```java
0
10
2
```

### 분류
- 구현

## 풀이

### 문제 파악
- 컵에 용량제한이 있고cup, 각컵에 우유가 담겨있음 milk
- 다음 컵에 가득찰때까지 우유를 따라줌
- 이와 같은 행동을 100번했을 때의 각 컵에 담긴 우유의 양을 구하는 프로그램

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem16769/Main.java)


- 따라주고나면 현재우유양 milk[index], 다음우유 milk[next]를 한 반복문에서 구해주기
- index = i%3;
- next = (i+1)%3
- 인덱스 위치를 잘 계산해줌
- 삼항연산식으로 계산하여 풀이했으나, max,min 으로 구하기도 함

```java
int index = 0 ;
int next = 0 ;

for (int i = 0; i < 100; i++) {

    index = i % 3 ;
    next = (i+1) % 3;

    // 현재 우유양 = 다음컵에 다부어주는 경우와
    // 다음컵용량 남은것 만큼 부어주는 경우 (다음컵용량-다음컵우유양 =다음컵 담을수 있는양)
    int temp = ( cup[next] - milk[next] >= milk[index] ? 0 : milk[index] - (cup[next] - milk[next]));
    //int temp  = Math.max(0,  milk[index] - (cup[next]-milk[next]));

    // 다음우유양 = 현재우유+다음우유
    // 현재우유+다음우유양이 다음컵용량보다 큰 경우에는 컵 용량까지만 가능  
    milk[next] = ( cup[next] > milk[index] + milk[next] ? milk[index] + milk[next]: cup[next]);
    //milk[next] = Math.min(cup[next],  milk[next]+ milk[index]);

    // 다음 컵연산에서 현재우유를 사용하기에 temp에 담아주었다가 대입
    milk[index] = temp;

}

```

---

#### references
<https://www.acmicpc.net/problem/16769>
