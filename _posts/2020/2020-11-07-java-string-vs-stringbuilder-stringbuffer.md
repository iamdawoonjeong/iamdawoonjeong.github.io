---
layout: single
title: "[JAVA] String VS StringBuilder VS StringBuffer"
date: 2020-11-07 23:58:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- string
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-string-vs-stringbuilder-vs-stringbuffer/"
---
# String VS StringBuilder VS StringBuffer

### 소스로 비교해보기

- example

```java
public static void main(String[] args) {
    String s1 = "hello";
    concat1(s1);  // s1 is not changed
    System.out.println("String: " + s1);

    StringBuilder s2 = new StringBuilder("hello");
    concat2(s2); // s2 is changed
    System.out.println("StringBuilder: " + s2);

    StringBuffer s3 = new StringBuffer("hello");
    concat3(s3); // s3 is changed
    System.out.println("StringBuffer: " + s3);
}

// Concatenates to String
public static void concat1(String s1) {
    s1 = s1 + "world";
}

// Concatenates to StringBuilder
public static void concat2(StringBuilder s2) {
    s2.append("world");
}

// Concatenates to StringBuffer
public static void concat3(StringBuffer s3) {
    s3.append("world");
}
```

- output

```java
String: hello
StringBuilder: helloworld
StringBuffer: helloworld
```


#### (Concat1) **String  : immutable, synchronization**
- main ()에서 전달 된 문자열은 변경되지 않음.
- **String이 변경 불가능**
- **string의 값을 변경하면 다른 객체가 생성되고 concat1 ()의 s1은 새 문자열의 참조를 저장**
- main () 및 cocat1 ()의 s1 참조는 다른 문자열을 참조

#### (Concat2) **StringBuilder : mutable , Asynchronous**
- 문자열의 실제 값 (main)을 변경하는 s2.append("world")를 수행
- **StringBuilder가 변경 가능 하므로 값이 변경 된다는 단순한 사실**

#### (Concat3) **StringBuffer : mutable, synchronization**
- **StringBuffer는 StringBuffer가 스레드로부터 안전하다는 한 가지 차이점을 제외하면 StringBuilder와 유사**
- 즉, 여러 스레드가 아무런 문제없이 사용가능
- 스레드 안전성은 성능 저하를 가져옴

#### StringBuilder > StringBuffer > String


### 사용
- 문자열이 프로그램 전체에서 일정하게 유지되는 경우 String 개체는 변경할 수 없으므로 String 클래스 개체를 사용
- 문자열이 변경 될 수 있고 (예 : 문자열 생성시 많은 논리 및 작업) 단일 스레드에서만 액세스 할 수있는 경우 StringBuilder를 사용하는 것으로 충분
- 문자열이 변경 될 수 있고 여러 스레드에서 액세스 될 경우 StringBuffer가 동기식이므로 스레드 안전성이 있으므로 StringBuffer를 사용하

---
#### References
<https://www.geeksforgeeks.org/string-vs-stringbuilder-vs-stringbuffer-in-java/>
