---
layout: single
title: "[Problem Solving - Baekjoon] 2014 소수의 곱"
date: 2021-01-15 22:45:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-2014/"
---
# [Baekjoon Online Judge] 2014 소수의 곱

## 문제
K개의 소수가 있다. 이때, 이 소수들 중에서 몇 개를 곱해서 얻게 되는 수들이 있을 것이다. 소수들을 선택할 때에는 같은 수를 선택해도 되며, 주어지는 소수 자체도 포함시키자.

예를 들어 세 소수가 2, 5, 7이었다면, 이러한 곱들을 오름차순으로 나타내 보면, 2, 4, 5, 7, 8, 10, 14, 16, 20, 25, 28, 32, 35, 등이 된다.

K개의 소수가 주어졌을 때, 이러한 소수의 곱들 중에서 N번째 수를 구해 보자. 단 정답은 231보다 작은 자연수이다.

### 입력
첫째 줄에 K(1 ≤ K ≤ 100), N(1 ≤ N ≤ 100,000)이 주어진다. 다음 줄에는 K개의 소수가 오름차순으로 주어진다. 같은 소수가 여러 번 주어지는 경우는 없으며, 주어지는 소수는 모두 541보다 작거나 같은 자연수이다.

### 출력
첫째 줄에 문제에서 설명한 대로 소수의 곱을 나열했을 때, N번째 오는 것을 출력한다.

### 예제

- input

```java
4 19
2 3 5 7
```

- output

```java
27
```

### 분류
- greedy

## 풀이

### 문제 파악

- 각 소수의 곱은 선택한 소수 보다 작음  

| 구분 | 소수 곱  |
|:----:|:-------:|
| 2    | 2 < 2*2 |
| 2    | 2 < 2*3 |
| 2    | 2 < 2*5 |
| 2    | 2 < 2*7 |
| 3    | 3 < 3*2 |
| 3    | 3 < 3*3 |
| 3    | 3 < 3*5 |
| 3    | 3 < 3*7 |
| 5    | 5 < 5*2 |
| 5    | 5 < 5*3 |
| 5    | 5 < 5*5 |
| 5    | 5 < 5*7 |
| 7    | 7 < 7*2 |
| 7    | 7 < 7*3 |
| 7    | 7 < 7*5 |
| 7    | 7 < 7*7 |

- 소수들이 hepa 들어가는 모습

```
2 3 5 7
3 5 7 2*2 2*3 2*5 2*7
5 7 2*2 2*3 2*5 2*7 3*2 ....
```


### 구현


[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2014/Main2.java)

- 2 3 5 7 을 반복 해서 곱했을 때, 곱해서나온 수(min)와 곱하는 수 (arr[i])  나누기 0 이 나오면 그뒤로는 계산이 필요없음

|      |     2   |     3   |    5    |    7    |
|:----:|:-------:|:-------:|:-------:|:-------:|
| 2    |  **4**  |    6    |   10    |   14    |
| 3    |  **6**  |  **9 ** |   15    |   21    |
| 5    |  **10** |  **15** | **25**  |   35    |
| 7    |  **14** |  **21** | **35**  | **49**  |


- 배열과 우선순위 큐를 선언하여 입력되는 수 담기
- 계산에 사용되는 변수는 int[^1]형으로 사용할 경우 틀리다고 나옴  
- 정답이 2의 31제곱 (2,147,483,648) 보다 작으므로 long[^2]형으로 선언해서 계산해주어야 하기 때문


```java
int[] arr = new int[k];
PriorityQueue<Long> pq = new PriorityQueue<Long>();

for (int i = 0; i < k; i++) {
    arr[i] = Integer.parseInt(st.nextToken());
    pq.offer((long) arr[i]);
}
```


- 메모리초과되므로 limit정해주기

```java
int index = 0; // 중복된수는 index 증가 안시키고 따로 관리하려고 선언
long min  = 0 ;
long limit = (long)Math.pow(2, 31); //메모리초과로 인한 limit 정해주기
```

- 우선순위 큐에서 뽑은 제일 적은 숫자를 대상으로 배열에 담겨있는 숫자하나씩 곱해주기
- 위에 표와 같이 나머지가 0인경우는 다음연산은 필요없음 (그 다음 계산부터는 중복되는 수가 나옴)

```java
while( index < n ) {
    //pq에서 최소수를 뽑고
    min  = pq.poll();

    //인덱스 증가
    index++;

    for (Integer it : arr) {
        System.out.println(min + " " + it);

        if ((min*it)  < limit) {
            pq.offer(min*it);
        }

        if (min%it == 0) {
            //for문 빠져나옴
            break;
        }
    }
}

```



### 구현2

- **set으로 중복체크하면 생각하기 매우 간단하나 메모리초과 발생 **

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2014/Main2.java)

- set 을 선언해 주고
```java
HashSet<Long> set = new HashSet<Long>();//계산되는 수의 중복체크를 위해
```

- pq 에 담기전 set에서 중복여부 체크해주고 중복이면 다음 식 계산하면 매우 간단

```java
while ( index < n ) {
        min = pq.poll();

        //set에 존재하면 중복이므로 넘어가고 다음수 뽑아서 진행
        if (set.contains(min)) {
            continue;
        }

        set.add(min);
        index++;

        for (Integer it : arr) {
            if (min*it < limit) {
                pq.offer(min*it);
            }
        }

    }
```

---

#### references
<https://www.acmicpc.net/problem/2014>

----

#### 주석
[^1]: 32비트 정수 (-2147483648 ~ 2147483647)
[^2]: 64비트 정수 (-9223372036854775808 ~ 9223372036854775807)
