---
layout: single
title: "[Problem Solving - Baekjoon] 10989 수 정렬하기3"
date: 2020-10-19 18:35:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-10989/"
---
# [Baekjoon Online Judge] 10989 수 정렬하기3

## 문제
N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.

### 입력
첫째 줄에 수의 개수 N(1 ≤ N ≤ 10,000,000)이 주어진다. 둘째 줄부터 N개의 줄에는 숫자가 주어진다. 이 수는 10,000보다 작거나 같은 자연수이다.

### 출력
첫째 줄부터 N개의 줄에 오름차순으로 정렬한 결과를 한 줄에 하나씩 출력한다.

### 예제

- input
```java
10
5
2
3
1
4
2
3
5
1
7
```

- output
```java
1
1
2
2
3
3
4
5
5
7
```

### 분류
- 정렬


## 풀이

### 문제 파악

```java
10  // n 개의 수 가 나옴  
5   // 정렬할 숫자들
2
3
1
4
2
3
5
1
7
```

### 구현
1. 단순 정렬 문제 인가 싶어서 Arrays.sort() 이용
2. 풀이를 찾아보니 counting sort를 이용하라고 함


### Arrays.sort() 이용

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem10989/MainAPI.java)

- 그냥 출력 했더니 시간초과

```java
for (int i : arr) {
    System.out.println(i);
}
```

- StringBilder 사용해서 결과 붙이고 출력했더니 메모리 초과

```java
StringBuilder sb = new StringBuilder();
 for (int i : arr) {
            sb.append(i+"\n");
}
System.out.println(sb);       
```


- 시간초과의 문제를 BufferedWriter를 써서 해결

```java
OutputStreamWriter osw = new OutputStreamWriter(System.out);
BufferedWriter bw = new BufferedWriter(osw);

for (int i : arr) {
    bw.write(i+"\n");//출력
}

bw.flush();//남아있는 데이터를 모두 출력시킴
bw.close();//스트림을 닫음
```



### CountingSort 이용

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem10989/Main.java)

```java
for (int i = 0; i < N; i++) {
    int number = Integer.parseInt(br.readLine());
    arr[number] += 1;
}

for (int i = 1; i < 10001; i++) {

    while(arr[i] > 0){
        bw.write(i+"\n");
        arr[i]--;
    }
}
```


### 결론

- 이전 문제에서는 Arrays.sort()가 메모리, 속도면에서 효율이 좋으나 counting sort 문제 관련해서는 아닌란것이 증명 됨  


| 항목	   | Arrays.sort() |  counting sort |
|:--------:|:--------:|:--------:|
|  코드길이(Byte) |  964    |   1045 	|
|  메모리(KB) 	 |  365532 	|  280600 	|
|  시간(ms) 	     |  2636 	|  1704   	|
|  시간복잡도     | O(n log(n))  | O(n) 	|




---

#### references
<https://www.acmicpc.net/problem/10989>
