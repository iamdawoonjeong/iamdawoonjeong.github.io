---
layout: single
title: "[Data Structure] 선형 자료구조(2) - 연결리스트(linked list)"
date: 2020-07-07 21:57:00.000000000 +09:00
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
- list
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/datastructure-linear-list/"
---
# [Data Structure] 선형 자료구조(2) - 연결리스트(linked list)

- 배열 array
- **연결리스트 linked list**
- 스택 stack
- 큐 queue


## 연결리스트 (linked list)
- 비연속적인 기억장소에 **연결 필드를 사용하여 순차적으로 배당**
- 기억장소(메모리)를 동적으로 할당, 관리
- 공간 활용을 최적화
- 목록 크기는 메모리 크기로 제한되며 미리 선언 할 필요가 없음
- 링크 된 목록에 빈 노드가있을 수가 없음
- 단일 형식의 목록에 기본 유형 또는 객체의 값을 저장가능
- 종류 : 연길리스트(Linked List), 이중 연결 리스트(linkDoubly Linked List), 원형 연결 리스트(Circular Linked List) , 이중 원형 연결 리스트(Circular Doubly List)


![datastructure-Linkedlist]({{ site.baseurl }}/assets/images/posts/2020/datastructure-Linkedlist.png)


### node
- 메모리에 무작위로 저장된(정렬되지 않은) 노드 라고하는 객체의 모음
- 특정 주소에 저장된 데이터와 메모리에 있는 다음 노드의 주소를 포함하는 포인터를 포함
- 리스트의 마지막 노드는 널에 대한 포인터를 포함
- Data field, Link field 로 구성
- 첫번째 노드는 무엇인가는 Head 노드에 있음
- 마지막 노드는 무엇인가는 tail 노드에 있음

### 연결리스트 장점
- 동적크기
- 삽입, 삭제가 배열보다 용이/빠름

### 연결리스트 단점
- array처럼 인덱스를 이용한 임의 액세스가 허용되지 않아, 첫번째 노드부터 순차적으로 액세스 해야함 (조회가 느림)
- 단일 연결리스트는 이전노드의 주소를 모름
- 포인터를 위한 추가 메모리 공간 필요
- 다음 및 이전 참조 요소를 추가로 저장하기 때문에 연결 목록에 더 많은 메모리가 필요

### 공간복잡도
- 최악의 경우 : O(n)

### 시간복잡도

|Algorithm | Average Case | Worst Case|
|:--------:|:--------:|:--------:|
|	Access	|	θ(n)	|	 O(n)	|
|	Search	|	θ(n)	|	O(n)	|
|	Insertion	|	θ(1)	|	O(1)	|
|	Deletion	|	θ(1)	|	O(1)	|



### 예제
#### - JAVA Collection Framework를 이용한 LinkedList 사용해보기
- 실제 java의 linked list는 linkDoubly Linked List로 구현 됨   
[전체소스 보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/list/LinkedListExample.java)


```java
// Creating object of the class linked list
LinkedList<String> ll = new LinkedList<String>();
```


output

```java
===== insertion : linkedList.add(element) =====
[A, B]
===== insertion : addLast(element), addFrist(element) =====
[A, B, C]
[D, A, B, C]
===== store : add(index, element) =====
[D, A, E, B, C]
===== deletion : remove(element), remove(index) =====
[D, A, E, C]
[D, A, E]
===== deletion : reremoveFirstmove(), removeLast() =====
[A]
===== insertion =====
[A, B, C, D, E]
===== length : size() =====
5
===== searching : get(index) =====
A
===== 순차적으로 읽기 - for =====
A B C D E
===== 순차적으로 읽기 - Iterator =====
A
B
C
D
E
```


#### - JAVA로 linked list 구현해보기  
[전체 소스 보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/list/linkedlist/implementation/LinkedList.java)


```java
//핵심은 노드를 만드는 것
private Node head;
private Node tail;
private int size = 0;

private class Node{
    private Object data;
    private Node next;
    public Node(Object input) {
        this.data = input;
        this.next = null;
    }
}
```


output


```java
===== addFirst() =====
[10, 20, 30]
===== addLast() =====
[10, 20, 30, 40, 50, 60]
===== add() =====
[10, 15, 20, 30, 40, 50, 60]
===== removeFirst() =====
[15, 20, 30, 40, 50, 60]
===== remove() =====
40
[15, 20, 30, 50, 60]
===== removeLast() =====
60
[15, 20, 30, 50]
===== size() =====
4
===== get() =====
15
===== indexOf() =====
-1
=====Iteration : class 생성 =====
=====next() =====
15
true
20
true
30
true
50
false
[15, 20, 30, 50]
=====addFirst() =====
[10, 15, 20, 30, 50]
=====add() =====
[5, 10, 15, 20, 30, 50]

```

