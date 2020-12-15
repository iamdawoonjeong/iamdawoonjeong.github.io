---
layout: single
title: "[Problem Solving - Baekjoon] 14620 꽃길"
date: 2020-12-15 20:45:00.000000000 +09:00
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
- graph
- Brute force
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-14620/"
---
# [Baekjoon Online Judge] 14620 꽃길

## 문제
2017년 4월 5일 식목일을 맞이한 진아는 나무를 심는 대신 하이테크관 앞 화단에 꽃을 심어 등교할 때 마다 꽃길을 걷고 싶었다.

진아가 가진 꽃의 씨앗은 꽃을 심고나면 정확히 1년후에 꽃이 피므로 진아는 다음해 식목일 부터 꽃길을 걸을 수 있다.

하지만 진아에게는 꽃의 씨앗이 세개밖에 없었으므로 세 개의 꽃이 하나도 죽지 않고 1년후에 꽃잎이 만개하길 원한다.

꽃밭은 N*N의 격자 모양이고 진아는 씨앗을 (1,1)~(N,N)의 지점 중 한곳에 심을 수 있다. 꽃의 씨앗은 그림 (a)처럼 심어지며 1년 후 꽃이 피면 그림 (b)모양이 된다.



꽃을 심을 때는 주의할 점이있다. 어떤 씨앗이 꽃이 핀 뒤 다른 꽃잎(혹은 꽃술)과 닿게 될 경우 두 꽃 모두 죽어버린다. 또 화단 밖으로 꽃잎이 나가게 된다면 그 꽃은 죽어버리고 만다.



그림(c)는 세 꽃이 정상적으로 핀 모양이고 그림(d)는 두 꽃이 죽어버린 모양이다.

하이테크 앞 화단의 대여 가격은 격자의 한 점마다 다르기 때문에 진아는 서로 다른 세 씨앗을 모두 꽃이 피게하면서 가장 싼 가격에 화단을 대여하고 싶다.

단 화단을 대여할 때는 꽃잎이 핀 모양을 기준으로 대여를 해야하므로 꽃 하나당 5평의 땅을 대여해야만 한다.

돈이 많지 않은 진아를 위하여 진아가 꽃을 심기 위해 필요한 최소비용을 구해주자!

### 입력
입력의 첫째 줄에 화단의 한 변의 길이 N(6≤N≤10)이 들어온다.

이후 N개의 줄에 N개씩 화단의 지점당 가격(0≤G≤200)이 주어진다.

### 출력
꽃을 심기 위한 최소 비용을 출력한다.

### 예제

- input

```java
6
1 0 2 3 3 4
1 1 1 1 1 1
0 0 1 1 1 1
3 9 9 0 1 99
9 11 3 1 0 3
12 3 0 0 0 1
```

- output

```java
12
```

### 분류
- 그래프 이론
- 그래프 탐색
- 브루트포스 알고리즘
- 깊이 우선 탐색

## 풀이

### 문제 파악
- 한 송이 꽃을 피우는데, 5개의 칸이 필요 = 꽃심는칸 + 상 + 하 + 좌 + 우
- 3송이 15개칸이 필요
- 겹치면 안 됨
- 모든 경우의 수를 다 따져봐야하는 브루트포스, 완전 탐색 알고리즘

### 구현


[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem14620/Main.java)


- 세 군데 위치를 겹치지 않게 모두 다 탐색하기 위해서 for문 세개 사용
- 하나의 꽃씨당 n*n 개의 칸에 들어갈 수 있음

```java
int result = 4000;
//3개 위치 추출
for (int i = 0; i < n*n; i++) {
    for (int j = i+1; j < n*n; j++) {
        for (int k = j+1; k < n*n; k++) {

            ArrayList<Integer>  list = new ArrayList<Integer>();
            list.add(i);
            list.add(j);
            list.add(k);
            //(0 1 2) ~  (33 34 35) 각 수 체크
            result = Math.min(result, check(list));
        }
    }
}

```

- 세 개의 위치로 비용 계산 후 리턴
- 겹치는 경우에는 4000리턴 해줌

```java
public static int check(ArrayList<Integer> list) {
    int result = 0;

    HashSet<Integer> set = new HashSet<Integer>();

    for (Integer it : list) {
        int i = it/n;
        int j = it%n;

        //꽃씨 심는자리
        result += arr[i][j];
        set.add(it);

        //꽃씨 주변 꽃 피는 자리 (상, 하, 좌, 우)
        for (int k = 0; k < 4; k++) {
            int nextX = i + dx[k];
            int nextY = j + dy[k];

            if ( nextX < 0 || nextX >= n || nextY < 0 || nextY >= n  ) {
                return 4000;
            }
            result += arr[nextX][nextY];
            set.add(nextX * n + nextY );
        }
    }

    //겹치는 칸이 있는경우 15개가 아니게 됨으로 4000리턴
    if (set.size() != 15) {
        return 4000;
    }
    return result;
}
```

---

#### references
<https://www.acmicpc.net/problem/14620>
