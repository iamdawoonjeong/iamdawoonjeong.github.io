---
layout: single
title: "[Problem Solving - Baekjoon] 1080 행렬"
date: 2021-01-14 00:30:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-1080/"
---
# [Baekjoon Online Judge] 1080 행렬

## 문제
0과 1로만 이루어진 행렬 A와 행렬 B가 있다. 이때, 행렬 A를 행렬 B로 바꾸는데 필요한 연산의 횟수의 최솟값을 구하는 프로그램을 작성하시오.

행렬을 변환하는 연산은 어떤 3*3크기의 부분 행렬에 있는 모든 원소를 뒤집는 것이다. (0 -> 1, 1 -> 0)

### 입력
첫째 줄에 행렬의 크기 N M이 주어진다. N과 M은 50보다 작거나 같은 자연수이다. 둘째 줄부터 N개의 줄에는 행렬 A가 주어지고, 그 다음줄부터 N개의 줄에는 행렬 B가 주어진다.

### 출력
첫째 줄에 문제의 정답을 출력한다. 만약 A를 B로 바꿀 수 없다면 -1을 출력한다.

### 예제

- input

```java
3 4
0000
0010
0000
1001
1011
1001
```

- output

```java
2
```


### 예제2 (반례)

- input

```java
3 4
1110
1110
1110
0001
0001
0001
```

- output

```java
-1
```


### 분류
- greedy

## 풀이

### 문제 파악

- 행렬A

```
0000
0010
0000
```

- 행렬B

```
1001
1011
1001
```

- A[0] [0] = 0 -> B[0] [0] = 1 : 첫번째 점이 한번 뒤집혀야함 (3*3 행렬 모두)
- 행렬의 뒤집힘 과정

```
0000 -> 1110 -> 1001
0010 -> 1100 -> 1011
0000 -> 1110 -> 1001
```

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1080/Main.java)

- 같은좌표의 숫자가 다른 경우 뒤집힘 (flip)

```java
//뒤집히는 좌표가 3*3 행렬이기 때문에 n-2, m-2 만큼 돌아야함
for (int i = 0; i < n-2; i++) {
   for (int j = 0; j < m-2; j++) {
       //같은 좌표의 값이 다른경우
       if (A[i][j] != B[i][j]) {
           //뒤집기
           flip(i,j,A);
           result += 1;//flip한 횟수

       }
   }
}
```

- 뒤집힌 행렬을 기준으로 다음 좌표(3*3만큼)도 확인

```java
private static void flip(int i, int j, int[][] A) {

     //현좌표에서 3*3까지만 뒤집어주기
     for (int x = 0; x < 3; x++) {
         for (int y = 0; y < 3; y++) {
             A[i+x][j+y] ^=1;  //XOR 1이 홀수개 1, 1이 짝수개  0
         }
     }
 }
```

- (0,0) 좌표 같은지 확인 후 결과 출력 

```java
for (int i = 0; i < n; i++) {
   for (int j = 0; j < m; j++) {
        if (A[i][j] != B[i][j]) {
            result = -1;
            break;
        }
    }
}

System.out.println(result);
```

---

#### references
<https://www.acmicpc.net/problem/1080>
