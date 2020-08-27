---
layout: single
title: "[Data Structure] 선형 자료구조(4) - 스택 (Stack)"
date: 2020-07-09 21:11:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- DataStructure
tags:
- data structure
- algorithm
- stack
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/datastructure-linear-stack/"
---
# [Data Structure] 선형 자료구조(4)  - 스택 (Stack)
- 배열 array
- 연결리스트 linked list
- **스택 stack**
- 큐 queue

## 스택 Stack
- **FILO(First In Last Out), LIFO(Last In First Out) 구조**, 첫 번째로 삽입 된 요소는 스택에서 마지막으로 삭제
- 순서가 지정된 목록 pushdown list
- top 이라는 한쪽 끝에서만 삽입 및 삭제가 수행 됨
- 스택은 최상위 요소를 가리키는 재귀 데이터 구조입니다.
- push (=add) : stack에 요소 추가
- pop (=delete) : stack에 요소 제거


![datastructure-stack-introduction]({{ site.baseurl }}/assets/images/posts/2020/datastructure-stack-introduction.png)


### Top의 값
- -1 : Empty
- 0	: stack 에 하나의 요소만 있음
- N-1 :Stack 이 full 인 상태
- N	: Overflow

### 장점
- 데이터의 삽입 삭제가 빠름

### 단점
- 탐색을 하려면 원소를 하나하나 꺼내서 옮겨가면서 해야함
- 맨위의 원소만 접근 가능

### 공간복잡도
- 최악의 경우 : O(n)

### 시간복잡도

|Algorithm | Average Case | Worst Case|
|:--------:|:--------:|:--------:|
|	Access	|	O(n)	|	 O(n)	|
|	Search	|	O(n)	|	O(n)	|
|	Insertion	|	O(1)	|	O(1)	|
|	Deletion	|	O(1)	|	O(1)	|


### 예제
#### JAVA Collection Framework의 Stack을 이용한 예제
- Java에서는 Stack 데이터 구조를 모델링하고 구현하는 Stack 클래스를 제공  
- Vector의 서브 클래스  


![datastructure-stack-in-java]({{ site.baseurl }}/assets/images/posts/2020/datastructure-stack-in-java.png)


[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/stack/StackExample.java)


```java
//Stack class 사용
Stack<Integer> stk = new Stack<Integer>();
```


output


```java
===== stack 생성 =====
===== insertion :  저장 add() =====
5
=====  deletion  : 삭제 remove() =====
[1, 2, 3]
=====  peek() =====
3
===== access : 순차적으로 읽기 - Iterator =====
1 2 3
```


#### JAVA로 배열을 이용해서 Stack 구현해 보기

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/stack/implementation/Stack.java)

```java
private Object[] elementData = new Object[size];  //배열 이용해서 생성
```

output

```java
===== createion stack and check size of stack=====
5
===== insertion  : 저장 push() =====

===== access =====
[10,20,30,40,50]

===== insertion (more than stack size) : overflow occur =====
...overflow

===== deletion : pop() =====
50
40
30

===== search : top() =====
20

===== access =====
[10,20]
20
10
===== deletion (empty stack)  =====
...empty
false
false
[]
```


---
#### references
<https://www.geeksforgeeks.org/stack-data-structure/>   
<https://www.geeksforgeeks.org/stack-class-in-java/>  
<https://www.javatpoint.com/data-structure-stack>  
<https://www.javatpoint.com/java-stack>  
