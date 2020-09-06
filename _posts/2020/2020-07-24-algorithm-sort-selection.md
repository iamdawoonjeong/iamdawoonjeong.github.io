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
- selection sort
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
# 정렬(Sort) - selection sort(선택정렬)


## selection sort(선택 정렬)
- 가장 간단한 정렬
- 각 요소를 정렬 된 배열의 적절한 위치에 삽입
- 빠른 정렬, 병합 정렬 등과 ​​같은 다른 정렬 알고리즘보다 효율성이 떨어짐
- 가장단순하다는 장점 밖에 없음
- 최소값을 선택해서 맨 앞에 위치 시킴

![algorithm-Selection-Sort-Animation]({{ site.baseurl }}/assets/images/posts/2020/algorithm-Selection-Sort-Animation.gif)

### 연산
1. 최소인덱스(array[0]) 값을 key으로 선택 (indexMin = i)
2. key 값 제외 배열 내 최소값을 찾기 (j = i+1 ; j < size)
3. key값보다 더 작은 값을 찾을 경우 교체 swap(array[indexMin], array[j])
4. 맨 처음 위치를 뺀 나머지 요소들을 같은 방법으로 반복 (i = 0 ; i < size-1)
5. 배열 내 최소 값이 맨 앞에 위치하게 되면서 오름차순 정렬 됨

###  pseudo code
```java
for i = 0 ; i < size-1
indexMin = i
   for j = i+1 ; j < size
      if arrayindexMin] > array[j]
         swap(array[indexMin], array[j])
      end if
   end for
end for
```

### java로 선택정렬 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-theory/src/sort/selection/SelectionSort.java)


```java
public void sortFor(int elementData[]){
    int size = elementData.length;

    for (int i = 1 ; i < size ; i++) {
        int key = elementData[i];
        int j;

        //반복문을 중첩 for로 했을 경우
        for (j = i-1; j >= 0 ; j--) {
            //key 보다 큰 값을 만나면
            if ( elementData[j] > key) {
                //해당 위치+1 에 큰 값을 대입 shift
                elementData[j+1] = elementData[j];
            } else {
               //정렬되어있기 때문에 key 보다 작은 값을 만날 경우 바로 반복문 빠져 나옴
               //작은값 위치 j 가지고 있음
                break;
            }
        }
        //key값을 작은값 보다 +1 위치에 넣어줌
        elementData[j+1] = key;
        System.out.println(toString());
    }
}
```


output


```java
[ * Selection Sort * ]
- before selection sort ----------
[9, 5, 6, 4, 7, 2, 1, 8, 3]
- sorting ----------
[1, 9, 6, 5, 7, 4, 2, 8, 3]
[1, 2, 9, 6, 7, 5, 4, 8, 3]
[1, 2, 3, 9, 7, 6, 5, 8, 4]
[1, 2, 3, 4, 9, 7, 6, 8, 5]
[1, 2, 3, 4, 5, 9, 7, 8, 6]
[1, 2, 3, 4, 5, 6, 9, 8, 7]
[1, 2, 3, 4, 5, 6, 7, 9, 8]
[1, 2, 3, 4, 5, 6, 7, 8, 9]
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
