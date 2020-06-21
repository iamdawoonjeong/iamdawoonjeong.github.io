---
layout: single
title: "[JAVA] Class와 Object"
date: 2020-06-21 14:30:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- JAVA
- oop
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-class-object/"
---
# Class와 Object

## Class
클래스는 객체를 생성하는데 사용되는 사용자 정의의 청사진(blue print), 설계도라 함  

### 클래스 속성
- 멤버 변수 (member variable), 멤버 필드 (member field), 필드 (field) : 메소드 밖에서 선언된 변수


```java
class <class_name>{  
    field;  
    method;  
}  
```

![java-class-in-java]({{ site.baseurl }}/assets/images/posts/2020/java-class-in-java.png)

## Object
- 상태,속성 : 객체의 변수
- 동작 : 객체의 메소드
- 동일성 : 객체에 고유한 이름 부여하고 한 객체가 다른 객체와 상호 작용

### 객체 선언, 인스턴스 (클래스 인스턴스화)
- 클래스의 객체가 생성되면 클래스가 인스터스화(메모리에 올리는 과정) 되었다고 함
- 모든 인스턴스는 클래스의 속성과 동작을 공유
- 속성의 값은 객체마다 고유  

#### 예제1)  


```java
클래스명 참조변수명; // 객체를 다루기위한 참조변수 선언   
참조변수명 = new 클래스명(); //객체생성 후 생성된 객체의 주소를 참조변수에 저장

Test t;
t = new Test();

Test t = new Test();  // Test()생성자를 호출  
```


#### 예제2) Object and Class Example: main within the class


```java
//Java Program to illustrate how to define a class and fields  
//Defining a Student class.
class Student{  
    //defining fields  
    int id;//field or data member or instance variable  
    String name;  

    //creating main method inside the Student class  
    public static void main(String args[]){  

       //Creating an object or instance  
       Student s1=new Student();//creating an object of Student  

      //Printing values of the object  
      System.out.println(s1.id);//accessing member through reference variable  
      System.out.println(s1.name);
    }  
}  
```

### 객체의 구성요소 - 변수, 메소드

## 변수 (객체의 속성)

### 변수의 종류
#### 클래스 변수 (=공유변수 shared variable)
- **멤버변수 중  static 이 붙은 것**
- 클래스 로딩될때 생성(클래스 메모리가 올라갈 때 자동적으로 생성)
- 인스턴스생성 없이 클래스이름.클래스변수명 으로 접근
- 모든 인스턴스가 하나의 저장공간을 공유하므로 항상 공통된 값 갖음
- 인스턴스 생성시 같은 값을 유지해야하는 경우 static 붙여서 선언

#### 인스턴스 변수
- **멤버변수 중 static 이 붙지 않은 것**
- 인스턴스 생성시 생성, 참조변수 없을 때 가비지 컬렉터에 의해 자동 제거됨
- 인스턴스 생성 후, 참조변수.인스턴스변수명 으로 접근
- 인스턴스가 생성될 때마다 생성되므로 인스터스마다 각기 다른 값 유지

#### 지역 변수
- 메스드내 선언, 메스드의 종료와 함께 소멸


## 메서드 (객체의 기능)
- 객체의 행위, 기능
- 자바의 메서드느 반드시 클래스 안에 정의되어야 함
- 반복적인 코드 줄이고, 코드의 관리가 용이

### 메서드 종류
#### 클래스 메서드 (static 메서드)
- 객체생성없이 클래스이름.메서드이름 으로 호출
- static 메서드내 인스턴스 변수 사용불가

#### 인스턴스 메서드
- 인스턴스 생성 후, 참조변수.메서드이름() 으로 호출
- 메서드내 인스턴스 변수 사용가능  

### static VS non-static
- static에서 > static을 호출 가능
- **static에서 > non-static 호출 불 가능**
- non-static 에서 > non-static 호출 가능
- **non-static 에서 > static 호출 가능**


## 생성자 constructer
- 새 객체를 초기화 하는데 사용
- 모양은 메서드와 비슷
- 클래스와 이름만 같고 리턴 타입이 없음
- 객체가 생성될때 한번 호출


```java
Test t = new Test();  
```
1. 연산자 new에 의해서 heap에 Test 클래스의 인스턴스 생성
2. 생성자 Test()가 호출되어 수행
3. 연산자 new의 결과로 생성된 Test인스턴스 주소가 반환되어 참조변수 t에 저장


### 기본 생성자
- 매개변수가 없는 생성자
- 모든 클래스에는 하나 이상의 생성자가 있어야 함
- 객체를 생성한 다음 객체의 레퍼런스를 이용하여 메서드를 호출


---
#### references
<https://www.geeksforgeeks.org/classes-objects-java/>  
<https://www.javatpoint.com/object-and-class-in-java>  
<https://www.javatpoint.com/difference-between-object-and-class>  
<https://www.geeksforgeeks.org/constructors-in-java/?ref=lbp>  
<https://www.geeksforgeeks.org/methods-in-java/?ref=lbp>  
