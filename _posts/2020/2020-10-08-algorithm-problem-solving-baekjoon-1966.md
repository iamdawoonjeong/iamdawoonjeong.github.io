---
layout: single
title: "[Problem Solving - Baekjoon] 1966 프린터큐"
date: 2020-10-08 23:25:00.000000000 +09:00
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
- queue
- baekjoon
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1966/"
---
# [Baekjoon Online Judge] 1966 프린터큐

## 문제
여러분도 알다시피 여러분의 프린터 기기는 여러분이 인쇄하고자 하는 문서를 인쇄 명령을 받은 ‘순서대로’, 즉 먼저 요청된 것을 먼저 인쇄한다. 여러 개의 문서가 쌓인다면 Queue 자료구조에 쌓여서 FIFO - First In First Out - 에 따라 인쇄가 되게 된다. 하지만 상근이는 새로운 프린터기 내부 소프트웨어를 개발하였는데, 이 프린터기는 다음과 같은 조건에 따라 인쇄를 하게 된다.

현재 Queue의 가장 앞에 있는 문서의 ‘중요도’를 확인한다.
나머지 문서들 중 현재 문서보다 중요도가 높은 문서가 하나라도 있다면, 이 문서를 인쇄하지 않고 Queue의 가장 뒤에 재배치 한다. 그렇지 않다면 바로 인쇄를 한다.
예를 들어 Queue에 4개의 문서(A B C D)가 있고, 중요도가 2 1 4 3 라면 C를 인쇄하고, 다음으로 D를 인쇄하고 A, B를 인쇄하게 된다.

여러분이 할 일은, 현재 Queue에 있는 문서의 수와 중요도가 주어졌을 때, 어떤 한 문서가 몇 번째로 인쇄되는지 알아내는 것이다. 예를 들어 위의 예에서 C문서는 1번째로, A문서는 3번째로 인쇄되게 된다.


### 입력
첫 줄에 test case의 수가 주어진다. 각 test case에 대해서 문서의 수 N(100이하)와 몇 번째로 인쇄되었는지 궁금한 문서가 현재 Queue의 어떤 위치에 있는지를 알려주는 M(0이상 N미만)이 주어진다. 다음줄에 N개 문서의 중요도가 주어지는데, 중요도는 1 이상 9 이하이다. 중요도가 같은 문서가 여러 개 있을 수도 있다. 위의 예는 N=4, M=0(A문서가 궁금하다면), 중요도는 2 1 4 3이 된다.


### 출력
각 test case에 대해 문서가 몇 번째로 인쇄되는지 출력한다.

### 예제
- input
```java
3
1 0
5
4 2
1 2 3 4
6 0
1 1 9 1 1 1
```

- output
```java
1
2
5
```

### 반례찾기 예제
- intput
```java
4
1 0
5
4 2
1 2 3 4
6 0
1 1 9 1 1 1
4 2
7 1 5 6
```

- output
```java
1
2
5
3
```

### 분류
- 구현
- 자료 구조
- 시뮬레이션
- 큐

## 풀이

### 문제 파악
```java
3      //test case 갯 수
1 0    //문서의 수 N /  어떤 위치에 있는지를 알려주는 M ( 0 <= M < N)
5      //N개 문서의 중요도
4 2
1 2 3 4
6 0
1 1 9 1 1 1
```
1. N개의 수와 M의 위치로 문서들중 M이 몇번째로 출력되는지 알아내는 문제
2. 3개의 케이스중두 번째 케이스 : 4개의 문서가 있는데 2번째 문서의 출력 순서는 3번째
3. 즉, 중요도 "3"의 출력 순서를 구해야하는데, 중요도가 더 큰 문서 4가 존재하니 이 문서가 출력 되고 중요도 3 문서가 출력 됨


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1966/Main.java)

- 1. **queue의 특성을 이용하기 위해 queue를 선언하여 각 테스트 케이스의 문서 중요도를 넣어줌**

```java
Queue<Integer> queue =  new LinkedList<Integer>();
```

- 2. 문서들의 중요도를 알기 위해 정렬해서 maxIndex 값을 따로 관리해주면서 사용

```java
Arrays.sort(arr); // 입력된 배열을 정렬해서 이용해줌 (원래 배열은 queue에 담에서 사용)
int maxIndex = arr.length-1;
int max = Integer.parseInt(arr[maxIndex]); //최대값
```

- 3. 반복문에서 따로 관리해주어야 할 변수들

```java
int count = 0; // 출력횟수 (몇번째로 출력되나?)

// queue가 index를 지원하지 않아서 출력순서 찾아야할 위치를 따로 관리
int index = M;   

int result = 0;  // 출력순서 결과값 따로 담기

//M번째 위치해있는 우선순위 (내가 출력순서를 찾아야 할 우선순위)
int target = Integer.parseInt(arr[M]);  
```

- 4. if 문서가 출력되는 경우 else 출력되지 않는 경우

- 5. ____문서가 출력되는 경우 if 내가 찾는 문서를 출력하는 경우 else 내가 찾는 문서는 아니나, 순서도가 높아서 출력 하는 경우

- 6. ____문서가 출력되지 않는 경우 : 우선 순위 작은거 만났을 때 뒤로 보내기 if 내가 찾는 문서 순서도가 낮아서 뒤로 가야하는 경우

```java
while (true) {

    //1. 출력되는 경우 : 우선순위 값 == head의 값 같음
    if (queue.peek() == max) {

        // 내가 원하는걸 찾았 을 때
        if (( max == target )  && (queue.peek() == target) && (index == 0)) {
            result =   ++count;
            break;
        }else {
        // 찾지 못했으나, 우선수위 임으로 출력
            queue.poll();
            count++;

            index--; //찾는게 한자리 앞으로 움직임
            maxIndex--; ; //맥스값도 하나 낮아짐
            max = Integer.parseInt(arr[maxIndex]);
        }

    } else if (queue.peek() < max) {
    //2. 출력되지 않는 경우 : 우선순위 작은거 만났을때-> queue에서 dequeue 후 inqueue해주기  

        //queue head에서 poll로 뽑은 후
        int temp = queue.poll();
        //다시 넣어줌
        queue.add(temp);

        //내가 찾아야하는 문서가 우선순위가 낮아서 다시 뒤로가야하는경우
        if (index==0) {
            //index값 재조정 (남은 배열 갯수 맨 뒷자리로 가게 되어있음)
            index = N-1-count;
        }else {
            index--;
        }

    }
}
```


---

#### references
<https://www.acmicpc.net/problem/1966>
