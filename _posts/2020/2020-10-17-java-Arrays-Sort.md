---
layout: single
title: "[JAVA] Arrays.sort() vs Collections.sort()"
date: 2020-10-17 22:22:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- sort
- array
- collection
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-arrays-sort-vs-collections-sort/"
---
# Arrays.sort() vs Collections.sort()

## Arrays.sort()
- arrays 사용
- primitive data type이 아닌  Wrapper 클래스 (객체)를 사용 해야함

```java
int[] test = new int[5];  // primitive 자료형 : 에러 남
Integer[] arr = new Integer[5];
```

### 오름차순
- Arrays.sort();

```java
Arrays.sort(arr);
```

### 내림차순

- 숫자 내림차순

```java
Arrays.sort(arr, new Comparator<Integer>() {

        @Override
        public int compare(Integer o1, Integer o2) {
            return Integer.compare(o2, o1);
        }
    });
```

- 문자 내림차순

```java
Arrays.sort(arr2, new Comparator<String>() {

    @Override
    public int compare(String o1, String o2) {
        return o2.compareTo(o1);
    }
});
```


### 2차원 정렬

- 1번째 인덱스 기준으로 오름차순 정렬

```java
Arrays.sort(arr, new Comparator<int[]>() {
    @Override
    public int compare(int[] o1, int[] o2) {
		//0번째 인덱스 기준 정렬
        return  o1[0] - o2[0];
    }
});
```


- 1번째 인덱스가 같을때 2번째 인덱스 오름차순 정렬

```java
Arrays.sort(arr, new Comparator<int[]>() {
    @Override
    public int compare(int[] o1, int[] o2) {
        if (o1[0] == o2[0]) {
            return  Integer.compare(o1[1], o2[1]);
        }else
            return Integer.compare(o1[0], o2[0]);
        }
});
```

## Collections.sort()
- Arrays List, Linked List와 같은 objects Collections에 사용

```java
ArrayList<Integer> list = new ArrayList<Integer>();
LinkedList<String> list2 = new LinkedList<String>();
```

### 오름차순
- Collections.sort()

```java
Collections.sort(list);
```

### 내림차순
- Collections.reverseOrder () 사용

```java
Collections.sort(list, Collections.reverseOrder());
```


[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-basic/src/sort/SortAPI.java)

---
#### references
<https://www.geeksforgeeks.org/sorting-in-java/?ref=lbp>
