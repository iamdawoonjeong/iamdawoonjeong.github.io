---
layout: single
title: "[Problem Solving - Baekjoon] 1092 배"
date: 2020-11-13 23:50:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-1092/"
---
# [Baekjoon Online Judge] 1092 배

## 문제
지민이는 항구에서 일한다. 그리고 화물을 배에 실어야 한다. 모든 화물은 박스에 안에 넣어져 있다. 항구에는 크레인이 N대 있고, 1분에 박스를 하나씩 배에 실을 수 있다. 모든 크레인은 동시에 움직인다.

각 크레인은 무게 제한이 있다. 이 무게 제한보다 무거운 박스는 크레인으로 움직일 수 없다. 모든 박스를 배로 옮기는데 드는 시간의 최솟값을 구하는 프로그램을 작성하시오.

### 입력
첫째 줄에 N이 주어진다. N은 50보다 작거나 같은 자연수이다. 둘째 줄에는 각 크레인의 무게 제한이 주어진다. 이 값은 1,000,000보다 작거나 같다. 셋째 줄에는 박스의 수 M이 주어진다. M은 10,000보다 작거나 같은 자연수이다. 넷째 줄에는 각 박스의 무게가 주어진다. 이 값도 1,000,000보다 작거나 같은 자연수이다.

### 출력
첫째 줄에 모든 박스를 배로 옮기는데 드는 시간의 최솟값을 출력한다. 만약 모든 박스를 배로 옮길 수 없으면 -1을 출력한다.

### 예제

- input

```java
3
6 8 9
5
2 5 2 4 7
```

- output

```java
2
```

### 분류
- 탐욕

## 풀이

### 문제 파악

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1092/Main.java)

- 크레인(cranes) 내림 차순으로 정렬
- 박스(box)를 내림차순으로 정렬

```java
//내림차순 정렬
Arrays.sort(cranes, new Comparator<Integer>() {

    @Override
    public int compare(Integer o1, Integer o2) {
        return Integer.compare(o2, o1);
    }
});

//내림차순 정렬
Arrays.sort(box, new Comparator<Integer>() {

    @Override
    public int compare(Integer o1, Integer o2) {
        return Integer.compare(o2, o1);
    }

});     
```

- 가장 무거운 박스를 가장 큰 크레인이 옮기지 못하는 경우는 -1로 출력

```java
//박스가 크레인보다 무거울 경우 옮기지 못 함
if (box[0] > cranes[0]) {
    System.out.println(-1);
    return ;
}
```

- 모든 크레인(n개)에 대해서 박스를 하나씩 옮길때 마다 시간(result)를 1씩 증가
- 크레인은  9-8-6  순으로 돌면서
- 박스 7-5-4-2-2 다 체크함
- n = 0 : 크레인 9 - 박스 7이 만나면  if문에서 박스 옮겨짐
- n = 1 : 그 다음 크레인 8을 가지고 박스 7 만나서 break; 그다음 박스 5 만나서 if 문 만나고 박스 옮겨짐
- 위와 같이 모든 크레인을 다돌고 나서도 옮긴박스 카운트 (count) 가 실제 박스 갯수 보다 작을 경우 다시 위 과정을 반복


```java
while(true) {
    //박스 다 옮겼으면 종료
    if(count == box.length) {
        break;
    }

    //모든 크레인에 대한 처리
    for (int i = 0; i < n; i++) {

      //아직 안 옮긴 박스 중에서 , 옮길 수 있는 박스를 만날 때까지 반복
        while(position[i] < box.length) {

            //박스를 0번부터 옮기며, 크레인이 박스의 보다 무거워야 옮기는 것 가능
            if (!checked[position[i]] && cranes[i] >= box[position[i]]){

                System.out.println(position[i] + " " + !checked[position[i]] );
                System.out.println(cranes[i] + " " + box[position[i]]);

                checked[position[i]] = true; //옮긴 박스는 옮겼다고 체크하고  
                position[i] += 1;  // 그 다음 박스를 옮겨야함
                count++; // 옮긴 박스 카운트
                break;
            }
            position[i] += 1; //다음박스를 옮기자
        }
    }
    result +=1; // 크레인 3개 한번에 동시에 사용했으므로, 1분 경과
}
System.out.println(result);
```

---
#### references
<https://www.acmicpc.net/problem/1092>
