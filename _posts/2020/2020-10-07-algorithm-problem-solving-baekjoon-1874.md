---
layout: single
title: "[Problem Solving - Baekjoon] 1874 스택수열"
date: 2020-10-07 22:45:00.000000000 +09:00
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
- stack
- baekjoon
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1874/"
---
# [Baekjoon Online Judge] 1874 스택수열


## 문제
스택 (stack)은 기본적인 자료구조 중 하나로, 컴퓨터 프로그램을 작성할 때 자주 이용되는 개념이다. 스택은 자료를 넣는 (push) 입구와 자료를 뽑는 (pop) 입구가 같아 제일 나중에 들어간 자료가 제일 먼저 나오는 (LIFO, Last in First out) 특성을 가지고 있다.

1부터 n까지의 수를 스택에 넣었다가 뽑아 늘어놓음으로써, 하나의 수열을 만들 수 있다. 이때, **스택에 push하는 순서는 반드시 오름차순을 지키도록 한다고 하자.** 임의의 수열이 주어졌을 때 스택을 이용해 그 수열을 만들 수 있는지 없는지, 있다면 어떤 순서로 push와 pop 연산을 수행해야 하는지를 알아낼 수 있다. 이를 계산하는 프로그램을 작성하라.


### 입력
첫 줄에 n (1 ≤ n ≤ 100,000)이 주어진다. 둘째 줄부터 n개의 줄에는 수열을 이루는 1이상 n이하의 정수가 하나씩 순서대로 주어진다. 물론 같은 정수가 두 번 나오는 일은 없다.


### 출력
입력된 수열을 만들기 위해 필요한 연산을 한 줄에 한 개씩 출력한다. push연산은 +로, pop 연산은 -로 표현하도록 한다. 불가능한 경우 NO를 출력한다.


### 예제1
- input
```
8
4
3
6
8
7
5
2
1
```

- output
```
+
+
+
+
-
-
+
+
-
+
+
-
-
-
-
-
```


### 예제2
- input
```
5
1
2
5
3
4
```

- ouput
```
NO
```


### 분류
- 자료 구조
- 스택


## 풀이

### 문제 파악

```java
8  // 입력될 숫자의 갯수 : N  
4  // N개의 수열
3
6
8
7
5
2
1
```
1. 스택의 push, pop 원리를 이용해서 주어진 수열을 표현해 하는 문제
2. 스택으로 표현이 안될 경우에는 NO 가 출력 되고, 표현 될 경우 push는 "+",  pop은 "-"로 표현 하여 출력


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1874/Main.java)

1. 입력을 scanner만 써오다가 InputStreamReader, BufferedReader를 이용해서 입력받음 (scanner와의 차이점은 추후 포스팅 예정)
```java
InputStreamReader isr = new InputStreamReader(System.in);
BufferedReader br = new BufferedReader(isr);
```

2. 출력을 저장하기 위해 StringBuilder 이용하는데, 사이즈를 가늠할 수 없어서 배열에 담지 않고 append를 이용해서 담을 예정.
   (배열은 얼마나 사이즈를 알 수 없기 때문이고 String 과의 차이점도 추후 포스팅 예정)
```java
StringBuilder sb = new StringBuilder();
```

3. 수열의 인덱스가 가리키는 수와 stack에 오름차순으로 넣은 수가 같은때까지 stack에 push하다가, 수가 같아지면 stack을 pop해주고 수열은 다음 인덱스를 가르침
```java
//스택에 push 하는 순서는 오름차순을 지키기 위해 for문 증가
for (int i = 1; i <= n; i++) {   
	//스택에 수열을 하나씩 넣고
    stack.add(i);
    //push를 + 표현하고, 예제 출력문 처럼 강제개행
    sb.append("+\n");

    //수열 요소의 값과, stack의 top의 값이 같다면
    while(stackp.peek() == arr[index]) {

        //stack을 pop해주고
        stack.pop();

        //pop을 - 로 표현하고, 예제 출력문 처럼 강제개행
        sb.append("-\n");

        //수열의 다음 값 비교를 위해 ++
        index++;

        //stack를 pop을 다 해서 비어있을 경우 해당 for문 빠져나오기
        if(stack.isEmpty()) {
            break;
        }
    }
}
```

4. 수열을 끝까지 탐색했고, stack이 비어있지않으면 정렬안된 수열이므로 NO 출력
```java
if(stack.isEmpty()) {
    //stack이 비어있으면 sb출력
    System.out.println(sb);
}else {
    //stack이 비어있지않으면 정렬이 안된 것 이므로 NO 출력
    System.out.println("NO");
}
 ```


---

#### references
<https://www.acmicpc.net/problem/1874>
