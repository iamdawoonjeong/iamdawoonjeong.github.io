---
layout: single
title: "[Problem Solving - Baekjoon] 9037 The candy war"
date: 2020-12-02 22:30:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-9037/"
---
# [Baekjoon Online Judge] 9037 The candy war

## 문제
알고리즘 유치원 선생님인 영희는 간식시간이 되자 아이들에게 사탕을 나누어 주려고 하였다. 하지만 욕심 많고 제멋대로인 유치원 아이들은 차례대로 받으라는 선생님의 말을 무시한 채 마구잡이로 사탕을 집어 갔고 많은 사탕을 집어 간 아이가 있는가 하면 사탕을 거의 차지하지 못하고 우는 아이도 있었다.

말로 타일러도 아이들이 말을 듣지 않자 영희는 한 가지 놀이를 제안했다. 일단 모든 아이들이 원으로 둘러 앉는다. 그리고 모든 아이들은 동시에 자기가 가지고 있는 사탕의 절반을 오른쪽 아이에게 준다. 만약 이 결과 홀수개의 사탕을 가지게 된 아이가 있을 경우 선생님이 한 개를 보충해 짝수로 만들어 주기로 했다. 흥미로워 보이는 이 놀이에 아이들은 참여 했고 이 과정을 몇 번 거치자 자연스럽게 모든 아이들이 같은 수의 사탕을 가지게 되어 소란은 종료되었다.

자기가 가진 사탕의 반을 옆에 오른쪽에 앉은 아이에게 주는 과정과 선생님이 사탕을 보충해 주는 과정을 묶어서 1 순환이라고 할 때 몇 번의 순환을 거치면 모든 아이들이 같은 수의 사탕을 가지게 되는지 계산 해보자. 단, 처음부터 홀수개의 사탕을 가지고 있으면 선생님이 짝수로 보충을 먼저 해주며 이 경우 순환수에 들어가지 않는다. 선생님은 충분한 수의 사탕을 갖고 있다고 가정하자.

### 입력
입력은 표준입력(standard input)을 통해 받아들인다. 입력의 첫 줄에는 테스트 케이스의 개수 T가 주어진다. 각각의 테스트 케이스의 첫 줄에는 아이의 인원 N (1 ≤ N ≤ 10)이 주어지고 그 다음 줄에는 각 아이들이 초기에 가지고 있는 사탕의 개수 Ci ( 1 ≤ i ≤ N, 1 ≤ Ci ≤ 30)가 주어진다. 분배 시 C1의 오른쪽에는 C2가, C2의 오른쪽에는 C3가…… 같은 식으로 앉게 되며 CN의 오른쪽에는 C1이 앉게 된다.

### 출력
출력은 표준출력(standard output)을 통하여 출력한다. 각 테스트 케이스에 대하여 모든 아이가 같은 개수의 사탕을 가질 때까지 몇 순환이 걸리는지 출력하시오.

### 예제

- input

```java
4
5
2 4 7 8 9
1
9
6
10 5 13 2 7 8
4
3 4 4 3
```

- output

```java
6
0
4
0
```

### 분류
- 구현

## 풀이

### 문제 파악

- 사탕의 갯수가 주어지고 홀수인 경우 한개씩 받아서 짝수로 시작
- 모든 아이들이 가진 사탕의 갯수가 같아야 함
- 내가 가진 사탕의 반을 옆사람에게 주고, 한번 다 돌고나면, 홀수개가 된 경우 한 개 증가시켜서 갯수 똑같은지 확인 반복  

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem9037/Main.java)

- 맨처음부터 사탕갯수 체크하고 시작

```java
public static void solution(int n, int[] candy) {

    int count = 0;

    //배열내 수가 같아질때까지 while문 반복
    while (!check(n, candy)){
        circulation(n, candy);
        count++;
    }
    System.out.println(count);
}
```

- 사탕 갯수 체크
- 홀수 일때 한개씩 증가 시키고 모두 같은수 인지는 set 을 활용하여 체크

```java
public static boolean check(int n, int[] candy) {

    //중복허용하지 않는 set에 담아서 길이체크
    HashSet<Integer> set = new HashSet<>();

    for (int i = 0; i < n; i++) {
        if (candy[i]%2 == 1) {
            candy[i]++;
        }
        set.add(candy[i]);
    }

    //길이가 1이면 모두 같은 수임
    return set.size() == 1 ? true : false;
}
```

- 순환 : 내가 받을 캔디의 수량을 따로 계산해서 더해주는 방법으로 진행

```java
public static void circulation(int n, int[] candy) {

    // 오른쪽사람에게 더 해질 사탕 갯수 따로 관리
    int[]  arr = new int[n];

    for (int i = 0; i < n; i++) {

        //홀수개 인 경우  
        if (candy[i] % 2 == 1) {
            // 한개추가
            candy[i]++;
        }

        //자신의 갯수의 반을
        candy[i] /= 2;
        // 오른쪽사람에게 줌
        arr[(i+1)%n] = candy[i];
    }

    //반개를 주고 남은 갯수와 더 해질 갯수 더함
    for (int i = 0; i < n; i++) {
        candy[i] += arr[i];
    }
}
```

---

#### references
<https://www.acmicpc.net/problem/9037>
