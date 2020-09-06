---
layout: single
title: "[Algorithm] 정렬(Sort)"
date: 2020-07-22 23:56:00.000000000 +09:00
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
- sort
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-sort/"
---
# Sort (정렬)
- 무질서한 자료들을 일정한 기준에 의하여 재배열 하는 과정  
- 파일에 저장된 레코드들을 특정 키(key) 필드에 다라 일정하게 재배열 하는 것
- 정렬문제의 해 또는 결과 : 정렬된 배열

#### 정렬의 키를 어떤순으로 정렬하는 가에 다른 구분
- Ascending sort (오름차순 정렬)
- Descending sort(내림차순 정렬)

#### 정렬방식이 수행되는 장소에 따라 구분
- Internal sort (내부정렬) : 파일을 주기억 장치 내부에 적재하여 정렬하는 방식
- External sort (외부정렬) : 정렬하려는 파일의 크기가 너무 커서 주기억 장치의 크기가 부족하여 모두 적재할 수 없을때 보조 기억 장치인 테이프나 디스크 이용하여 정렬을 수행하는 방식

#### 정렬방식에 의한 내부 정렬구분
- 교환 방식 : 키를 비교하여 교환에 의하여 정렬하는 방식 selection sort(선택 정렬), bubble sort(버블 정렬), quick sort(퀵 정렬)
- 삽입 방식 : 키를 비교하여 삽입에 의하여 정렬하는 방식 insertion sort(삽입 정렬), shell sort(쉘 정렬)
- 선택 방식 : 키를 비교하여 선택에 의하여 정렬하는 방식 heap sort(힙 정렬)
- 병합 방식 : 키를 비교하여 병합에 의하여 정렬하는 방식 2-way merge sort (병합 정렬), n-way merge sort (병합 정렬)
- 분배 방식 : 키를 구성하는 각 자릿수를 특정 bucket에 분배하여 정렬하는 방식 radix sort(기수 정렬), radix exchange sort(기수 교환 정렬)

#### 시간복잡도에 의한 내부 정렬 구분
- O(n<sup>2</sup>) 정렬 알고리즘 :  selection sort, bubble sort, quick sort, insertion sort, shell sort
- O(nlogn) 정렬 알고리즘 : quick sort, heap sort, merge sort

### Sort 종류
- selection sort(선택 정렬)
- bubble sort(버블 정렬)
- quick sort(퀵 정렬)
- insertion sort(삽입 정렬)
- shell sort(쉘 정렬)
- heap sort(힙 정렬)
- merge sort (병합 정렬)
- radix sort(기수 정렬)


---

#### references
<https://www.javatpoint.com/bubble-sort>  
<https://www.geeksforgeeks.org/merge-sort//>  
<https://www.tutorialspoint.com/data_structures_algorithms/sorting_algorithms.htm>  
