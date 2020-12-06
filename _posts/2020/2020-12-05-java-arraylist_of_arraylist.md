---
layout: single
title: "[JAVA] ArrayList의 ArrayList"
date: 2020-12-05 17:00:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- array list
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-arraylist_of_arraylist/"
---
# ArrayList의 ArrayList

[0 만들기](http://dawoonjeong.com/algorithm-problem-solving-baekjoon-7490/) 풀면서 사용했던 ArrayList의 ArrayList
실질적으로 자주 쓰진 않지만 알아두면 알고리즘 문제 풀 때 한번씩 사용 하게 됨

### 사용법

- 선언

```java
ArrayList<ArrayList<Integer> > list = new ArrayList<ArrayList<Integer> >();
```

- value set

```java
// list is an ArrayList of ArrayLists
ArrayList<ArrayList<Integer>> list =  new ArrayList<ArrayList<Integer>>();

// Create n lists one by one and append to the  
// master list (ArrayList of ArrayList)
ArrayList<Integer> a1 = new ArrayList<Integer>();
a1.add(1);
a1.add(2);
list.add(a1);

ArrayList<Integer> a2 = new ArrayList<Integer>();
a2.add(5);
list.add(a2);

ArrayList<Integer> a3 = new ArrayList<Integer>();
a3.add(10);
a3.add(20);
a3.add(30);
list.add(a3);
```

- iterator

```java
for (ArrayList<Integer> al : list) {
    System.out.println(al);
}


for (int i = 0; i < list.size(); i++) {
    for (int j = 0; j < list.get(i).size(); j++) {
        System.out.print(list.get(i).get(j) + " ");
    }
    System.out.println();
}
```

- output

```java
[1, 2]
[5]
[10, 20, 30]
1 2
5
10 20 30
```

### 정렬하기

-  선언 및 데이터 입력

```java
ArrayList<ArrayList<Integer>> list2 =  new ArrayList<ArrayList<Integer>>();

ArrayList<Integer> b1 = new ArrayList<Integer>();
b1.add(5);
b1.add(3);
b1.add(2);
b1.add(1);
b1.add(4);
list2.add(b1);

ArrayList<Integer> b2 = new ArrayList<Integer>();
b2.add(10);
b2.add(40);
b2.add(50);
b2.add(30);
b2.add(20);
list2.add(b2);
```

- sort

```java
for (ArrayList<Integer> al : list) {
    Collections.sort(al);
    System.out.println(al);
}
```

- output

```java
[1, 2, 3, 4, 5]
[10, 20, 30, 40, 50]
```

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-basic/src/arraylistofarraylist/ArrayListOfArrayList.java)

---
#### references
<https://www.geeksforgeeks.org/arraylist-of-arraylist-in-java/>
