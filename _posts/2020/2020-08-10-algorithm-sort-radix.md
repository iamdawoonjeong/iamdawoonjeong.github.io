---
layout: single
title: "[Algorithm] 정렬(Sort)-기수 정렬(Radix Sort)"
date: 2020-08-10 21:21:00.000000000 +09:00
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
- radix sort
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-sort-radix/"
---
# 정렬(Sort) - 기수 정렬(Radix Sort)

## Radix Sort(기수 정렬)
- bucket(=queue) 에 분배하면서 정렬하는 방법
- LSD : Least Signification Digit (최하위 자릿수) 우선 정렬
- MSD : Most Siginification Digit (최상위 자릿수) 우선 정렬
- 기억장소 낭비

### 연산
1. 각 자료 최소 유효 자릿수에 해당하는 버킷에 모두 큐 순으로 분배하고 낮은 수의 버킷에서 부터 차례로 큐순으로 자료를 꺼냄
2. 각 자료를 십단위 값에 해당하는 버킷에 모두 분배하여 꺼내는 식으로 최대 유효 자릿수까지 반복 수행하면 정렬 됨  

### Example:

0. 아래와 같은 배열을 준비  


```
10,21,17,34,44,11,654,123
```


1.  LSD 정렬  : 1의 따라 분배  


```
0: 10
1: 21 11
2:
3: 123
4: 34 44 654
5:
6:
7: 17
8:
9:
```


- 결과


```
10,21,11,123,24,44,654,17
```


2. 10의 자리수에 따라 분배


```
0:
1: 10 11 17
2: 21 123
3: 34
4: 44
5: 654
6:
7:
8:
9:
```


- 결과

```
10,11,17,21,123,34,44,654
```


3. 100의 자리수에 따라 분배 (most significant digit)


```
0: 010 011 017 021 034 044
1: 123
2:
3:
4:
5:
6: 654
7:
8:
9:
```


- 결과


```
10,11,17,21,34,44,123,654
```


### java로 radix 정렬 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/sort/radix/RadixSort.java)


```java
public static int getMax(int[] arr, int n) {
    int max = arr[0];

    for (int i = 1; i < n; i++) {
         if (arr[i] > max) {
            max = arr[i];
         }
    }
    return max;
}


public static void countSort(int[] arr, int n, int exp) {
    int output[] = new int[n]; // output array
    int i;
    int count[] = new int[10];
    Arrays.fill(count, 0);

    //발생횟수를 count[] 저장
    for (i = 0; i < n ; i++) {
        count [(arr[i]/exp)%10]++;
    }

    //count [i]에 output[]의 숫자의 실제 위치가 포함되도록 count[i]를 변경
    for (i = 1; i < 10; i++) {
        count[i] += count[i-1];
    }

    //출력 배열 저장
    for (i = n-1 ; i >= 0; i--) {
       output[count[(arr[i]/exp)%10]-1]=arr[i];
       count[(arr[i]/exp)%10]--;
    }

    // output[]을 arr[]에 복사
    // arr []에 현재 배열에 따라 정렬 된 숫자가 포함됨
    for (i = 0; i < n; i++) {
        arr[i] = output[i];
    }
}
```


- output


```java
[ * Radix Sort * ]
- before radix sort ----------
[10,21,17,34,44,11,654,123]
- sorting ----------
[10,21,11,123,34,44,654,17]
[10,11,17,21,123,34,44,654]
[10,11,17,21,34,44,123,654]
- after radix sort ----------
[10,11,17,21,34,44,123,654]
```


#### Complexity


| Complexity | Best Case | Average Case | Worst Case |
|:--------:|:--------:|:--------:|:--------:|
| Time | Ω(n+k) | θ(nk) | O(nk) |
| Space | | | O(n+k) |


---

#### references
<https://www.javatpoint.com/radix-sort>   
<https://www.geeksforgeeks.org/radix-sort/>    
<https://www.hackerearth.com/practice/algorithms/sorting/radix-sort/tutorial/>  
