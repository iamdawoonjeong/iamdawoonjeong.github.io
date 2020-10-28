---
layout: single
title: "[Problem Solving - Baekjoon] 1472 소트인사이드 "
date: 2020-10-16 23:22:00.000000000 +09:00
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
- sort
- baekjoon
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1472/"
---
# [Baekjoon Online Judge] 1472 소트인사이드


## 문제
배열을 정렬하는 것은 쉽다. 수가 주어지면, 그 수의 각 자리수를 내림차순으로 정렬해보자.

### 입력
첫째 줄에 정렬하고자하는 수 N이 주어진다. N은 1,000,000,000보다 작거나 같은 자연수이다.

### 출력
첫째 줄에 자리수를 내림차순으로 정렬한 수를 출력한다.

### 예제
- input
```
2143
```

- output
```
4321
```


## 분류
- 구현
- 정렬



## 풀이

### 문제파악
1. 내림차순 정렬을해보자
2. Bubble Sort, Arrays.sort() 사용

### 구현

#### bubblesort 구현하여 정렬

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1472/Main.java)

```java
private static int[] solution(int[] numbers) {

    boolean swaped = false;

    for (int i = 0; i < numbers.length-1; i++) {
        for (int j = 0; j < numbers.length-1-i; j++) {
            if(numbers[j] < numbers[j+1]) {
                int temp = numbers[j];
                numbers[j] = numbers[j+1];
                numbers[j+1] = temp;
                swaped=true;
            }
        }

        if(!swaped) {
            break;
        }

    }
    return numbers;

}

```

#### 내림차순 정렬 방법1

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1472/MainAPI.java)

```java
Arrays.sort(arr, new Comparator<Integer>() {

    @Override
    public int compare(Integer o1, Integer o2) {
        return Integer.compare(o2, o1);
    }

});
```

#### 내림차순 정렬 방법2

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1472/MainAPI2.java)

```java
Arrays.sort(arr, new Comparator<Integer>() {

    @Override
    public int compare(Integer o1, Integer o2) {
        return o2.compareTo(o1);
    }
});

```


### 결론
- 지난번 [2750 수 정렬하기](http://dawoonjeong.com/algorithm-problem-solving-baekjoon-10930/) 문제에서 정렬 알고리즘을 구현 하는 것보다 api사용이 빠르다는 것을 확인
- 그러나 이 문제인 경우 버블정렬을 구현했을때와 sort를 사용했을때 비슷한데 이는 문제의 조건으로 추정 됨  
- 이 문제는 N이 1억개가 주어지고, 2750 수 정렬하기 문제는 1000개 였음
- 문제의 조건에 따라 달라질 수 있으니 적절한 것을 사용


---
#### references
<https://www.acmicpc.net/problem/1472>
