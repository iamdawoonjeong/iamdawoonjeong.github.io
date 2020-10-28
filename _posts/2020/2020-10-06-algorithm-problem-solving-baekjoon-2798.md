---
layout: single
title: "[Problem Solving - Baekjoon] 2798 블랙잭"
date: 2020-10-06 22:40:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-2798/"
---
# [Baekjoon Online Judge] 2798 블랙잭

## 문제
카지노에서 제일 인기 있는 게임 블랙잭의 규칙은 상당히 쉽다. 카드의 합이 21을 넘지 않는 한도 내에서, 카드의 합을 최대한 크게 만드는 게임이다. 블랙잭은 카지노마다 다양한 규정이 있다.

한국 최고의 블랙잭 고수 김정인은 새로운 블랙잭 규칙을 만들어 상근, 창영이와 게임하려고 한다.

김정인 버전의 블랙잭에서 각 카드에는 양의 정수가 쓰여 있다. 그 다음, 딜러는 N장의 카드를 모두 숫자가 보이도록 바닥에 놓는다. 그런 후에 딜러는 숫자 M을 크게 외친다.

이제 플레이어는 제한된 시간 안에 N장의 카드 중에서 3장의 카드를 골라야 한다. 블랙잭 변형 게임이기 때문에, 플레이어가 고른 카드의 합은 M을 넘지 않으면서 M과 최대한 가깝게 만들어야 한다.

N장의 카드에 써져 있는 숫자가 주어졌을 때, M을 넘지 않으면서 M에 최대한 가까운 카드 3장의 합을 구해 출력하시오.


### 입력
첫째 줄에 카드의 개수 N(3 ≤ N ≤ 100)과 M(10 ≤ M ≤ 300,000)이 주어진다. 둘째 줄에는 카드에 쓰여 있는 수가 주어지며, 이 값은 100,000을 넘지 않는다.

합이 M을 넘지 않는 카드 3장을 찾을 수 있는 경우만 입력으로 주어진다.


### 출력
첫째 줄에 M을 넘지 않으면서 M에 최대한 가까운 카드 3장의 합을 출력한다.



### 예제 1
- input
```
5 21
5 6 7 8 9
```

- output
```
21
```


### 예제2
- input
```
10 500
93 181 245 214 315 36 185 138 216 295
```

- output
```
497
```


### 분류
브루트포스(Brute-force) 알고리즘 : 모든 가능성을 시도하는 간단한 방법



## 풀이

### 문제 파악
1. 예제1 : 첫째 줄에 N개의 카드 숫자를 입력받아 최대 합 M을 넘지 않는 조합을 두번 째 줄에서 3개의 조합으로 만들기
```
5 21 //입력되는 카드 숫자의 갯수 N, 카드 3개의 최대 합 M
5 6 7 8 9 // N개의 카드
```
2. 두번째 줄의 카드를 **모든 경우의 수로 조합**해서 최대 합에 가장 가까운 or 최대합의 수를 만들어주는 조합 찾기  


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2798/Main.java)


1. system.in 표준 입력을 통해 숫자를 입력 받은 수를 정규식으로 구분하기 위해 scanner로 받음
```java
Scanner sc = new Scanner(System.in);
```

2. 첫번째 라인 카드의 갯수와 카드 3개의 합 받기
```java
String[] str = sc1.split(" ");
int N = Integer.parseInt(str[0]); //카드의 갯수
int M = Integer.parseInt(str[1]); //카드 3개의 합
```

3. 두번째 라인은 카드의 갯수 N개 만큼  카드의 숫자들을 받기
```java
for (int i = 0; i < N; i++) {
    numbers[i] = Integer.parseInt(str2[i]);
}
```

4. 3개의 카드 숫자가 중복 되지 않고, 합이 M보다 작아야하며 최대합을 찾아주는 로직
```java
for (int i = 0; i < N; i++) {
    for (int j = 0; j < N; j++) {
        for (int k = 0; k < N; k++) {

            //카드의 숫자가 중복 되지 않고
            if ((numbers[i] != numbers[j]) && (numbers[j] != numbers[k]) && (numbers[i] != numbers[k])) {
                sum  = numbers[i] + numbers[j] + numbers[k] ;

                //세 카드 숫자의 합이 M보다 작아야 하며
                if (sum <= M ) {

					//최대 합을 찾기
                    if(sum >= maxSum) {
                        maxSum = sum;
                    }
                }
            }
        }
    }
}
```    


---
#### references

<https://www.acmicpc.net/problem/2798>  
<https://en.wikipedia.org/wiki/Brute-force_search>  
<https://www.freecodecamp.org/news/brute-force-algorithms-explained/>  
