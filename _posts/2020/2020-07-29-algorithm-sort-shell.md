---
layout: single
title: "[Algorithm] 정렬(Sort)-쉘정렬(Shell Sort)"
date: 2020-07-29 18:43:00.000000000 +09:00
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
- shell sort
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-sort-shell/"
---
# 정렬(Sort) - shell sort(쉘정렬)


## shell sort(쉘 정렬)
- 쉘 정렬은 삽입 정렬의 일반화로 여러 위치의 간격으로 분리 된 요소를 비교하여 삽입 정렬의 단점을 극복한 정렬


### 연산
1. h 값 초기화
2. 목록을 동일한 간격 h의 더 작은 하위 목록으로 나눔 (데이터를 나누는 값은 보통 전체에서 2로 나누는 값(h/2)으로 진행하나, 3을 나누고 1을 더하는 경우(h/3+1)가 더 빠르다고 알려져 있음)
3. 삽입 정렬을 사용하여 이러한 하위 목록 정렬
4. 전체 목록이 정렬 될 때까지 반복

###  pseudo code
```java
   for gap = array size/2 to gap>0
      if a[i] > a[i-gap]
         swap(a[i], a[i-gap])
      end if
   end for
```   


### java로 쉘 정렬 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-theory/src/sort/shell/ShellSort.java)

```java
  public void sort(int elementData[]) {
        int size = elementData.length;

        //gap(h) 정하기 처음엔 배열길이/2 로 시작하여 계속해서 2로 나눔
        for (int gap = size/2 ; gap > 0 ; gap /=2) {
             for (int i = gap ; i < size ; i++) {
                // gap 위치인 i의 값을 temp에 저장해두기 ([i]값은 비워짐)
                int temp = elementData[i];

                int j;
                //temp에 넣어 둔 값과 gap반큼 뺀 인덱스위치의 값과 비교하여 temp값이 클 경우  
                for (j = i;  j >= gap && elementData[j-gap]>temp; j = j-gap) {
                    //swap
                    elementData[j] = elementData[j-gap];
                }
                //temp에 넣어둔 값 넣어주기
                elementData[j] = temp;
             }
        }
    }
```


- output


```java
[ * Shell Sort * ]
- before shell sort ----------
[9, 5, 6, 4, 7, 2, 1, 8, 3]
- sorting ----------
[3, 2, 1, 4, 7, 5, 6, 8, 9]
[1, 2, 3, 4, 6, 5, 7, 8, 9]
[1, 2, 3, 4, 5, 6, 7, 8, 9]
- after shell sort -----------
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

#### Complexity


| Complexity | Best Case | Average Case | Worst Case |
|:--------:|:--------:|:--------:|:--------:|
| Time  | Ω(nloegn)	| θ(nlog (n)<sup>2</sup>) | O(n log n<sup>2</sup>) |
| Space | | | O(1) |


---
#### references
<https://www.javatpoint.com/shell-sort>  
<https://www.geeksforgeeks.org/shellsort/>    
<https://www.tutorialspoint.com/data_structures_algorithms/shell_sort_algorithm.htm>  
