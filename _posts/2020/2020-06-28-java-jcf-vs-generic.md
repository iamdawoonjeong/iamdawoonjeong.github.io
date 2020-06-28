---
layout: single
title: "[JAVA] 제네릭(Generic) VS 비제네릭(non-Generic)"
date: 2020-06-28 13:55:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- JAVA
- generic
- non-generic
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-generic-vs-non-generic/"
---
# Generic VS non-Generic

### Generic : 매개변수화된 타입
1. 자바 컬렉션 프레임워크의 클래스를 선언할 때 <>을 이용
2. List<Integer> 전체를 파라미터화된 List 라고 함  
3. <Integer>를 Integer 타입 파라미터(Type Parameter)라고 함
4. 파라미터화된 타입(parameterized type)이란, 꺽쇠 괄호 안에서 선언한 타입으로만 입출력하도록 제한한 타입임으로 캐스팅은 하지 않음
5. 꺽쇠 괄호안에 들어 갈 수 있는 타입에 대한 제한 사항을 통틀어서 Generics라고 함   
6. 캐스팅 하지 않고도 클래스를 쓸수 있게 해주는 기능

### 코드 재사용
- Generic : 메소드 / 클래스 / 인터페이스를 한 번만 작성하고 모든 유형에 사용 해야 함
- non-Generic : 필요할 때마다 코드를 반복해서 작성


### 형식 안전성
- 제네릭은 런타임보다 컴파일 타임에 오류를 표시[^1]

![java-inheritance]({{ site.baseurl }}/assets/images/posts/2020/java-inheritance.svg)

### 예
#### 개별 유형 캐스팅이 필요한 경우
- non-Generic : 학생의 이름을 저장하는 ArrayList를 만들고 실수로 프로그래머가 문자열 대신 정수 개체를 추가하는 경우 컴파일러에서 허용-> 이 데이터를 ArrayList에서 검색하면 런타임에 제네릭이 아닌 ArrayList에 대한 문제가 발생


```java
// A Simple Java program to demonstrate that NOT using
// generics can cause run time exceptions

import java.util.*;

class Test {
    public static void main(String[] args)
    {
        // Creating an ArrayList without any type specified
        ArrayList al = new ArrayList();

        al.add("Sachin");
        al.add("Rahul");
        al.add(10); // Compiler allows this

        String s1 = (String)al.get(0);
        String s2 = (String)al.get(1);

        try {
            // Causes Runtime Exception
            String s3 = (String)al.get(2);
        }
        catch (Exception e) {
            System.out.println("Exception: " + e);
        }
    }
}
```


output


```java
Exception:
 java.lang.ClassCastException:
 java.lang.Integer cannot be cast to java.lang.String
```


- Generic : 제네릭으로 만든 경우 String 개체 만 사용하고 다른 경우에는 컴파일 시간 오류가 발생


```java
// Using generics converts run time exceptions into
// compile time errors

import java.util.*;

class Test {
    public static void main(String[] args)
    {
        // Creating an ArrayList with String specified
        ArrayList<String> al = new ArrayList<String>();

        al.add("Sachin");
        al.add("Rahul");

        // Now Compiler doesn't allow this
        al.add(10);

        String s1 = al.get(0);
        String s2 = al.get(1);
        String s3 = al.get(2);
    }
}

```


output
```java
15: error: no suitable method found for add(int)
        al.add(10);
```


#### 개별 유형 캐스팅이 필요하지 않은 경우
- non-Generic : 데이터가 ArrayList에서 검색 될 때마다 매번 유형 변환 해야 함. 즉, 모든 검색 작업에서 타입 캐스팅 필요


```java
// A Simple Java program to demonstrate that
// type casting is needed everytime in Non-Generic

import java.util.*;

class Test {
    public static void main(String[] args)
    {
        // Creating an ArrayList without any type specified
        ArrayList al = new ArrayList();

        al.add("Sachin");
        al.add("Rahul");

        // For every retrieval,
        // it needs to be casted to String for use
        String s1 = (String)al.get(0);
        String s2 = (String)al.get(1);
    }
}
```


- generic : 리스트가 문자열 데이터 만 보유한다는 것을 이미 알고있는 경우, String 객체 만 가져오고 검색하는 동안 String 객체 만 반환. 따라서 개별 유형 캐스팅이 필요 없음.


```java
// A Simple Java program to demonstrate that
// type casting is not needed in Generic

import java.util.*;

class Test {
    public static void main(String[] args)
    {
        // Creating an ArrayList with String specified
        ArrayList<String> al = new ArrayList<String>();

        al.add("Sachin");
        al.add("Rahul");

        // Retrieval can be easily
        // without the trouble of casting
        String s1 = al.get(0);
        String s2 = al.get(1);
    }
}
```

### non-Generic Collection VS Generic Collection 

| 기준 | NON-GENERIC COLLECTION	| GENERIC COLLECTION |
|:--------:|:--------|:--------|
| Syntax | ArrayList list = new ArrayList();| ArrayList<T> list = new ArrayList<T>();|
| Type-safety	| 모든데이터보유. 안전하지는 않음| 정의 된 유형의 데이터 만 보유. 따라서 안전|
| Type casting	| 검색 할 때마다 개별 유형 캐스팅을 수행 | 타입 캐스팅이 필요없음 |
| Compile-Time Checking	| runtime시 안전성 확인 | Compile-time에 형식 안전성을 확인|

---
#### referencs
<https://www.geeksforgeeks.org/non-generic-vs-generic-collection-in-java/>  
<https://www.javatpoint.com/generics-in-java>  
<https://code.snipcademy.com/tutorials/java/generics/inheritance>


---
#### 참고
[^1]: 런타임에 코드가 실패하는 것보다 컴파일 타임에 코드의 문제를 아는 것이 항상 좋음
