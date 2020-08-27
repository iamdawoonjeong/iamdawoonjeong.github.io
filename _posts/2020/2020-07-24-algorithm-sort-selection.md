---
layout: single
title: "[Algorithm] 정렬(Sort)-선택정렬(Selection Sort)"
date: 2020-07-24 18:43:00.000000000 +09:00
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
- selection
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-sort-selection/"
---
# [Data Structure] 정렬(Sort) - selection sort(선택정렬)


## selection sort(선택 정렬)
- 가장 간단한 정렬
- 각 요소를 정렬 된 배열의 적절한 위치에 삽입
- 빠른 정렬, 병합 정렬 등과 ​​같은 다른 정렬 알고리즘보다 효율성이 떨어짐
- 가장단순하다는 장점 밖에 없음

### 연산
1. 최소인덱스(리스트[0]) 값을 key으로 선택
2. 리스트내 최소값을 찾아, key값과 교체(패스(pass)) (리스트내 key보다 작은 값을 찾아 swap해주는 걸 한번 반복 할 경우 결국 최소값과 교체하게 됨)
3. 맨 처음 위치를 뺀 나머지 리스트를 같은 방법으로 교체

###  pseudo code
```java
   for i = 0 to (n-1)
      if a[i] > a[j]
         swap(a[i], a[j])
      end if
   end for
```

### java로 선택정렬 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-theory/src/sort/selection/SelectionSort.java)


```java
    public void sort(int elementData[]){
        int size = elementData.length;
        for (int i = 0; i < size-1; i++) {
            int indexMin = i;

            for (int j = i+1 ; j < size; j++) {
                //배열 내, 최소인덱스에 있는 값보다 작은 값을 만났을 경우
                if (elementData[indexMin] > elementData[j]) {
                    //swap 해주기
                    int temp = elementData[indexMin];
                    elementData[indexMin] = elementData[j];
                    elementData[j] = temp;
                }
            }
        }
    }
```


### Complexity


| Complexity | Best Case | Average Case | Worst Case |
|:--------:|:--------:|:--------:|:--------:|
| Time  | Ω(n) | θ(n<sup>2</sup>) | O(n<sup>2</sup>) |
| Space |      |                  | O(1)             |


---
#### references
<https://www.javatpoint.com/selection-sort>   
<https://www.geeksforgeeks.org/selection-sort/>  
<https://www.tutorialspoint.com/data_structures_algorithms/sorting_algorithms.htm>  
<https://ko.wikipedia.org/wiki/%EC%84%A0%ED%83%9D_%EC%A0%95%EB%A0%AC>  
