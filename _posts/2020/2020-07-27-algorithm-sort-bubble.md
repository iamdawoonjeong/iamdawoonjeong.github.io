---
layout: single
title: "[Algorithm] 정렬(Sort)-버블정렬(Bubble Sort)"
date: 2020-07-27 18:43:00.000000000 +09:00
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
- bubble sort
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-sort-bubble/"
---
# [Data Structure] 정렬(Sort) - bubble sort(버블정렬)


## bubble sort(버블 정렬)
- 인접한 두개의 배열 요소 key를 비교하여 교환하는 과정을 단계별로 거쳐 정렬이 완료될 때 까지 반복

### 연산
1. 주어진 리스트에서 i, i+1 값비교  
2. i+1의 값이 i보다 작을 경우 교체
3. 리스트 0번부터 맨마지막까지 계속 반복


###  pseudo code
```java
   for i = 0 to (n-1)
      if a[i] > a[i+1]
         swap(a[i], a[i+1])
      end if
   end for
```   


### java로 버블정렬 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-theory/src/sort/bubble/BubbleSort.java)


```java
 public void sort(int elementData[]) {
        int size  = elementData.length;

        for (int i = 0; i < size; i++) {
            for (int j = 0; j < size-i-1 ; j++) {
                //인덱스값이 1만큼 큰 값과 비교하여 작은 값을 만났을 경우
                if(elementData[j] > elementData[j+1]) {
                    //swap  
                    int temp = elementData[j];
                    elementData[j] = elementData[j+1];
                    elementData[j+1] = temp;
                }
            }
        }
    }
```



### Complexity


| Complexity | Best Case | Average Case | Worst Case |
|:--------:|:--------:|:--------:|:--------:|
| Time  | O(n<sup>2</sup>) | O(n) | O(n<sup>2</sup>) |
| Space |                  |      | O(1)             |


---
#### references
<https://www.javatpoint.com/bubble-sort>  
<https://www.geeksforgeeks.org/bubble-sort/>  
