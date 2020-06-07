---
layout: single
title: "[JAVA] JVM 메모리"
date: 2020-06-07 13:54:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- JAVA
- JVM
- memory
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-jvm-memory/"
---

# JVM (Java Virtual Machine) 메모리

> Write Once Run Anywhere (WORA) -JAVA

한 번 작성 하면, 어디에서든지 실행 될 수 있다를 의미하는 이 표어는 자바의 특징이며,
이것을 가능하게 하는 것은 바로 JVM이 있기 때문이다.

![java-JvmSpec]({{ site.baseurl }}/assets/images/posts/2020/java-JvmSpec7.png)

## JVM 메모리 구조

### 메소드(Method) 영역
- **클래스 이름, 직계 상위 클래스 이름, 메소드 및 변수 정보** 등과 같은 모든 클래스 레벨 정보가 정적 변수를 포함하여 저장
- JVM 당 하나의 메소드 영역 만 있으며 공유 자원

### 힙(Heap) 영역
- **JVM 당 하나의 힙 영역**
- 모든 객체의 정보가 힙 영역에 저장
- 모든 클래스 인스턴스 및 배열에 할당
- new 키워드를 사용한 배열과, 객체가 힙 공간이 할당, 동일한 참조가 스택에 존재
- 공유 리소스
- 시스템 구성에 따라 고정 또는 동적 크기


### 스택(Stack) 영역
- 모든 스레드에 대해 JVM은 여기에 저장된 하나의 런타임 스택을 만듦
- 이 스택의 모든 블록을 메소드 레코드를 저장하는 활성화 레코드 / 스택 프레임이라고 함
- 해당 메소드의 모든 로컬 변수는 해당 프레임에 저장
- 스레드가 종료되면 런타임 스택이 JVM에 의해 파괴 됨
- 공유 리소스가 아님

### PC Registers
- 스레드의 현재 실행 명령의 주소를 저장
- 각 스레드에는 별도의 PC 레지스터가 존재

### 네이티브 메소드 스택 (Native Method Stack)
- 모든 스레드에 대해 별도의 네이티브 스택이 생성
- 기본 메소드 정보를 저장

---

<https://ko.wikipedia.org/wiki/%EC%9E%90%EB%B0%94_%EA%B0%80%EC%83%81_%EB%A8%B8%EC%8B%A0>    
<https://ko.wikipedia.org/wiki/Write_once,_run_anywhere>  
<https://www.geeksforgeeks.org/jvm-works-jvm-architecture/>   
<https://www.geeksforgeeks.org/java-memory-management/>
