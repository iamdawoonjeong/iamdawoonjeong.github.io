---
layout: single
title: "[JAVA] Foreach VS Iterator"
date: 2020-11-08 21:30:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- foreach
- iterator
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-foreach-vs-iterator/"
---
# foreach vs iterator 

## foreach
- **컬렉션의 항목을 순회하기 위한 것**
- ":" 인 in 이라고 읽음 

```java
// for-each를 사용하여 컬렉션 'c'반복 
for (Element e: c)
   System.out.println(e);
```

## Iterator 
- 컬렉션 프레임 워크에서 컬렉션을 탐색하고 컬렉션의 항목에 대한 순차적 액세스를 위해 제공하는 인터페이스
   
```java
// iterator를 사용하여 컬렉션 'c' 반복 
for (Iterator i = c.iterator(); i.hasNext(); ) 
   System.out.println(i.next());
```

## 사용 
- 컬렉션을 **수정해야하는 경우 Iterator를 사용**
- **중첩 된 for loop 사용해야할 때는 for-each 루프를 사용** 하는 것이 더 좋음

```java
Exception in thread "main" java.util.NoSuchElementException
    at java.util.LinkedList$ListItr.next(LinkedList.java:888)
    at Main.main(Main.java:29)
```

## 결론
- **iterator, for-each 은 임의 액세스가 없는 컬렉션에 대한 단순 for 루프보다 빠름** 
- 임의 액세스를 허용하는 컬렉션에서는 for-each / for / iterator 에 대한 성능 변화가 없음 


##  for vs foreach

###  for  
- 특정 조건이 성립할 때 까지 반복

### foreach 
- 특정 열거 인터페이스가 열거된 요소를 하나씩 가져옴
- 컬렉션을 다루는 명령이나 API를 적극적으로 사용하는 것이 좋음
- 컬렉션 수만큼만 반복하므로 증감을 고려하지 않아도 되어서 안전성이 높음

---
#### References
<https://www.geeksforgeeks.org/iterator-vs-foreach-in-java/>