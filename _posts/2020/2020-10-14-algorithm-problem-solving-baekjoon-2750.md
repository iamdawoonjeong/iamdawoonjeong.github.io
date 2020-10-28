---
layout: single
title: "[Problem Solving - Baekjoon] 2750 수 정렬하기"
date: 2020-10-14 22:42:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Problem Solving
tags:
- data structure
- algorithm
- sort
- quick
- baekjoon
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-2750/"
---
# [Baekjoon Online Judge] 2750 수 정렬하기

## 문제
N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.

### 입력
첫째 줄에 수의 개수 N(1 ≤ N ≤ 1,000)이 주어진다.
둘째 줄부터 N개의 줄에는 숫자가 주어진다.
이 수는 절댓값이 1,000보다 작거나 같은 정수이다. 수는 중복되지 않는다.

### 출력
첫째 줄부터 N개의 줄에 오름차순으로 정렬한 결과를 한 줄에 하나씩 출력한다.

### 예제
- input
```
5
5
2
3
4
1
```

- output
```
1
2
3
4
5
```


### 분류
- 구현
- 정렬


## 풀이


### 문제 파악
1. 첫째줄에 수의 개수 n -> 두번째 줄부터 n개의 숫자들
2. 정렬 후 출력
```
5   // 수의 갯수 n
5   // 여기서 부터는 n개의 수들  
2
3
4
1
```


### 연산
1. 숫자의 갯수를 입력받고, 풀어야 할 숫자들 입력 받기
2. 정렬은 bubble sort 구현 or Arrsys.sort 를 사용하여 정렬
3. 출력

[참고:버블정렬](http://dawoonjeong.com/algorithm-sort-bubble/)

### 구현

#### bubble sort를 직접 구현 해서 정렬

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2750/Main.java)


```java
private static int[] solution(int[] numbers) {

    boolean swaped = false;
    for (int i = 0; i < numbers.length -1; i++) {

        swaped = false;
        for (int j = 0; j < numbers.length-1-i; j++) {
            //swap
            if (numbers[j] > numbers[j+1]) {
                int temp = numbers[j];
                numbers[j] = numbers[j+1];
                numbers[j+1] = temp;
                swaped = true;
            }
        }

        if (!swaped){
            break;
        }
    }

    return numbers;

}
```

#### Arrays.sort() 를 이용해서 정렬

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2750/MainAPI.java)

```java
Arrays.sort(numbers);
```

#### bubble sort VS Arrays.sort() 비교


| 항목	   | bubble sort  |  Arrays.sort() |
|:--------:|:--------:|:--------:|
|  코드길이(Byte) |  1519    |   872 	|
|  메모리(KB) 	 |  14048 	|  14000 	|
|  시간(ms) 	     |  164 	|  136   	|
|  시간복잡도     | O(n<sup>2</sup>) | O(n log(n)) 	|


- 메모리는 사용되는 변수에 따라 크게 달라질 수 있으나, 여기서는 별차이가 없다.
- PV 라고해서, 처음에 정렬문제 떠올랐을 때, bubbule sort를 굳이 구현해서 써야겠다는 생각이 앞섰으나,
  코드 길이로 보나 시간복잡도로 보나 간단한건 역시 자바에서 제공해주는 arrays.sort() 사용하는 것이 여러면에서 나은 것 같다.
  물론, 이는 채점프로그램이 제공해준다면 말이다.
- 심지어  arrays.sort()는 정렬 알고리즘 중에서 평균수행능력이 가장 뛰어난 quick sort(평균 시간복잡도 : O(n log n)) 보다 수행능력이 뛰어나다고 한다. (아래 java doc 참조)


> Sorts the specified array into ascending numerical order.
Implementation note: The sorting algorithm is a Dual-Pivot Quicksort by Vladimir Yaroslavskiy, Jon Bentley, and Joshua Bloch. **This algorithm offers O(n log(n)) performance on many data sets that cause other quicksorts to degrade to quadratic performance, and is typically faster than traditional (one-pivot) Quicksort implementations.**


---
#### references
<https://www.acmicpc.net/problem/2750>  
<https://docs.oracle.com/javase/7/docs/api/>
