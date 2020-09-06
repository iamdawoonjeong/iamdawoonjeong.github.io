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
# 정렬(Sort) - bubble sort(버블정렬)


## bubble sort(버블 정렬)
- 인접한 두개의 배열 요소 key를 비교하여 교환하는 과정을 단계별로 거쳐 정렬이 완료될 때 까지 반복

![algorithm-bubble-sort1]({{ site.baseurl }}/assets/images/posts/2020/algorithm-bubble-sort1.png)

### 연산
1. **주어진 배열에서 첫번째 요소부터 그 다음 요소의 값 비교 (j > j+1)**
2. **앞에 위치한 배열이 값이 더 클 경우 교체 swap(j, j+1) swap == true**
3. 배열 첫 요소부터 마지막-1 요소까지 한 번의 횟수를 비교 반복 했을 때, 마지막 요소는 배열 내 가장 큰 값이 오게 되어 있음
4. 마지막 요소를 제외하고 다시 처음부터 swap을 위한 위의 과정 반복 (for j=0 ; j < size-i-1)
5. 처음부터 다시 비교하는 반복횟수는 배열사이즈-1 만큼의 횟수 만큼 반복 하게 됨 (for i=0 ; j < size-1)
6. swap이 발생이 안 되었다면, 이미 정렬이 된 배열임으로 break문으로 빠져나오기 (if swap==false break)
7. 제일 큰 값이 맨 뒤에 위치하게 되면서 오른차순 정렬이 됨

###  pseudo code
```java
for i=0 ; i < size-1
    swap=false
    for j = 0 ; i < (size-i-1)
        if a[j] > a[j+1]
            swap(a[j], a[j+1])
            swap = true
        end if
    end for
    if swap == false break
ebd for
```   

### java로 버블정렬 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-theory/src/sort/bubble/BubbleSort.java)


```java
public void sort(int elementData[]) {
    int size  = elementData.length;

    //swap 했는지 체크
    boolean swaped ;
    for (int i = 0; i < size-1; i++) {

        swaped = false;
        for (int j = 0; j < size-i-1 ; j++) {

            //인덱스값이 1만큼 큰 값과 비교하여 작은 값을 만났을 경우
            if(elementData[j] > elementData[j+1]) {
                //swap  
                int temp = elementData[j];
                elementData[j] = elementData[j+1];
                elementData[j+1] = temp;
                swaped = true;
            }
        }

        //swap이 한번도 되지 않았다면 정렬되었음으로 break
        if (swaped==false) {
            break;
        }
        System.out.println(toString());
    }
}
```


output


```java
[ * Bubble Sort * ]
- before bubble sort ----------
[9, 5, 6, 4, 7, 2, 1, 8, 3]
- sorting ----------
[5, 6, 4, 7, 2, 1, 8, 3, 9]
[5, 4, 6, 2, 1, 7, 3, 8, 9]
[4, 5, 2, 1, 6, 3, 7, 8, 9]
[4, 2, 1, 5, 3, 6, 7, 8, 9]
[2, 1, 4, 3, 5, 6, 7, 8, 9]
[1, 2, 3, 4, 5, 6, 7, 8, 9]
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
