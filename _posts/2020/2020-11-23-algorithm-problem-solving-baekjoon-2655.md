---
layout: single
title: "[Problem Solving - Baekjoon] 2655 가장높은탑쌓기"
date: 2020-11-23 18:30:00.000000000 +09:00
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
- DP
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-2655/"
---
# [Baekjoon Online Judge] 2655 가장높은탑쌓기

## 문제
밑면이 정사각형인 직육면체 벽돌들을 사용하여 탑을 쌓고자 한다. 탑은 벽돌을 한 개씩 아래에서 위로 쌓으면서 만들어 간다. 아래의 조건을 만족하면서 가장 높은 탑을 쌓을 수 있는 프로그램을 작성하시오.

1. 벽돌은 회전시킬 수 없다. 즉, 옆면을 밑면으로 사용할 수 없다.
2. 밑면의 넓이가 같은 벽돌은 없으며, 또한 무게가 같은 벽돌도 없다.
3. 벽돌들의 높이는 같을 수도 있다.
4. 탑을 쌓을 때 밑면이 좁은 벽돌 위에 밑면이 넓은 벽돌은 놓을 수 없다.
5. 무게가 무거운 벽돌을 무게가 가벼운 벽돌 위에 놓을 수 없다.

### 입력
첫째 줄에는 입력될 벽돌의 수가 주어진다. 입력으로 주어지는 벽돌의 수는 최대 100개이다. 둘째 줄부터는 각 줄에 한 개의 벽돌에 관한 정보인 벽돌 밑면의 넓이, 벽돌의 높이 그리고 무게가 차례대로 양의 정수로 주어진다. 각 벽돌은 입력되는 순서대로 1부터 연속적인 번호를 가진다. 벽돌의 넓이, 높이 무게는 10,000보다 작거나 같은 자연수이다.

### 출력
탑을 쌓을 때 사용된 벽돌의 수를 빈칸없이 출력하고, 두 번째 줄부터는 탑의 가장 위 벽돌부터 가장 아래 벽돌까지 차례로 한 줄에 하나씩 벽돌 번호를 빈칸없이 출력한다.

### 예제

- input

```java
5
25 3 4
4 4 6
9 2 3
16 2 5
1 5 2
```

- output

```java
3
5
3
1
```

### 분류
- 다이나믹 프로그래밍

## 풀이

### 문제 파악

- 입력된 벽돌 순서, 넓이, 무게, 높이

|벽돌순서|width|height|weigh|
|:----:|:----:|:----:|:-----:|
| 0 | 0 | 0 | 0 |
| 1 | 25 | 3 | 4 |
| 2 | 4 | 4 | 6 |
| 3 | 9 | 2 | 3 |
| 4 | 16 | 2 | 5 |
| 5 | 1 | 5 | 2 |


- 문제 조건 5에 의하여 무거운 벽돌이 가벼운 벽돌 위로 올라갈 수 없으므로, 무게순으로 쌓기로 함
- 무게순 벽돌 순서  0 - 5 - 3 - 1 - 4 - 2

|벽돌순서|width|height|weigh|
|:----:|:----:|:----:|:-----:|
| 0 | 0 | 0 | 0 |
| 5 | 1 | 5 | 2 |
| 3 | 9 | 2 | 3 |
| 1 | 25 | 3 | 4 |
| 4 | 16 | 2 | 5 |
| 2 | 4 | 4 | 6 |


- 무게 순으로 벽돌 쌓으면서 최대 높이 구하기

| 0 | 1 | 2 | 3 | 4 | 5 |
|:----:|:----:|:----:|:-----:|:-----:|
| 0 | 0 | 0 | 0 | 0 | 0 |
| 0 | 5 | 0 | 0 | 0 | 0 |
| 0 | 5 | 7 | 0 | 0 | 0 |
| 0 | 5 | 7 | 10 | 0 | 0 |
| 0 | 5 | 7 | 10 | 9 | 0 |
| 0 | 5 | 7 | 10 | 9 | 9 |

- max value = 10

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2655/Main.java)

- 주어진 벽돌 순서, 넓이, 무게, 높이를 다 입력 함
- arr[0] 은 벽돌 순서 입력  

```java
int[][] arr = new int[n+1][4];

for (int i = 1; i < n+1; i++) {
    StringTokenizer st = new StringTokenizer(br.readLine());
    arr[i][0] = i;
    arr[i][1] = Integer.parseInt(st.nextToken());  //width
    arr[i][2] = Integer.parseInt(st.nextToken());  //height
    arr[i][3] = Integer.parseInt(st.nextToken());  //weight
}

```

- 문제 조건 **5.무게가 무거운 벽돌을 무게가 가벼운 벽돌 위에 놓을 수 없다.** 로 무게 순으로 오름차순해서 벽돌을 쌓기

```java
//  weight순 오름차순정렬
Arrays.sort(arr, new Comparator<int[]>() {
    @Override
    public int compare(int[] o1, int[] o2) {
            return Integer.compare(o1[3], o2[3]);
    }
});

```

- 문제 조건 **4. 탑을 쌓을 때 밑면이 좁은 벽돌 위에 밑면이 넓은 벽돌은 놓을 수 없다.** 로 넓이를 비교하여 벽돌을 쌓기
- dp 에 각 벽돌을 쌓았을 때에 대하여 최대 높이를 계산한 값을 넣음

```java
int[] dp = new int[n+1];

for (int i = 1; i < n+1; i++) {
    for (int j = 0; j < i; j++) {
        if(arr[i][1] > arr[j][1]) {
            dp[i] = Math.max(dp[i], dp[j]+arr[i][2]);
        }
    }
}
```

- dp에 담아둔 벽돌의 최대 높이를 계산

```java     
//쌓은 벽돌들의 최대 높이를 계산
int maxValue = 0;
for (int i : dp) {
    maxValue = Math.max(i, maxValue);
}
```

- dp 맨뒤부터 max value 가 나온 인덱스 부터 ~ 0 까지의 벽돌번호 result에 담아두기  
- result 에 담을 때 마다, 현재 키를 빼줘야 다음 벽돌 계산 가능  

```java
int index = n;
ArrayList<Integer> result = new ArrayList<Integer>();

while (index != 0) {
    if (maxValue == dp[index]) {
        result.add(arr[index][0]);  //벽돌번호
        maxValue -= arr[index][2];  //키빼기
    }
    index--;
}
```

- 출력 첫번째줄 : 쌓은 벽돌의 갯수

```java
//쌓은 벽돌의 갯수
System.out.println(result.size());
```

- 출력 첫번째줄부터 ~ : 가장 위 벽돌부터 가장 아래 벽돌까지 차례로 한 줄에 하나씩 벽돌 번호를 빈칸없이 출력

```java
// 벽돌의 번호
for (int i = result.size()-1 ; i >= 0; i--) {
    System.out.println(result.get(i));
}
```

---

#### references
<https://www.acmicpc.net/problem/2655>
