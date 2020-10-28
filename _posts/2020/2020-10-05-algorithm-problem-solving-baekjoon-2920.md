---
layout: single
title: "[Problem Solving - Baekjoon] 2920 음계"
date: 2020-10-05 22:36:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-2920/"
---
# [Baekjoon Online Judge] 2920 음계


### 시작하기 전 백준 문제 푸는 방법
- 클래스 명은 반드시 Main 으로 해야 함 (컴파일 에러뜸..나..)
- import도 다 명시해주어야 함
- 출력은 반드시 문제에 나온 것처럼 그대로 나와야함. 다른것 나오면 에러임 (이쁘게 출력하고픈 마음 알겠으나 쓸데없는 출력은 자제)
- 컴파일에러, 런타임에러, 시간초과 등의 갖가지 사유로 문제를 풀지 못 했을 경우는 코드 검토 후 수정을 강력히 권고 (대부분 내 잘못이지 채점 서버 잘못아님)


## 문제
다장조는 c d e f g a b C, 총 8개 음으로 이루어져있다. 이 문제에서 8개 음은 다음과 같이 숫자로 바꾸어 표현한다. c는 1로, d는 2로, ..., C를 8로 바꾼다.

<span style="color:red">1부터 8까지 차례대로 연주한다면 ascending, 8부터 1까지 차례대로 연주한다면 descending, 둘 다 아니라면 mixed 이다.</span>

연주한 순서가 주어졌을 때, 이것이 ascending인지, descending인지, 아니면 mixed인지 판별하는 프로그램을 작성하시오.


### 입력
첫째 줄에 8개 숫자가 주어진다. 이 숫자는 문제 설명에서 설명한 음이며, 1부터 8까지 숫자가 한 번씩 등장한다.


### 출력
첫째 줄에 ascending, descending, mixed 중 하나를 출력한다.


### 예제 1
- input
```
1 2 3 4 5 6 7 8
```

- output
```
ascending
```


### 예제2
- input
```
8 7 6 5 4 3 2 1
```

- output
```
descending
```

### 예제3
- input
```
8 1 7 2 6 3 5 4
```

- output
```
mixed
```


## 풀이


### 문제 파악
1. 8개의 숫자가 한 번씩 등장하는 한 줄이 입력
2. **입력된 숫자의 순서가 ascending인지 descending인지 mixed인지를 판단**
3. 판단 결과 출력


### 연산
1. 한 줄 입력 받기
2. 8개의 숫자 array로 변경
3. **i 와 i+1 번째 숫자를 비교해서 ascending인지 descending인지 mixed인지 판단**
4. 결과 출력


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2920/Main.java)

1. system.in 표준 입력을 통해 숫자를 입력 받은 수를 정규식으로 구분하기 위해 scanner로 받음
```java
Scanner sc = new Scanner(System.in);
```

2. 입력받은 문자를 array로 변경
```java
String[] arr = sc.nextLine().split(" ");
```

3. for문으로 array내 element i와 i-1번째 크기를 비교해서 판단
```java
for (int i = 1; i < arr.length; i++) {
    if (Integer.parseInt(arr[i]) > Integer.parseInt(arr[i-1])) {
        ascending = true;
    }else if (Integer.parseInt(arr[i]) < Integer.parseInt(arr[i-1])) {
        descending = true;
    }
}
```

4. 애초에 아래와 같이 입력받은 배열을 int로 한 번 변환했다면, 바로 위와 같이 반복문내 Intger.parseInt를 매번 실행하지 않아도 될 문제
5. 그러나 숫자가 8개 밖에 없으니.. 그냥 진행해서 풀었음
```java
int[] input = new int[arr.length];
for (int i = 0; i < arr.length; i++) {
    input[i] = Integer.parseInt(arr[i]);
}
```

6. 결과 판단은 boolean으로 해 줌


```java
boolean ascending = false;
boolean descending = false;

if (ascending && descending) {
    System.out.println("mixed");
} else if (ascending){
    System.out.println("ascending");
}else if (descending) {
    System.out.println("descending");
}
```    


---

#### references
<https://www.acmicpc.net/problem/2920>
