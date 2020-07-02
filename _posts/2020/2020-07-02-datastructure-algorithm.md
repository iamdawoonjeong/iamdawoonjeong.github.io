---
layout: single
title: "[Data Structure] 자료구조/알고리즘 이란?"
date: 2020-07-02 22:47:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Algorithm
tags:
- data structure
- algorithm
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/datastructure-algorithm/"
---
# 자료구조(Data Structure), 알고리즘(Algorithm) 이란?

## 자료구조(Data Structure)
- 자료를 효율적으로 사용하기 위해서 자료의 특성에 따라서 분류하여 컴퓨터에 구성하고 저장하고 처리하는 방법
- 선택한 자료구조는 보다 효율 적인 알고리즘(어떤 문제를 해결하는 방법)을 사용할 수 있게 함
- 효과적으로 설계된 자료구조는 실행시간 혹은 메모리 용량과 같은 자원을 최소한으로 사용하면서 연산 수행
- 컴퓨터가 효율적으로 문제를 처리하기 위해서 문제를 정의하고 분석하여 그에 대한 최적의 프로그램 작성
- 레코드, 배열, 스택등과 같은 형태의 기억장소로 표현

### 자료구조의 분류
![datastructure-introduction]({{ site.baseurl }}/assets/images/posts/2020/datastructure-introduction.png)

#### 선형 자료구조 Linear data structure (1:1)
- 배열 array : 정적인 자료 구조
- 연결리스트 linked list : 연결필드(포인트)를 이용한 비연속적인 기억 공간에 저장하는 동적인 자료 구조
- 스택 stack : LIFO
- 큐 queue : FIFO

#### 비선형 자료구조 Non-Linear data structure
- 트리 tree (1 : n) : 관계를 표현하는 구조
- 그래프 graph ( n : m ) : 계층적인 관계를 나타내는 구조

### 자료구조 선택 기준
- 처리할 양에 따른 사용 가능한 기억 장소 측면 고려
- 삽입, 삭제에 관계된 갱신 여부나 활용빈도에 따른 자료 처리 속도, 기억 장소 고려
- 손쉬운 유지보수
- 기법이 용이성 측먄 고려



## 알고리즘(Algorithm)
- 문제해결 방법을 추상화하여 각 절차를 논리적으로 기술해 놓은 명세서/과정  
- 자료를 처리하는 입장에서 설명하면 가공되지 않은 입력된 자료를 받아들여, 그 입력자료에 어떤 변환과정을 거쳐 결과를 출력하는 일종의 함수(function)

### 순서도를 이용한 알고리즘 표현
![algorithm-diagram]({{ site.baseurl }}/assets/images/posts/2020/algorithm-diagram.png)


### 알고리즘성능분석방법

#### 공간복잡도 (space complexity)
- 알고리즘을 프로그램으로 실행하여 완료하기까지 필요한 총 저장 공간량
- 수행될때마다 얼마나 많은 저장공간이 필요한가
- **공간복잡도= 고정공간+ 가변공간**


#### 시간복잡도 (time complexity)
- 알고리즘을 프로그램으로 실행하여 완료하기까지의 총 소요시간
- 시간복잡도= 컴파일시간+ 실행시간
- 수행될때마다 처리하는 횟수 / 성능고려

#### 점근적 분석 , Big-O 복잡도
최악의 경우(worst case)에 대한 알고리즘 복장도 정의
- O(1) : 입력 자료의 수에 관계없이 일정한 실행 시간을 갖는 알고리즘
- O(log n) : 입력 자료의 크기가 n일경우 log n 번만큼의 수행시간을 가짐
- O(n) : 입력 자료의 크기가 n일경우 n 번만큼의 수행시간을 가짐
- O(n log n) : 입력 자료의 크기가 n일경우 n*(log n) 번만큼의 수행시간을 가짐
- O(n<sup>2</sup>) : 입력 자료의 크기가 n일경우 n의 2제곱번 만큼의 수행시간을 가짐
- O(n<sup>3</sup>) : 입력 자료의 크기가 n일경우 n의 3제곱번 만큼의 수행시간을 가짐
- O(2<sup>n</sup>) : 입력 자료의 크기가 n일경우 2의 n제곱번 만큼의 수행시간을 가짐
- O(n!) : 입력 자료의 크기가 n일경우 n*(n-1)*(n-2)... * 1(n!)번 만큼의 수행시간을 가짐


일반적인 알고리즘 문제의 기본 해법은 대부분 이 수행시간을 가짐 ex)외판원 문제(TSP)의 기본적인 해법


![datastructure-bigo]({{ site.baseurl }}/assets/images/posts/2020/datastructure-bigo.png)


### 알고리즘 선택시 고려 사항
- 속도가 빠른 알고리즘은 복잡해 지고, 속도가 느린 알고리즘은 단순해 짐   
- 속도가 빠를 수록 반복횟수를 줄이기 위해 구간내 조작이 복잡해짐   
- 자료의 양이 어느 정도 인가를 염두해두고 양이 적을때에는 O(n<sup>2</sup>)이 O(n log n)알고리즘 보다 효율적인 경우가 많음
- 1회성 용이 아닌, 계속 반복해서 사용하는 알고리짐이라면 반드시 시간이 걸리더라고 속도 빠른 알고리즘을 작성하는 것이 중요
- 속도가 빠른 알고리즘은 기억 공간을 많이 사용할 수 있으므로, 기억장소 사용량에 대해 확인하여 실제 사용 할 수 있는 알고리즘인지 고려 해야 함
- 동일한 알고리즘 이라도, 자료구조 및 기억장소의 운영 방법에 따라 수행시간, 공간 사용도는 큰 차이가 남
- 동일한 시간 복잡도를 가진 알고리즘이라도, 입력자료의 상태에 따라 수행시간 결과가 크게 차이나는 경우 발생할 수 있으며, 이에 따른 최악의 경우, 평균의 경우, 최선의 경우 등에 대한 수행 능력을 분석할수 있어야 함
- 정확성, 결함여부 등 전체적인 구조나 흐름이 읽기 쉽고, 이해하기 쉽고 수정에 용이 한가 역시 중요함


---
##### References
<https://ko.wikipedia.org/wiki/점근_표기법>  
<https://ko.wikipedia.org/wiki/알고리즘>  
<https://www.javatpoint.com/data-structure-algorithm>  
도서: C언어로 구현한 자료구조 (정일출판사 /임형근 저)
