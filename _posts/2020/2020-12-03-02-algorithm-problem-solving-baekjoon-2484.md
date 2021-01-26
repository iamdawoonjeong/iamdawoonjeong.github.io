---
layout: single
title: "[Problem Solving - Baekjoon] 2484 주사위 네개"
date: 2020-12-03 23:30:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-2484/"
---
# [Baekjoon Online Judge] 2484 주사위 네개

## 문제
1에서부터 6까지의 눈을 가진 4개의 주사위를 던져서 다음과 같은 규칙에 따라 상금을 받는 게임이 있다.

1. 같은 눈이 4개가 나오면 50,000원+(같은 눈)*5,000원의 상금을 받게 된다.
2. 같은 눈이 3개만 나오면 10,000원+(3개가 나온 눈)*1,000원의 상금을 받게 된다.
3. 같은 눈이 2개씩 두 쌍이 나오는 경우에는 2,000원+(2개가 나온 눈)*500원+(또 다른 2개가 나온 눈)*500원의 상금을 받게 된다.
4. 같은 눈이 2개만 나오는 경우에는 1,000원+(같은 눈)*100원의 상금을 받게 된다.
5. 모두 다른 눈이 나오는 경우에는 (그 중 가장 큰 눈)*100원의 상금을 받게 된다.

예를 들어, 4개의 눈이 3, 3, 3, 3으로 주어지면 50,000+3*5,000으로 계산되어 65,000원의 상금을 받게 된다. 4개의 눈이 3, 3, 6, 3으로 주어지면 상금은 10,000+3*1,000으로 계산되어 13,000원을 받게 된다. 또 4개의 눈이 2, 2, 6, 6으로 주어지면 2,000+2*500+6*500으로 계산되어 6,000원을 받게 된다. 4개의 눈이 6, 2, 1, 6으로 주어지면 1,000+6*100으로 계산되어 1,600원을 받게 된다. 4개의 눈이 6, 2, 1, 5로 주어지면 그 중 가장 큰 값이 6이므로 6*100으로 계산되어 600원을 상금으로 받게 된다.

N(1≤N≤1,000)명이 주사위 게임에 참여하였을 때, 가장 많은 상금을 받은 사람의 상금을 출력하는 프로그램을 작성하시오.

### 입력
첫째 줄에는 참여하는 사람 수 N이 주어지고 그 다음 줄부터 N개의 줄에 사람들이 주사위를 던진 4개의 눈이 빈칸을 사이에 두고 각각 주어진다.

### 출력
첫째 줄에 가장 많은 상금을 받은 사람의 상금을 출력한다.

### 예제
- input

```java
4
3 3 3 3
3 3 6 3
2 2 6 6
6 2 1 5
```

- output

```java
65000
```

### 분류
- 구현

## 풀이

### 문제 파악
- [주사의 세개](http://dawoonjeong.com/algorithm-problem-solving-baekjoon-2480/)의 문제와 비슷하나 조건이 많아짐
- 같은 방식에서 몇가지 조건만 더 추가


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2484/Main.java)

- 같은 눈이 2번 나왔을때, 1번 나왔을때의 조건을 잘 따져야함
- 배열과 if문으로 제어하려다보니 변수를 많이 쓴 느낌이 듦(개선할 수 있음 해봄이 좋을 듯)

```java
for (int i = 0; i < n; i++) {
    st = new StringTokenizer(br.readLine()); //주사위를 던진 4개의 숫자 받기

    int[] arr = new int[7];
    ArrayList<Integer> list = new ArrayList<Integer>();


    Arrays.fill(arr, 0);
    for (int j = 0; j < 4; j++) {
        arr[Integer.parseInt(st.nextToken())] += 1 ;
    }

    int reward = 0;
    int max = 0;
    int dup = 0;
    int temp = 0;

    for (int j = 1; j < 7; j++) {

        //나온적 없는 수는 continue로 넘김
        if ( arr[j] == 0){
            continue;
        }

        //같은 눈이 4개가 나오면 50,000원+(같은 눈)*5,000원의 상금
        if ( arr[j] == 4 ) {
            reward = 50000 + (j*5000);
            break;

        }else if ( arr[j] == 3 ){
            //10,000원+(3개가 나온 눈)*1,000원의 상금
            reward = 10000 + (j*1000);
            break;

        }else if (arr[j]  == 2) {

            //1,000원+(같은 눈)*100원의 상금
            reward = 1000 + (j*100);

            dup++;
            if (dup == 1) {
                temp = j;
            }

            if (dup == 2 ) {
                //같은 눈이 2개씩 두 쌍이 나오는 경우에는 2,000원+(2개가 나온 눈)*500원+(또 다른 2개가 나온 눈)*500원의 상금을 받게 됨
                reward = 2000 + (temp*500) + (j*500);
                break;
            }

        }else if (arr[j] == 1) {

            if (dup == 0 ) {
                max = Math.max(max, j);
                // (그 중 가장 큰 눈)*100원
                reward = max * 100;
            }

        }
    }
    result[i] = reward;
}


Arrays.sort(result);
System.out.println(result[n-1]);
```

---

#### references
<https://www.acmicpc.net/problem/2484>
