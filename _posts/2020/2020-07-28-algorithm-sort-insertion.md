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
- insert sort
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
# 정렬(Sort) - insertion sort(삽입정렬)


## insertion sort(삽입 정렬)
- 일상생활에서 자주 사용하는 정렬방식
- 단순하면서도 융통성이 있음
- 배열의 정렬되지 않은 요소 중 가장 작은 값이 모든 패스에서 선택되어 적절한 위치에 배열로 삽입됨

![algorithm-insertionsort]({{ site.baseurl }}/assets/images/posts/2020/algorithm-insertionsort.png)



### 연산
1. index = 1 의 값을 key로 잡고 key 값 이전에 있는 위치한 배열들과 크기 비교  (j = i-1 ; j >= 0 ; j--)
2. key보다 큰 값을 만날 경우 찾은 큰 값을 큰값+1 위치로 shift (if array[j] > key array[j+1] = array[j])
3. key보다 작은 값을 만날 경우 해당 위치 +1 에 key값을 삽입
4. key의 위치를 증가시키면서 반복 (i = 1 ; i < size)
5. key 위치 이전의 요소들은 오름 차순으로 정렬이 되어 있음


###  pseudo code
```java
for i = 1 ; i < size
    key = array[i]
    for j = i-1 ; j >= 0 ; j--
        if array[j] > key
            array[j+1] = array[j]
        else break
        end if
    end for
    array[j+1] = key;
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


output

```java
[ * Insert Sort * ]
- ** before insert sort using for  ----------
[9, 5, 6, 4, 7, 2, 1, 8, 3]
- sorting ----------
[5, 9, 6, 4, 7, 2, 1, 8, 3]
[5, 6, 9, 4, 7, 2, 1, 8, 3]
[4, 5, 6, 9, 7, 2, 1, 8, 3]
[4, 5, 6, 7, 9, 2, 1, 8, 3]
[2, 4, 5, 6, 7, 9, 1, 8, 3]
[1, 2, 4, 5, 6, 7, 9, 8, 3]
[1, 2, 4, 5, 6, 7, 8, 9, 3]
[1, 2, 3, 4, 5, 6, 7, 8, 9]
- ** before insert sort using while ----------
[9, 5, 6, 4, 7, 2, 1, 8, 3]
- sorting ----------
[5, 9, 6, 4, 7, 2, 1, 8, 3]
[5, 6, 9, 4, 7, 2, 1, 8, 3]
[4, 5, 6, 9, 7, 2, 1, 8, 3]
[4, 5, 6, 7, 9, 2, 1, 8, 3]
[2, 4, 5, 6, 7, 9, 1, 8, 3]
[1, 2, 4, 5, 6, 7, 9, 8, 3]
[1, 2, 4, 5, 6, 7, 8, 9, 3]
[1, 2, 3, 4, 5, 6, 7, 8, 9]
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
