---
layout: single
title: "[Algorithm] 탐욕 알고리즘 - 허프만 코드 (Huffman Code)"
date: 2020-08-28 23:13:00.000000000 +09:00
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
permalink: "/algorithm-greedy-huffman/"
---

# 탐욕 알고리즘 - Huffman Code (허프만 코드)
- Huffman의 탐욕 알고리즘은 각 문자의 발생 빈도 테이블을 사용하여 각 문자를 이진 문자열로 표현하는 최적의 방법을 구축
- Huffman의 코딩은 코드 길이가 해당 문자의 상대적 빈도 또는 가중치에 따라 달라 지도록 문자에 코드를 제공


## 장점
- 데이터는 Huffman 코드를 사용하여 효율적으로 인코딩 될 수 있음
- 데이터를 압축하는 데 널리 사용되고 유익한 기술


## 압축 방법
### Fixed Length code (고정 길이 코드)
- 동일한 비트 수로 표시되는 각 문자
- 문자 당 최소 3 비트  


```java
000

b 001

c 010

d 011

e 100

f 101
```
- 10<sup>5</sup>자 파일의 경우 3 x 10<sup>5</sup> 비트 가 필요
- prefix가 없는 binary code는 leaf에 저장된 인코딩 된 문자와 함께 binary tree로 표시되거나 시각화 될 수 있음


### Prefix Code(접두사 코드)
- 저장공간을 절약하기 위한 방법인 Variable Length Code (가변 길이 코드)의 한 방법
- 접두사 코드는 인코딩과 디코딩을 명확히하기 때문에 바람직 함
- 파일의 각 문자를 설명하는 코드 단어를 연결하여 인코딩
- 인코딩 된 데이터로 시작하는 코드 워드는 명확하기 때문에 디코딩도 간단 함


## 특징
- Huffman tree 또는 Huffman 코딩 트리는 트리의 각 leaf이 주어진 알파벳의 문자에 해당하는 full bianry 정의 됨
- Huffman 트리는 최소 외부 경로 가중치와 관련된 binary tree로 취급 됨
- 주어진 leaf set에 대한 가중치 경로 길이의 최소 합과 관련된 것이며, 목표는 최소 외부 경로 가중치로 트리를 만드는 것



---

#### references
<https://www.javatpoint.com/greedy-algorithms>  
<https://www.javatpoint.com/huffman-coding>  
<https://www.geeksforgeeks.org/greedy-algorithms/>  
<https://www.geeksforgeeks.org/huffman-coding-greedy-algo-3/>  
<https://www.tutorialspoint.com/huffman-trees-in-data-structure>    
