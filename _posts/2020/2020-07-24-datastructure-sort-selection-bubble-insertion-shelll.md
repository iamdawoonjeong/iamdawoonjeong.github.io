---
layout: single
title: "[Data Structure] 정렬(Sort)-선택정렬, 버블정렬, 삽입정렬, 쉘정렬 정의 및 구현"
date: 2020-07-24 18:43:00.000000000 +09:00
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
- sortß
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/datastructure-sort-selection-bubble-insertion-shell/"
---
# [Data Structure] 정렬(Sort) - selection sort(선택정렬) bubble sort(버블정렬), insertion sort(삽입정렬), shell sort(쉘정렬) 정의 및 구현


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

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/sort/selection/SelectionSort.java)


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

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/sort/bubble/BubbleSort.java)


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

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/sort/insert/InsertSort.java)


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

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/sort/shell/ShellSort.java)

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


#### Complexity


| Complexity | Best Case | Average Case | Worst Case |
|:--------:|:--------:|:--------:|:--------:|
| Time  | Ω(nloegn)	| θ(nlog (n)<sup>2</sup>) | O(n log n<sup>2</sup>) |
| Space | | | O(1) |


---
#### references
<https://www.javatpoint.com/selection-sort>  
<https://www.javatpoint.com/bubble-sort>  
<https://www.javatpoint.com/insertion-sort>  
<https://www.javatpoint.com/shell-sort>  
<https://www.javatpoint.com/quick-sort>  
<https://www.geeksforgeeks.org/selection-sort/>  
<https://www.geeksforgeeks.org/bubble-sort/>  
<https://www.geeksforgeeks.org/insertion-sort/>  
<https://www.geeksforgeeks.org/shellsort/>  
<https://www.geeksforgeeks.org/quick-sort/?ref=lbp/>  
<https://www.tutorialspoint.com/data_structures_algorithms/sorting_algorithms.htm>  
<https://www.tutorialspoint.com/data_structures_algorithms/selection_sort_algorithm.htm>  
<https://www.tutorialspoint.com/data_structures_algorithms/insertion_sort_algorithm.htm>  
<https://www.tutorialspoint.com/data_structures_algorithms/shell_sort_algorithm.htm>  
<https://ko.wikipedia.org/wiki/%EC%84%A0%ED%83%9D_%EC%A0%95%EB%A0%AC>  
