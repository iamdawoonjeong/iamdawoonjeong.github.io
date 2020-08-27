---
layout: single
title: "[Data Structure] 선형 자료구조(1) - 배열(array)"
date: 2020-07-04 23:30:00.000000000 +09:00
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
- array
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/datastructure-linear-array/"
---
# [Data Structure] 선형 자료구조(1)  - 배열(array)

- **배열 array**
- 연결리스트 linked list
- 스택 stack
- 큐 queue


## 선형리스트(Linear List)란?
- 선형 리스트 (linear list) = 선형 자료구조 (linear data structure) = (ordered list/dense list/ sequential list)
- 빈틈없는 엘리먼트 적제
- 엘리먼트들의 논리적 순서 = 엘리먼트들의 물리적 순서

### 선형 리스트 종류
- 리스트 List  : 자료의 목록
- 선형리스트 Linear List : 순서를 갖는 리스트
- 다항식의 순차 자료구조
- 행렬의 순차 자료구조
- 배열
- 연결 리스트

### 선형리스트 자료 처리 조작
- 접근(access) : 특정 자료 항목의 위치를 찾는 조작
- 삽입, 추가 (insertion) : 리스트의 순서를 유지하면서 새로운 자료 입하는 조작
- 삭제, 제거 (deletion) : 리스트의 순서를 유지하면서 특정 자료 삭제 하는 조작
- 리스트 길이구하기 (length)
- i번째 요소 찾기 (searching)
- i번째 요소에 내용 수정하기 (modifying)
- i번째 요소에 자료 저장하기 (store)
- 리스트 전체를 순차적으로 읽기 (access)
- 둘이상의 리스트 하나로 만들기 (merging)
- 리스트내의 모든 자료들을 어떤 기준에 따라 새로운 순서로 정렬하기(sorting)
- 리스트 전체 또는 일부 자료들을 복사하여 새로운 리스트 만들기 (copying)
- 하나의 리스트를 둘, 또는 그이상의 새로운 부분 리스트로 만들기 (splitting)



## 배열 (array) : 순차자료구조
- 가장 보편적이고 단순한 선형리스트 구조
- 정적인 자료 구조   
- 항목을 순차적으로 **연속적인 기억장소** 에 배당  


![datastructure-Arrays]({{ site.baseurl }}/assets/images/posts/2020/datastructre-Arrays.png)


### 배열의 장점
- O(1)시간에 i 번째 자료에 직접 접근 가능
- 삽입,삭제가 발생하지 않는 정적인 응용 업무에서 처리해야할 자료가 언제나 같은 개수를 유지할 경우 기억장소 100%활용하기 때문에 좋은 구조 (density = 1 )

### 배열의 단점
- 메모리 사용의 비효율성
- 배열의 크기를 프로그램 실행전에 최대크기로 선언해야 함 (런타임에 확장 불가)
- 배열의 모든 요소는 연속적으로 메모리에 저장되어야 함
- 추가 삭제 후에 연속적인 물리 주소를 유지하기 위한 엘리먼트들을 이동시키는 추가 적인 작업과 시간 소요 (연산량이 많아짐)
- 원소 삭제해도 크기는 줄어들지 않음
- 추가삭제는 느리지만 인덱스 조회는 빠름


### 시간복잡도 계산

|algorithm | average case | worst case|
|:--------:|:--------:|:--------:|
|	access	|	O(1)	|	O(1)	|
|	search	|	O(n)	|	O(n)	|
|	insertion	|	O(n)	|	O(n)	|
|	deletion	|	O(n)	|	O(n)	|

- 삽입 : (n+1)/2 = O(n)
- 삭제 : (n-1)/2 = O(n)
- 검색 : 순차 검색의 경우 O(n)  


### 공간복잡도
- 최악의 경우 : O(n)


### 배열의 요소에 액세스
- 배열의 첫 번째 요소의 저장 주소 : base address (운영체제가 배당하는 주소)
- 배열요소의 크기 : size  
**a[i] 요소의 바이트 주소 = base address + ( size x i )**


### 예제: 자바의 1차원 배열
[1차원 배열 예제 소스](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/array/ArrayExample.java)

output


```java
===== store :  array[i] = data , modifying : array[i] = newdata - i번째 요소저장 =====
===== searching : array[i] - i번째 요소찾기(1) (numbers1[0]) =====
10
===== i번째 요소찾기(2) : 값이 없는 경우 =====
0 : int는 0출력
null : string은 null 출력
===== 배열의 크기 찾기 - array.length =====
4
===== Iteration(반복)으로 순차적으로 읽기1 - while =====
10
20
30
0
===== Iteration(반복)으로 순차적으로 읽기2 - for =====
10
20
30
0
```


### 다차원 배열의 요소에 액세스
- 2차원 배열의 주소  
**a[i][j] 요소의 바이트 주소 = base address + size * ( i x 최대 열의 수 + j)**
- 3차원 배열의 주소  
**a[i][j][k] 요소의 바이트 주소 = base address + size * (( i x 최대 행의수 x 최대 열의 수) + ( j x 최대 열의 수)  + k)**


### 예제: 자바의 다차원 배열
[다차원 배열 예제 소스](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/array/ArrayNExample.java)

output

```java
===== 2차원 배열 생성 방법 (1) =====
1 2 0
0 0 0
0 0 0
0 0 5
===== 2차원 배열 생성 방법 (2) (불규칙 가능) =====
0 0 0 0
0 0 0 0 0
0 0 0 0 0 0
===== 2차원 배열 생성 방법 (3) =====
1 2 3 4 5
2 3 4 5 6
6 7 8 9 0
===== 2차원 배열 생성 방법 (4) =====
1 2 3 4 5
2 3 4 5 6
6 7 8 9 0
===== searching : array[i] - i번째 요소찾기(1) (d[2][3]) =====
5
0
===== 배열의 크기 찾기 - array.length =====
3 * 5
===== Iteration(반복)으로 순차적으로 읽기 - for =====
1 2 3 4 5
2 3 4 5 6
6 7 8 9 0
```

---
#### references
<https://www.geeksforgeeks.org/arrays-in-java/>  
<https://www.geeksforgeeks.org/array-data-structure/>  
<https://www.javatpoint.com/data-structure-array>  
<https://www.javatpoint.com/data-structure-2d-array>  
<https://opentutorials.org/module/1335/>  
