---
layout: single
title: "[Problem Solving - Baekjoon] 7490 0 만들기"
date: 2020-10-27 23:00:00.000000000 +09:00
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
- recursive
- recursion
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-7490/"
---
# [Baekjoon Online Judge] 7490 0 만들기

## 문제
1부터 N까지의 수를 오름차순으로 쓴 수열 1 2 3 ... N을 생각하자.

그리고 '+'나 '-', 또는 ' '(공백)을 숫자 사이에 삽입하자(+는 더하기, -는 빼기, 공백은 숫자를 이어 붙이는 것을 뜻한다). 이렇게 만든 수식의 값을 계산하고 그 결과가 0이 될 수 있는지를 살피자.

N이 주어졌을 때 수식의 결과가 0이 되는 모든 수식을 찾는 프로그램을 작성하라.

### 입력
첫 번째 줄에 테스트 케이스의 개수가 주어진다(<10).

각 테스트 케이스엔 자연수 N이 주어진다(3 <= N <= 9).

### 출력
각 테스트 케이스에 대해 ASCII 순서에 따라 결과가 0이 되는 모든 수식을 출력한다. 각 테스트 케이스의 결과는 한 줄을 띄워 구분한다.

### 예제
- input

```java
2
3
7
```
- output

```java
1+2-3

1+2-3+4-5-6+7
1+2-3-4+5+6-7
1-2 3+4+5+6+7
1-2 3-4 5+6 7
1-2+3+4-5+6-7
1-2-3-4-5+6+7
```

## 풀이

### 문제 파악
- 모든 연산자에 대한 경우의 수를 구해야하는 **완전탐색문제**
- 모든 연산자 리스트의 경우의 수가 대략 3<sup>8</sup> =  6561 으로 완전탐색하는데 충분할 것으로 예상


```java
2   // testCase : 테스트 케이스 갯수
3   // n : 1~3까지의 오름차순 순
7   // n : 1~7까지의 오름차순 순
```

- 1부터 n까지의 오름차순을 +, -, 스페이스 공백(앞뒤 숫자가 연결된 숫자) 연산을 넣어 계산한 결과 0이 되는 경우를 출력
- 문제 파악하는것은 어렵지 않아으나 구현하는 부분에서 상당히 난이도를 느꼈음
- python은 eval 함수를 사용하면 string으로 되어있는 산술식 연산된다고 함
- java에서는 stringbuilder 타입으로 산술식을 만들고 -> 공백없애고 -> 연산자 피연산자를 나누어서 -> 계산시 하나씩 꺼내오는 형태로 구현

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem7490/Main.java)

- 연산자 경우의 수를 구하는 재귀함수 호출 부분
- arraylist 의 arraylist를 구현하여 연산자 list를 생성해줌   

```java
static ArrayList<ArrayList<Character>> operator;

public static void recursive(ArrayList<Character> list, int n) {

    if(list.size() == n ) {
        operator.add((ArrayList<Character>) list.clone());
        return;
    }

    list.add(' ');
    recursive(list, n);
    list.remove(list.size()-1);

    list.add('+');
    recursive(list, n);
    list.remove(list.size()-1);

    list.add('-');
    recursive(list, n);
    list.remove(list.size()-1);

}
```


- StringBuilder를 출력용으로 피연산자와 연산자를 붙여서 식 만들기
- 피연산자 숫자가 한개 더 많으므로 한번 더 붙임

```java
for (ArrayList<Character> op : operator) {
    sb = new StringBuilder();
    int num;
    for (num = 0; num < n-1; num++) {
        sb.append(num+1).append(op.get(num));
    }
    sb.append(num+1);

    String calc = sb.toString();
    calc  = calc.replaceAll(" ", "");

    if (calculation(calc) == 0) {
        System.out.println(sb);
    }
}
```

- StringBuilder로 만든 출력용 연산을 이용하여 계산
- 연산자를 제외한 피연산자들을 String 배열로 넣음
- 연산자들을 순서대로 연산자 리스트 ArrayList 에 넣어줌
- 피연산자와 연산자들을 조합해서 계산후 0일 경우 출력

```java
public static int calculation(String str) {

    //operator 제외하고 숫자만 배열로 넣음
    String[] num = str.split("[+\\-]");

    ArrayList<Character> opList = new ArrayList<>();


    for (Character ch : str.toCharArray()) {
        if ('+' == ch || '-' == ch) {
            opList.add(ch);
        }
    }

    int cal = Integer.parseInt(num[0]);
    for (int i = 1; i < num.length; i++) {
        if ( opList.get(i-1).equals('+') ) {
            cal+= Integer.parseInt(num[i]);
        }
        if ( opList.get(i-1).equals('-') ) {
            cal-= Integer.parseInt(num[i]);
        }
    }

    return cal;
}
```

- 재귀함수 불러지는 순서

![problem-solving-7490-01]({{ site.baseurl }}/assets/images/posts/2020/problem-solving-7490-01.png)


![problem-solving-7490-02]({{ site.baseurl }}/assets/images/posts/2020/problem-solving-7490-02.png)


---

#### references
<https://www.acmicpc.net/problem/7490>
<https://velog.io/@dnstlr2933/%EC%9E%AC%EA%B7%80%ED%95%A8%EC%88%98>
