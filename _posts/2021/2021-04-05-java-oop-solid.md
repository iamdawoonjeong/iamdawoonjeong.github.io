---
layout: single
title: "[JAVA] OOP 5대원리 : SOLID (객체 지향 설계)"
date: 2021-04-05 22:30:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- java
- oop
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-oop-solid/"
---
# OOP 5대원리  : SOLID (객체 지향 설계)

### SRP (The Single Responsibility Principle)
- **한 클래스는 하나의 책임만 가져야 한다**
- 한 클래스는 하나의 목적에 맞도록만 짜라
- 하나의 책임원리->응집도 관력

### OCP(The Open-Closed Principle)
- **소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다**
- 개방 폐쇠의 원리->엔티티,상속(부모 변경 지양)
- A-->B (A를 변경하지 않고 B를 변경)
- 객체 지향 프로그램은 이 방법을 따르는게 좋다라는 원리 

### LSP (The Liskov Substitution Principle)
- **프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다**
- 부모의 이름으로 자식을 써라
- 리스코프 교체원리
- 다형성 관련(부모로 자식을 사용-->인터페이스 사용권장)

### DIP(The Depend Inversion Principle)
- **프로그래머는 “추상화에 의존해야지, 구체화에 의존하면 안된다”**
- 의존성 주입은 이 원칙을 따르는 방법 중 하나다
- 의존의 대상을 추상 클래스나 인터페이스 권장

### ISP (The Interface Segregation Principle)
- **특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다**
- 인터페이스 격리 원칙
- 필요한 메서드만 갖는 인터페이스를 구현하라
- SRP와 유사

----
#### references
<https://ko.wikipedia.org/wiki/SOLID_(%EA%B0%9D%EC%B2%B4_%EC%A7%80%ED%96%A5_%EC%84%A4%EA%B3%84)>
<https://www.geeksforgeeks.org/solid-principle-in-programming-understand-with-real-life-examples/>
