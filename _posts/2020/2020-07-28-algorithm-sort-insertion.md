---
layout: single
title: "[Algorithm] 정렬(Sort)-삽입정렬(Insertion Sort)"
date: 2020-07-28 18:43:00.000000000 +09:00
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
permalink: "/algorithm-sort-insertion/"
---
# [Data Structure] 정렬(Sort) - insertion sort(삽입정렬)


## insertion sort(삽입 정렬)
- 일상생활에서 자주 사용하는 정렬방식
- 단순하면서도 융통성이 있음
- 배열의 정렬되지 않은 요소 중 가장 작은 값이 모든 패스에서 선택되어 적절한 위치에 배열로 삽입됨


### 연산
1. n 크기의 arr을  i = 1에서 n-1까지의 루프
2. 요소 arr [i]를 선택하여 정렬 된 순서 arr [0… i-1]에 삽입


###  pseudo code
```java
   for i = 0 to (n-1)
      if a[i] > a[i+1]
         swap(a[i], a[i+1])
      end if
   end for
```   


### java로 삽입정렬 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-theory/src/sort/insert/InsertSort.java)


```java
    public void sort(int elementData[]){
        int size = elementData.length;

        for (int i = 0; i < size; i++) {
            int key = elementData[i];
            int j = i-1;

            //이미 정렬되어있는 i~1 부터 0 까지 의 값 중에서 i번째의 key 보다 큰 값을 만나면
            while(j >= 0 && elementData[j] > key) {
                //해당 위치에 큰 값을 대입
                elementData[j+1] = elementData[j];
                //큰 값일 나오지 않을때까지 반복  
                j = j-1;
           }
           //큰 값이 더이상 나오지 않고 while문이 종료되면
           //key값을 [j+1] 위치에 넣어줌
            elementData[j+1] = key;
        }
    }

```

#### Complexity


| Complexity | Best Case | Average Case | Worst Case |
|:--------:|:--------:|:--------:|:--------:|
| Time | Ω(n) | θ(n<sup>2</sup>) | O(n<sup>2</sup>) |
| Space | | | O(1) |



---
#### references
<https://www.javatpoint.com/insertion-sort>  
<https://www.geeksforgeeks.org/insertion-sort/>  
<https://www.tutorialspoint.com/data_structures_algorithms/insertion_sort_algorithm.htm>  
