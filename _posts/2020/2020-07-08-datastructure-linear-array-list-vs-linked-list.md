---
layout: single
title: "[Data Structure] 선형 자료구조(3) - 배열 리스트(array list) VS 연결리스트(linked list)"
date: 2020-07-08 22:26:00.000000000 +09:00
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
- array list
- linked list
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/datastructure-linear-array-list-vs-linked-list/"
---
#[Data Structure] 선형 자료구조(3) - 배열 리스트(array list) VS 연결리스트(linked list)

## DataStruncture 에서의 Array  VS Linked List

|Algorithm | Array | Linked List |
|:--------:|:--------:|:--------:|
|	구조	|	배열은 유사한 유형의 데이터 요소 모음을 포함하는 데이터 구조	|	기본이 아닌 데이터 구조로 간주되며 노드라고 하는 정렬되지 않은 링크 된 요소의 모음이 포함	|
|	Search	|	요소는 인덱스가 있기때문에 접근이 쉬움	|	head부터 시작해서 i번째 요소에 도달 할 때까지 길을 따라야함 |
|	Access	|	액세스하는 것은 빠름	|	 선형 시간이 걸리므로 상당히 느림	|
|	Insertion / Deletion	|	많은 시간이 소요	|  성능은 빠름	|
|	Size	|	고정	|  동적이고 유연하며 크기를 확장 및 축소 가능	|
|	메모리 할당	| 컴파일 된 시간 동안 메모리가 할당	|  실행 또는 런타임 동안 할당|
|	메모리 저장  |	연속적으로 저장	|  무작위로 저장 |
|	메모리 요구  |	인덱스 내에 저장되기 때문에 메모리 요구 사항이 적음	|  다음 및 이전 참조 요소를 추가로 저장하기 때문에 더 많은 메모리가 필요함 |
|	메모리 효율	|	비효율적 |  효율적 |


## JAVA 에서의  Array  VS  List

### 리스트 (List) ?
- 개념은 순서가 있는 엘리먼트의 모임
- 빈 엘리먼트는 허용되지 않음
- 중복된 데이터를 허용한다는 것

### JAVA에서 List
- JAVA에서는 Collection Framework에서 지원하기 때문에 LinkedList, ArrayList 클래스 사용
- 특정 타입값들이 순차적으로 정렬된 컬렉션
- List를 사용하려면 메서드와 생성자, 매겨변수는 필드정의로 list인터페이스를 사용

### Array 와 List관계
- array 은 크기 명시 (계산 된 값을 이용하여 암시할수도 있음) : JVM은 배열이 생성될때 반드시 배열의 크기를 알아야 함
- 인덱스값을 이용한 접근 가능
- 원소 추가시 배열크기 늘려야함 (실제로는 현재 배열에 있는 모든 원소를 새로운 배열로 복사한 다음 새로운 배열이 원본배열의 주소를 가르키도록 재할당)


## JAVA 에서의  Array List  VS Linked List


### ArrayList
- 내부적으로 **동적 배열**을 사용하여 요소를 저장
- 요소를 제거하면 모든 비트가 메모리에서 이동
- List 만 구현하므로 목록으로만 작동
- **데이터 저장 및 액세스에 더 좋음**


### LinkedList
- 내부적으로 **이중 연결리스트 (linkDoubly Linked List)** 를 사용하여 요소를 저장
- 조작은 내부적으로 배열을 사용하기 때문에 느림
- linkDoubly Linked List 을 사용하므로 ArrayList보다 빠르므로 메모리에서 비트 이동이 필요하지 않음
- List 및 Deque 인터페이스를 구현하므로 목록 및 대기열 역할을 모두 수행
- **LinkedList는 데이터 조작에 좋음**


#### 원소의 갯수가 계속 변경되는 리스트라면 LinkedList 생성하는 것이 더 적합할 수 있음

![datastructure-arrayList-vs-linkedList]({{ site.baseurl }}/assets/images/posts/2020/datastructure-arrayList-vs-linkedList.png)


### 예제


#### JAVA ArrayList Collection Framework를 이용한 ArrayList 사용해보기
[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/list/ArrayListExample.java)


```java
// Creating object of the class Array List
ArrayList<Integer> numbers = new ArrayList<Integer>();
```


output


```java
0,10 1,20 2,30 3,40
===== insertion : add(1,50) =====
0,10 1,50 2,20 3,30 4,40
===== 순차적으로 읽기  - Iterator =====
10 50 20 30 40
===== 순차적으로 읽기 - foreach =====
10 50 20 30 40
=====  remove  =====
0,10 1,50 2,30 3,40
```


#### JAVA로 ArrayList 구현해보기
[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/list/arraylist/implementation/ArrayList.java)


```java
//배열로 구현해보기
private Object[] elementData = new Object[100];
```


output


```java
=====addLast =====
[10,20,30,40]
=====add =====
[10,15,20,30,40]
=====addFirst =====
[5,10,15,20,30,40]
=====remove =====
10
[5,15,20,30,40]
=====removeLast =====
40
=====removeFirst =====
5
[15,20,30]
=====get =====
15
20
30
=====size =====
3
=====indexOf =====
2
-1
=====Iteration : for=====
15
20
30
=====Iteration : clasee 생성 =====
=====next() =====
15
20
30
=====previous()=====
30
20
15
=====add,remove=====
[15,20,30,35]
```


---
#### references
<https://www.geeksforgeeks.org/linked-list-vs-array/>  
<https://www.javatpoint.com/difference-between-arraylist-and-linkedlist>  
<https://opentutorials.org/module/1335/8821>
