---
layout: single
title: "[Data Structure] 선형 자료구조(5) - 큐(Queue)"
date: 2020-07-10 18:29:00.000000000 +09:00
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
- queue
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/datastructure-linear-queue/"
---
# [Data Structure] 선형 자료구조(5)  - 큐(Queue)
- 배열 array
- 연결리스트 linked list
- 스택 stack
- **큐 queue**


## 큐(Queue)
- FIFO ( First In First Out) :  선입선출
- rear (뒤) :  삽입 작업을 수행
- front, head (앞): 삭제 작업을 수행


![datastructure-queue-introduction]({{ site.baseurl }}/assets/images/posts/2020/datastructure-queue-introduction.png)


### 장점
- 조치 순서에 상당히 공평
- 데이터의 삽입 삭제가 빠름

### 단점

- size 결정 : array로 구현한 queue일 경우, 배열의 크기를 미리 선언해야함.  runtime에 queue확장할 수 없고, 재사용 할 수 없음
- 메모리 낭비 : queue의 요소를 저장하는 데 사용되는 배열 공간은 해당 요소를 front end 에만 삽입 할 수 있고 front 값이 너무 높아서 큐 요소를 저장하는 데 재사용 할 수 없음. 그 전의 모든 공간은 결코 채워질 수 없음
- 대기열이 완전히 채워 졌으며, rear == max-1 조건 이 true 이므로 더 이상 요소를 삽입 할 수 없음


![datastructure-circular-queue]({{ site.baseurl }}/assets/images/posts/2020/datastructure-circular-queue.png)


- front end 에서 2개의 요소를 삭제했어도, rear = max -1 조건이 여전히 유지 되므로 요소를 삽입 할 수 없음


![datastructure-circular-queue2]({{ site.baseurl }}/assets/images/posts/2020/datastructure-circular-queue2.png)


### 종류
- 선형큐(Queue)
- 순환큐(Circular Queue)


### 응용
- 프린터, 디스크, CPU와 같은 단일 공유 리소스에 사용
- 데이터의 비동기식 전송 (데이터가 두 프로세스간에 동일한 속도로 전송되지 않는 경우)에 사용됩니다. 파이프, 파일 IO, 소켓
- 큐는 MP3 미디어 플레이어, CD 플레이어 등과 같은 대부분의 응용 프로그램에서 버퍼로 사용
- 재생 목록에서 노래를 추가하고 제거하기 위해 미디어 플레이어에서 재생 목록을 유지하는 데 사용
- 큐는 운영 체제에서 인터럽트를 처리하는 데 사용


### 공간복잡도
- 최악의 경우 : O(n)

### 시간복잡도

|Algorithm | Average Case | Worst Case|
|:--------:|:--------:|:--------:|
|	Access	|	θ (n)	|	 O(n)	|
|	Search	|	θ (n)	|	O(n)	|
|	Insertion	|	θ (1)	|	O(1)	|
|	Deletion	|	θ (1)	|	O(1)	|


### 예
#### JAVA Collection Framework를 이용한 Queue 사용해보기  
- 자료구조 를 구현한 자바 인터페이스
- add . remove . peek메서드 지원

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/queue/QueueExample.java)

```java
//Queue는 interface라 직접 객체 생성을 할 수 없으므로, LinkedList 로 인스턴스 생성
Queue<String> queue = new LinkedList<String>();		
```

output

```java
===== queue 생성 =====
===== insertion :  저장 add() =====
[A]
[A, B]
[A, B, C]
[A, B, C, D]
===== access : 순차적으로 읽기 - Iterator =====
A
B
C
D
E
===== 해당 큐의 head 조회 - poll() =====
A
true
=====  deletion  : 삭제 remove() =====
[C, D, E, F]
[D, E, F]
[E, F]
[F]
[]
===== 해당 큐의 head 조회 - poll() =====
null

```



#### JAVA로 Stack 구현해 보기

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/queue/implementation/Queue.java)


```java

    //데이터 추가시 rear 증가
	public boolean add(Object element) {

		if (isOverFlow()) {
			System.out.println("...queue over flow");
			return false;
		}else {
			if (front == -1 && rear == -1 ) {
				front++;
				rear++;
			}else {
				rear ++;
			}

			elementData[rear] = element;
		}

		return true;

	}

   //데이터 제거시 front 증가
	public Object remove() {
		if (isEmpty()) {
			System.out.println("... queue empty");
			return false;
		}else {
			Object removedElement = elementData[front];
			elementData[front] = null;
			front++;
			return removedElement;
		}
	}

```


output


```java
===== createion queue and check size of stqueueack=====
5
===== insertion :  저장 add() =====
[A,B,C,D,E]
===== deletion  : 삭제 remove() =====
[D,E]
D

```

## 순환 큐(Circular Queue)
- 첫 번째 인덱스는 마지막 인덱스 바로 다음에 옴
- front = -1 및 rear = max-1 일 때 순환 큐가 가득 참
- 선형 큐의 문제점인 메모리 낭비를 극복


![datastructure-circular-queue3]({{ site.baseurl }}/assets/images/posts/2020/datastructure-circular-queue3.png)



## 데크 (Deque : Double ended queue)
- 큐 2개를 반대로 붙여서 만든 자료구조
- Queue에 확장형으로 자료구조의 양끝에 원소를 추가하고 삭제 가능
- Queue 인터페이스 의 하위 유형
- 동적인 연결리스트에 의한 표현이 더욱 접함
- 입력 제한 데크 (scroll) : 입력이 한쪽 끝으로만 가능하도록 설정한 데크
- 출력 제한 데크 (shelf) : 출력이 한쪽 끝으로만 가능하도록 설정한 데크

![datastructure-deque]({{ site.baseurl }}/assets/images/posts/2020/datastructure-deque.png)




---
#### references
<https://www.javatpoint.com/data-structure-queue>  
<https://www.javatpoint.com/array-representation-of-queue>  
<https://www.javatpoint.com/java-priorityqueue>  
<https://www.geeksforgeeks.org/queue-data-structure/>   
<https://www.geeksforgeeks.org/queue-interface-java/>  
<https://www.geeksforgeeks.org/deque-interface-java-example/>  
