---
layout: single
title: "[Problem Solving - Baekjoon] 12865 평범한 배낭"
date: 2020-11-06 22:33:00.000000000 +09:00
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
- DP
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-12865/"
---
# [Baekjoon Online Judge] 12865 평범한 배낭

## 문제
이 문제는 아주 평범한 배낭에 관한 문제이다.

한 달 후면 국가의 부름을 받게 되는 준서는 여행을 가려고 한다. 세상과의 단절을 슬퍼하며 최대한 즐기기 위한 여행이기 때문에, 가지고 다닐 배낭 또한 최대한 가치 있게 싸려고 한다.

준서가 여행에 필요하다고 생각하는 N개의 물건이 있다. 각 물건은 무게 W와 가치 V를 가지는데, 해당 물건을 배낭에 넣어서 가면 준서가 V만큼 즐길 수 있다. 아직 행군을 해본 적이 없는 준서는 최대 K무게까지의 배낭만 들고 다닐 수 있다. 준서가 최대한 즐거운 여행을 하기 위해 배낭에 넣을 수 있는 물건들의 가치의 최댓값을 알려주자.

### 입력
첫 줄에 물품의 수 N(1 ≤ N ≤ 100)과 준서가 버틸 수 있는 무게 K(1 ≤ K ≤ 100,000)가 주어진다. 두 번째 줄부터 N개의 줄에 거쳐 각 물건의 무게 W(1 ≤ W ≤ 100,000)와 해당 물건의 가치 V(0 ≤ V ≤ 1,000)가 주어진다.

입력으로 주어지는 모든 수는 정수이다.

### 출력
줄에 배낭에 넣을 수 있는 물건들의 가치합의 최댓값을 출력한다.

### 예제

- input

```java
4 7
6 13
4 8
3 6
5 12
```

- output

```java
14
```

### 분류

- 동적프로그래밍


## 풀이

### 문제 파악

- 이전에 구했던 물건의 가치를 알아야 다음 단계의 가치도 구할 수 있는 동적 프로그래밍
- 동적프로그래밍으로 생각하는 것 자체가 쉽지 않았던 문제이나 기초라고 하니 반드시 알아두어야 할 문제
- 많이 나오는 문제라고함

| w | v |
|:----:|:----:|
| 6 | 13 |
| 4 |  8 |
| 3 |  6 |
| 5 | 12 |


|   |  0 |  1 |  2 |  3 |  4 |  5 |  6 |  7 |
|:----:|:----:|:----:|:-----:|:-----:|:-----:|:-----:|:-----:|
| 0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |
| 6 |  0 |  0 |  0 |  0 |  0 |  0 | 13 | 13 |
| 4 |  0 |  0 |  0 |  0 |  8 |  8 | 13 | 13 |
| 3 |  0 |  0 |  0 |  6 |  8 |  8 | 13 | **14** |
| 5 |  0 |  0 |  0 |  6 |  8 | 12 | 13 | 14 |

- k > weight[j] : 이전 물건의 가치가 채워짐 (dp[j-1])
- k = weight[j] : 현재 물건의 가치가 채워짐(value[j])
- k > weight[j] : 이전 물건의 가치 (dp[j-1]) VS 배낭무게에서 현재 물건의 무게를 뺀 남은 무게의 물건의 가치 (dp[i-weight[j]] [j-1]) + 현재 물건의 가치(value[j]) > 중에서 더 큰값
- 결국 dp[k] [n]이 제일 큰 값이 됨


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem12865/Main.java)


```java
//배낭무게 1 ~ k 까지 하나씩 채움
for (int i = 1; i <= k; i++) {
    //물건 무게 1 ~  n까지 하나씩 채움
    for (int j = 1; j <= n; j++) {
        // 물건무게가 배낭무게보다 적어 담을 수 있는 경우
        if (weight[j] <= i) {
            // 위에있던 값, 이전에 구했던 값을 비교해서 큰 거 넣기
            // dp[i-weight[j]][j-1] = [배낭무게 - 물건무게][이전물건무게의 최대가치] + 현 물건의 가치
            dp[i][j] = Math.max(dp[i][j-1], dp[i-weight[j]][j-1] + value[j]);
        }else {
            //물거의 무게가 배낭무게보다 커서 담을 수 없는 경우
            //같은 배낭 무게에서 내려옴
            dp[i][j] = dp[i][j-1];
        }

    }
}     
```

---

#### references
<https://www.acmicpc.net/problem/12865>
