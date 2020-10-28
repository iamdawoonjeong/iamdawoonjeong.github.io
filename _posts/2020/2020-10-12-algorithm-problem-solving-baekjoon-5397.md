---
layout: single
title: "[Problem Solving - Baekjoon] 5397 키로거"
date: 2020-10-12 22:45:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-5397/"
---
# [Baekjoon Online Judge] 5397 키로거

## 문제
창영이는 강산이의 비밀번호를 훔치기 위해서 강산이가 사용하는 컴퓨터에 키로거를 설치했다. 며칠을 기다린 끝에 창영이는 강산이가 비밀번호 창에 입력하는 글자를 얻어냈다.

키로거는 사용자가 키보드를 누른 명령을 모두 기록한다. 따라서, 강산이가 비밀번호를 입력할 때, 화살표나 백스페이스를 입력해도 정확한 비밀번호를 알아낼 수 있다.

강산이가 비밀번호 창에서 입력한 키가 주어졌을 때, 강산이의 비밀번호를 알아내는 프로그램을 작성하시오.


### 입력
첫째 줄에 테스트 케이스의 개수가 주어진다. 각 테스트 케이스는 한줄로 이루어져 있고, 강산이가 입력한 순서대로 길이가 L인 문자열이 주어진다. (1 ≤ L의 길이 ≤ 1,000,000) 강산이가 백스페이스를 입력했다면, '-'가 주어진다. 이때 커서의 바로 앞에 글자가 존재한다면, 그 글자를 지운다. 화살표의 입력은 '<'와 '>'로 주어진다. 이때는 커서의 위치를 움직일 수 있다면, 왼쪽 또는 오른쪽으로 1만큼 움직인다. 나머지 문자는 비밀번호의 일부이다. 물론, 나중에 백스페이스를 통해서 지울 수는 있다. 만약 커서의 위치가 줄의 마지막이 아니라면, 커서 및 커서 오른쪽에 있는 모든 문자는 오른쪽으로 한 칸 이동한다.


### 출력
각 테스트 케이스에 대해서, 강산이의 비밀번호를 출력한다. 비밀번호의 길이는 항상 0보다 크다.


### 예제1
- input
```java
2
<<BP<A>>Cd-
ThIsIsS3Cr3t
```

- output
```java
BAPC
ThIsIsS3Cr3t
```

### 예제2 (반례찾기)
- input
```java
1
A<B<C<D<E
```
- output
```java
EDCBA
```

### 분류
- 자료 구조
- 스택


## 풀이

### 문제 파악

```java
2   //문제 케이스 갯수  들어감
<<BP<A>>Cd-  //키로거로 입력된 내용
ThIsIsS3Cr3t
```
1.  '-' 백스페이스
2.  '<' 마우스 커서가 왼쪽으로 (한칸 앞으로)
3.  '>' 마우스 커서가 오른쪽으로 (한칸 뒤로)
4. **스택을 두 개 이용해야 함** (처음에 linked list로 도전했다가 반례 나옴 실패)
5. 커서가  왼쪽 스택과 오른쪽스택 사이에 있다고 가정 하여 구현 => (head)left stack(tail) (커서)  (tail)right stack(head)   
6. 입력하면 왼쪽 스택에 쌓이고 삭제시 왼쪽스택부터 지움


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem5397/Main.java)

1. stack 두개 생성해주기
    ```java
    Stack<Character> leftStack = new Stack<Character>();
    Stack<Character> rightStack = new Stack<Character>();
    StringBuilder sb = new StringBuilder();
    ```

2. 입력받은 문자를 한글자씩 char[] 에 저장(foreach 로 한글자씩 비교하기 위해)
    ```java
    char[] word = str.toCharArray();
    ```

3. foreach문을 이용해 한글자씩 판단해 줌
    ```java
    for (char c : word) {
        switch (c) {
        case '-': {
            //'-' 를 만났을때는 왼쪽 스택 pop
            if (!leftStack.isEmpty()){
                leftStack.pop();
            }
            break;

        } case '<' :{
            //'<' 를 만났을때는 커서가 왼쪽으로 한칸 이동했기 때문에 왼쪽 스택 pop 한 후 오른쪽 스택에 push
            if (!leftStack.isEmpty()) {
                rightStack.push(leftStack.pop());
            }
            break;

        } case '>' :{
            //'>' 를 만났을때는 커서가 오른쪽으로 한칸 이동했기 때문에 오른쪽 스택 pop 한 후 왼쪽 스택에 push
            if(!rightStack.isEmpty()) {
                leftStack.push(rightStack.pop());
            }
            break;

        }
        //defualt는 왼쪽 스택에 쌓아주기
        default:
            leftStack.push(c);
            break;
        }

    }
    ```

4. 출력 (스택 FILO : pop할 경우 제일 나중에 입력한 것 부터 나옴)
    ```java
    //left stack 그냥 append로
    for (Character ch : leftStack) {
        sb.append(ch);
    }
    // right stack은 pop으로  
    while (!rightStack.isEmpty()) {
        sb.append(rightStack.pop());
    }
    ```


---

#### references
<https://www.acmicpc.net/problem/5397>