## 이중 연결 리스트 (Doubly Linked List)
- 노드에 시퀀스의 이전 노드와 다음 노드에 대한 포인터가 포함


![datastructure-doubly-linked-list]({{ site.baseurl }}/assets/images/posts/2020/datastructure-doubly-linked-list.png)


- 첫 번째 노드의 prev 부분과 마지막 노드의 next 항상 각 방향으로 끝을 나타내는 null을 포함
- linked list 에서는 한 방향으로 만 순회 할 수 있는 제한을 극복해서, 각 노드에는 이전 노드의 주소가 포함되어 있기 때문에 각 노드의 이전 부분에 저장된 이전 주소를 사용하여 이전 노드에 대한 모든 세부 정보를 찾을 수 있음


![datastructure-doubly-linked-list2]({{ site.baseurl }}/assets/images/posts/2020/datastructure-doubly-linked-list2.png)


### 이중 연결 리스트 장점
- 양방향으로 (앞뒤로) 포인터를 유지하므로 리스트의 요소를 쉽게 조작 가능

### 이중 연결 리스트 단점
- 모든 노드에 더 많은 공간을 소비하므로 삽입 및 삭제에서 광범위한 기본 작업이 발생 됨

### 예제
#### - JAVA로 doubly linked list 구현해보기  
[전체 소스 보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/list/doublylinkedlist/implementation/DoublyLinkedList.java)



```java
//핵심은 노드를 만드는 것
private Node head;
private Node tail;
private int size = 0;

private class Node{
    private Object data;
    private Node prev;
    private Node next;

    public Node(Object input) {
        this.data = input;
        this.prev = null;
        this.next = null;
    }
```


output


```java

===== addFirst() =====
[10, 20, 30]
===== addLast() =====
[10, 20, 30, 40, 50, 60]
===== add() =====
[10, 15, 20, 30, 40, 50, 60]
===== removeFirst() =====
[15, 20, 30, 40, 50, 60]
===== remove() =====
40
[15, 20, 30, 50, 60]
===== removeLast() =====
60
[15, 20, 30, 50]
===== size() =====
4
===== get() =====
15
===== indexOf() =====
-1
=====Iteration : class 생성 =====
=====next() =====
15
true
20
true
30
true
50
false
[15, 20, 30, 50]
=====addFirst() =====
[10, 15, 20, 30, 50]
=====add() =====
[5, 10, 15, 20, 30, 50]

```




## 원형 연결 리스트 (Circular Linked List)
- 마지막 노드는리스트의 첫 번째 노드에 대한 포인터를 포함
- node의 시작과, 끝이 없음
- 운영 체제의 작업 유지 관리에 사용


![datastructure-circular-singly-linked-list.png]({{ site.baseurl }}/assets/images/posts/2020/datastructure-circular-singly-linked-list.png)


### 원형 연결 리스트 장점
- 특정 노드의 위치를 찾아야 할 때, linked list처럼 첫번째 노드부터 찾지 않고, 앞에서 찾은 노드 다음 위치부터 찾을 수 있음

### 원형 연결 리스트 단점
- 이전노드의 주소를 모름




## 이중 원형 연결 리스트 (Circular Doubly List)
- Circular Doubly List는 노드에 NULL을 포함하지 않음
- 마지막 노드에는 첫 번째 노드 주소가 포함
- 목록의 첫 번째 노드에는 이전 포인터의 마지막 노드 주소도 포함


![datastructure-circular-doubly-linked-list]({{ site.baseurl }}/assets/images/posts/2020/datastructure-circular-doubly-linked-list.png)


### 이중 원형 연결 리스트 장점
- 포인터를 쉽게 조작 할 수 있으며 검색 효율이 두 배


### 이중 원형 연결 리스트단점
- 더 많은 공간과 더 비싼 기본 조작이 필요


---
#### references
<https://www.geeksforgeeks.org/data-structures/linked-list/>  
<https://www.geeksforgeeks.org/linked-list-in-java/>  
<https://www.javatpoint.com/singly-linked-list>  
<https://www.javatpoint.com/doubly-linked-list>  
<https://www.javatpoint.com/circular-singly-linked-list>  
<https://www.javatpoint.com/circular-doubly-linked-list>  
<https://opentutorials.org/module/1335/8636>  
<https://opentutorials.org/module/1335/8941>  
<https://visualgo.net/>  
