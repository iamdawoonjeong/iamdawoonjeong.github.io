---
layout: single
title: "[JAVA] 배열 Array, 배열의 복사 (deep copy, shallow copy)"
date: 2020-06-22 21:03:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- JAVA
- array
- deepCopy
- shallowCopy
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-array/"
---

# Array, 배열의 복사 (deep copy, shallow copy)

## 배열의 선언
- 선언 : 스택[^1]영역에만 올라감

```java
int [] arr ;  
```

- 초기화 : 메모리(힙 영역) 할당

```java
arr = new int[5];  
```

- 선언 - 초기화

```java
int [] arr = new int[5];  
```
![java-Blank-Diagram-Page-1-10]({{ site.baseurl }}/assets/images/posts/2020/java-Blank-Diagram-Page-1-10.jpeg)

## 배열의 복사
- 배열은 참조 타입
- 배열의 값은 기본 타입

### shallow copy =  reference assignment(참조에 의한 대입)
- 2차원 배열의 clone()

![java-Blank-Diagram-Page-1-12]({{ site.baseurl }}/assets/images/posts/2020/java-Blank-Diagram-Page-1-12.jpeg)

```java
int a[] = {1, 8, 3};

// a[] 와 같은 사이즈로 b[] 배열 생성
int b[] = new int[a.length];

// b는 a와 같은 주소를 참조하게 됨
b = a;     

// b의 값이 변경 될 경우 a가 영향을 받게 됨
b[0]++;
```

output

```java
//a[]의 값
2 8 3

//b[]의 값  
2 8 3
```


### deep copy= value assignment(값에 의한 대입)
- 1차원 배열의 clone()
- System.arraycopy() : 일대일 값 복사

![java-Blank-Diagram-Page-1-11]({{ site.baseurl }}/assets/images/posts/2020/java-Blank-Diagram-Page-1-11.jpeg)

```java
int a[] = {1, 8, 3};

// a[] 에서 b[]로 clone (새로운 object 생성)  
int b[] = a.clone();

// b[]의 값이 변할 경우 a[]값은 변하지 않음
b[0]++;


// a[] 와 같은 사이즈로 c[] 배열 생성
int c[] = new int[a.length];

// a[] 에서 b[]를 copy  
System.arraycopy(a, 0, c, 0, 3);

// c[]의 값이 변할 경우 a[]값은 변하지 않음
c[0]++;

```

output
```java
//Contents of a[]
1 8 3

//Contents of b[]
2 8 3

//Contents of c[]
2 8 3
```


---
#### references
<https://www.geeksforgeeks.org/arrays-in-java/>  
<https://www.geeksforgeeks.org/system-arraycopy-in-java/>  


---
#### 각주
[^1]:이름을 보관하는 공간
