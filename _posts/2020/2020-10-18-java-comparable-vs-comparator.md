---
layout: single
title: "[JAVA] Comparable VS Comparator"
date: 2020-10-18 23:17:00.000000000 +09:00
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
- comparable
- comparator
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-comparable-vs-comparator/"
---
# Comparable VS Comparator

## Comparable
- java.lang.Comparable
- compareTo() 메소드를 제공 : 문자열에 대한 자연정렬[^1]을 수행하는 데 사용

### 사용방법

- Comparable 클래스의 인스턴스를 생성

```java
int compareTo (T obj)

"a".compareTo("b") // -1 : 객체의 값이 더 작은 경우에는 음수 값을 반환
"b".compareTo("a") // 1 :  객체의 값이 더 높으면 양수 값을 반환
"a".compareTo("a") // 0 : 값이 같으면 0을 반환
```

- Arrays.sort()를 이용한 문자 내림차순 구현  

```java
Arrays.sort(arr2, new Comparator<String>() {

    @Override
    public int compare(String o1, String o2) {
        return o2.compareTo(o1);
    }
});
```

## Comparator
- java.util.Comparator
- Comparator는 우리가 비교하는 요소 유형 외부에 존재
- compare() 메소드를 제공
- Collections.Sort(), Arrays.sort() 작동시, Comparator의 compare()를 호출하여 객체를 정렬

### 사용 방법

- Comparator를 구현하는 클래스를 만듦(따라서 이전에 compareTo()에서 수행 한 작업을 수행하는 compare() 메서드)

```java
public class Test implements Comparator<Object> {

    @Override
    public int compare(Object o1, Object o2) {
        return 0;
    }
}
```

- Comparator 클래스의 인스턴스를 생성

```java
public int compare(Object obj1, Object obj2):
```

- 오버로드 된 sort () 메서드를 호출하여 Comparator를 구현하는 클래스의 목록과 인스턴스를 모두 제공

```java
Arrays.sort(arr, new Comparator<Integer>() {

    @Override
    public int compare(Integer o1, Integer o2) {
        return Integer.compare(o2, o1);
    }
});
```

- 첫 번째 인수가 두 번째 인수보다 작으면 음의 정수를 반환
- 첫 번째 인수와 두 번째 인수가 같으면 0을 반환
- 첫 번째 인수가 두 번째 인수보다 큰 경우 양의 정수를 반환



## 결론

- 객체 정렬이 자연 순서를 기반으로 해야하는 경우 Comparable을 사용
- 다른 객체의 속성에 대해 정렬을 수행해야하는 경우 Comparator를 사용
- Comparable은 단일 정렬 시퀀스를 제공하는 반면 Comparator는 여러 정렬 시퀀스를 제공
- Comparable은 원래 클래스에 영향을 주는 반면 comparator는 원래 클래스에 영향을주지 않음


---

#### references
<https://www.geeksforgeeks.org/comparator-interface-java/?ref=lbp>  
<https://www.geeksforgeeks.org/comparable-vs-comparator-in-java/?ref=lbp>



---

#### 주석

[^1]: 자연 정렬의 의미는 개체에 적용되는 정렬 순서 (예 : 정수 정렬을위한 숫자 순서, 문자열의 알파벳 순서 등)
