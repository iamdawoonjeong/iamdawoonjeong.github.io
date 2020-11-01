---
layout: single
title: "[Problem Solving - Programmers] 42587 프린터"
date: 2020-10-30 23:33:00.000000000 +09:00
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
- programmers
- queue
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-programmers-42587/"
---
# [Programmers] 42587 프린터

## 문제
일반적인 프린터는 인쇄 요청이 들어온 순서대로 인쇄합니다. 그렇기 때문에 중요한 문서가 나중에 인쇄될 수 있습니다. 이런 문제를 보완하기 위해 중요도가 높은 문서를 먼저 인쇄하는 프린터를 개발했습니다. 이 새롭게 개발한 프린터는 아래와 같은 방식으로 인쇄 작업을 수행합니다.

1. 인쇄 대기목록의 가장 앞에 있는 문서(J)를 대기목록에서 꺼냅니다.
2. 나머지 인쇄 대기목록에서 J보다 중요도가 높은 문서가 한 개라도 존재하면 J를 대기목록의 가장 마지막에 넣습니다.
3. 그렇지 않으면 J를 인쇄합니다.
예를 들어, 4개의 문서(A, B, C, D)가 순서대로 인쇄 대기목록에 있고 중요도가 2 1 3 2 라면 C D A B 순으로 인쇄하게 됩니다.

내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 알고 싶습니다. 위의 예에서 C는 1번째로, A는 3번째로 인쇄됩니다.

현재 대기목록에 있는 문서의 중요도가 순서대로 담긴 배열 priorities와 내가 인쇄를 요청한 문서가 현재 대기목록의 어떤 위치에 있는지를 알려주는 location이 매개변수로 주어질 때, 내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 return 하도록 solution 함수를 작성해주세요.

### 제한사항
현재 대기목록에는 1개 이상 100개 이하의 문서가 있습니다.
인쇄 작업의 중요도는 1~9로 표현하며 숫자가 클수록 중요하다는 뜻입니다.
location은 0 이상 (현재 대기목록에 있는 작업 수 - 1) 이하의 값을 가지며 대기목록의 가장 앞에 있으면 0, 두 번째에 있으면 1로 표현합니다.

### 입출력 예

| priorities | location |  return |
|:--------:|:--------:|:--------:|
| [2, 1, 3, 2]	| 2  |  1 |
| [1, 1, 9, 1, 1, 1] | 0 | 5 |


### 분류
- 큐

## 풀이

### 문제 파악
- 백준문제 [1966](http://dawoonjeong.com/algorithm-problem-solving-baekjoon-1966)와 유사한 문제
- 똑같이 구현했으나 시간초과로 실패

### 구현


#### Queue 사용

- 기존소스에서 max, maxIndex를 따로 구현해주었는데, maxIndex만 씀
- 찾아야할 문서의 값(target)도 따로 구현해 주었으나 index 값 체크로 확인하는 로직으로 수정
- 코드가 간결해줌  

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/programmers/lessons42587/Solution.java)

```java
int index = location;
int maxIndex = priorities.length-1;

while (!queue.isEmpty()) {

    if ( queue.peek() == priorities[maxIndex-answer] ) {
        queue.poll();
        answer+=1;

        if (index == 0) {
            queue.clear();
            break;
        }else {
            index--;
        }

    }else {
       queue.add(queue.poll());

       if (index == 0) {
           index = queue.size()-1;
       }else {
           index--;
       }
    }
}        
```

#### PriorityQueue 사용

- PriorityQueue<Integer>를 선언하여 Collections.reverseOrder() 해 줌

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/programmers/lessons42586/Solution2.java)

```java
PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
```

- offer로 element를 추가하면 내림차순으로 [3, 2, 2, 1] 저장 됨

```java
for (Integer priority : priorities) {
    pq.offer(priority);
}
```

- 로직이 매우 간단해짐
- 기존에 index 체크해주는 것이 없어짐

```java
while (!pq.isEmpty()) {
    for (int i = 0; i < priorities.length; i++) {
        if (pq.peek() == priorities[i]) {
            pq.poll();
            answer+=1;

            if (location == i) {
                pq.clear();
                break;
            }
        }
    }
}
```

---

#### references
<https://programmers.co.kr/learn/courses/30/lessons/42587>  
<https://jjjayyy.tistory.com/92>
