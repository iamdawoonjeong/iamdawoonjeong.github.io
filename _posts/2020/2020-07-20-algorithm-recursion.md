---
layout: single
title: "[Algorithm] 순환적 호출 / 재귀 호출 알고리즘 (Recursion / Recursive Call)"
date: 2020-07-20 18:27:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Algorithm
tags:
- data structure
- algorithm
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-recursion/"
---
# 순환적 호출 / 재귀 호출 알고리즘 (Recursion / Recursive Call) Algorithm


## 비순환적 알고리즘 indirect recursion

### 자바로 구현한 indirect recursion  -  for을 이용한 1~n까지의 합 구하기


```java
public static int functionFor(int n) {
    int sum = 0;

    //1~n 까지의 합
    // for (int i = 1; i <= n; i++) {

    //n~1 까지의 합
    for (int i = n ;  i > 0 ; i--) {
        sum = sum + i;
        System.out.print(sum + " ");
    }
    return sum;
}
```


## 순환알고리즘 Direct Recursion
- 자기 자신을 호출


### 장점
- 알고리즘 작성이 간결해 짐

### 단점
- 비순환적 알고리즘 보다 가억장소 많은 사용 (Stack 사용)
- 과다한 함수가 호출되는 경우 실행시간의 효율이 떨어짐


![algorithm-PK6Ht]({{ site.baseurl }}/assets/images/posts/2020/algorithm-PK6Ht.png)


### 자바로 구현한 direct recursion  -  recursion을 이용한 1~n까지의 합 구하기


```java
public static int functionRecursion(int n) {
    if(n==0) {
        return n;
    }else {
        System.out.print(n + " ");
        return n + functionRecursion(n-1);
    }
}
```


### Complexity
- 시간 복잡도, 공간복잡도 O(n)


## 순환적, 비순환적 알고리즘 예제

[Sum : 1 ~ n 까지의 합 구하기 (Recrusion, for)](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-theory/src/recursion/Sum.java)

[Factorial : n! 구하기 (Recrusion, for)](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-theory/src/recursion/Factorial.java)

[Fibonacci 구하기 (Recrusion, for)](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-theory/src/recursion/Fibonacci.java)

[GCD(최대공약수)구하기 (Recursion, for)](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-theory/src/recursion/GCD.java)


---
##### References
<https://ko.wikipedia.org/wiki/%EC%9E%AC%EA%B7%80_(%EC%BB%B4%ED%93%A8%ED%84%B0_%EA%B3%BC%ED%95%99)>  
<https://stackoverflow.com/questions/19865503/can-recursion-be-named-as-a-simple-function-call>  
도서: C언어로 구현한 자료구조 (정일출판사 /임형근 저)
