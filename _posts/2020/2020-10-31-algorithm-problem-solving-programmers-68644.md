---
layout: single
title: "[Problem Solving - Programmers] 68644 두 개 뽑아서 더하기"
date: 2020-10-31 23:40:00.000000000 +09:00
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
- programmers
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-programmers-68644/"
---
# [Programmers]  68644 두 개 뽑아서 더하기

## 문제
정수 배열 numbers가 주어집니다. numbers에서 서로 다른 인덱스에 있는 두 개의 수를 뽑아 더해서 만들 수 있는 모든 수를 배열에 오름차순으로 담아 return 하도록 solution 함수를 완성해주세요.

### 입력
numbers의 길이는 2 이상 100 이하입니다.
numbers의 모든 수는 0 이상 100 이하입니다.


### 예제

| numbers | result |
|:--------|:--------|
| [2,1,3,4,1] | [2,3,4,5,6,7] |
| [5,0,2,7] | [2,5,7,9,12] |


## 풀이

### 문제 파악
- 주어진 배열내 겹치지 않는 인덱스 위치의 두수를 더한 값들을 오름차순으로 나열

```
2 = 1 + 1 입니다. (1이 numbers에 두 개 있습니다.)
3 = 2 + 1 입니다.
4 = 1 + 3 입니다.
5 = 1 + 4 = 2 + 3 입니다.
6 = 2 + 4 입니다.
7 = 3 + 4 입니다.
따라서 [2,3,4,5,6,7] 을 return 해야 합니다.
```

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/programmers/lessons68644/Solution.java)

- 겹치지 않는 두수를 선택해서 더해서 넣어줌

```java
HashSet<Integer> set = new HashSet<Integer>();  
for (int i = 0; i < numbers.length; i++) {
    for (int j = i+1; j < numbers.length; j++){
        if ( i < j) {
            int sum = numbers[i] + numbers[j];
            set.add(sum);
        }
    }
}
```

- 결과값에 넣어줌

```java
answer = new int[set.size()];
int index=0;
for (Integer num : set) {
    answer[index] = num;
    index++;
}
```

- 오름차순으로 나열해서 출력

```java
Arrays.sort(answer);
```


---

#### references
<https://programmers.co.kr/learn/courses/30/lessons/68644?language=java>
