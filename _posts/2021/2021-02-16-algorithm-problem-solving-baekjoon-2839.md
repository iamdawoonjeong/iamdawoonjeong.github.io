---
layout: single
title: "[Problem Solving - Baekjoon] 2839 설탕 배달"
date: 2021-02-16 18:10:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-2839/"
---
# [Baekjoon Online Judge] 2839 설탕 배달

## 문제
[문제 보기](https://www.acmicpc.net/problem/2839){: target="_blank"}

## 풀이

### 문제 파악
- 설탕은 5kg, 3kg 중 5kg의 갯수를 최대치로 설정 한 후 나머지를 3kg 으로 옮겨야 최소 갯수가 될 수 있음
- 입력된 설탕의 무게(n)에 5kg 최대 갯수를 구하고  + 남은 무게를 3kg로 옮기고 나서도 남은 무게 가 있다면, 5kg 의 갯수를 줄여가면서 계산   

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2839/Main.java){: target="_blank"}

```java
int max = n/5; // 5키로 최대 갯수
int count = 0 ;
int remain = n;

while( max >= 0 ) {
    count = 0;   //변수초기화
    remain = n;

    if (max > 0 ) {
        count = max ;
        remain = remain  - (max*5);
    }

    if (remain%3 ==0) {
        count = count + (remain/3);
        remain = (remain%3);
    }

    if (remain==0) {
       //남은 무게가 없으면 끝내기
        break;
    }else {
        //5kg의 갯수를 줄여서 다시 연산
        // max = -1 이 되면 종료
        max--;
    }
}

if (remain != 0 ) {
    System.out.println(-1);
}else {
    System.out.println(count);
}
```

---

#### references
<https://www.acmicpc.net/problem/2839>{: target="_blank"}
