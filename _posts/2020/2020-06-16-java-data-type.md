---
layout: single
title: "[JAVA] 데이터 타입, 명명규칙, API문서 작성"
date: 2020-06-16 21:53:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- JAVA
- datatype
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-data-type/"
---
# [JAVA] 데이터 타입, 명명규칙, API문서 작성

## 데이터 타입 (Data type)


![java-Data-types-in-Java]({{ site.baseurl }}/assets/images/posts/2020/java-Data-types-in-Java.jpg)


### 기본타입 (Primitive data type)
- byte : 1byte = 8bit
- short : 2byte
- int  : 4byte
- long : 8byte
- float : 4byte
- double  : 8byte
- boolean : 2byte
- char : 1byte


### 참조 타입 (Reference type)
- 기본 타입 외의 모든 타입
- 객체의 주소를 저장  
- API, class, interface, array, enum, User define (사용자 정의)


#### 랩퍼클래스 (wrapper class)
- 기본형을 클래스로 정의 한 것
- Wrapper Class를 통해서 기본타입과 참조타입간 변화하려고 할 때 사용

##### primitive data type - wrapper class
- boolean - Boolean
- byte - Byte
- char - Char
- short - Short
- int - Int
- long - Long
- float - Float
- double - Double

```
//wrapper class 사용 예제
Integer it = new Integer(5);
int a= it.intValue();

String s= “12345”;
int b = Integer.parseInt(s)
```

```
//boxing
int a = 10;
integer I = new integer(a);

//unboxing
integer I = 10;
int a=I;
```

## 자바 명명법 (Naming convention)
#### 파스칼
- 대문자로 시작
- 클래스, 인터페이스, 생성자
- 각 단어가 시작하는 부분 대문자로 표시, 나머지는 소문자로 표시
- NameOfDesk , MyNameIs

#### 카멜
- 소문자로 시작하고 새로운 단어에서 대문자를 사용
- 메서드, 멤버필드, AWT, SWING 등 과 같은 화면 관련
- getName(), setName(), name, kingOfKing

#### 헝가리안
- AWT,SWING등과 같은 화면 관련 (헝가리안 보단 카멜 방식 권장)
- 비트, 라벨, 텍스트 필드와 같이 화면(GUI)에 관련된 것은 btnAdress, IbName, txtName

#### 전체 대문자
-  상수[^1] : PI, E와 같이 변하지 않는 값

#### 전체 소문자
- 패키지(package) : java.lang, java.util, java.sql

## API 문서
- javadoc 생성: 도스창에서 해당 java파일이 있는 경로지정
- javadoc : use private author

### Javadoc에서 사용되는 파라미터
- @author : 개발자
- @exception : 메소드에서의 예외 확인
- @param : 메소드의 매개변수, 아규먼트
- @return : 메소드의 반환값, 리턴 내용
- @see : 다른주제에 관한 링크지정, 추가 또는 관련 내용 참고
- @serial : 직렬화 필드
- @since : 릴리즈 기록, 언제부터 사용했는가
- @throws : 메소드에서의 예외
- @version : 클래스의 버전


---
#### references
<https://www.geeksforgeeks.org/data-types-in-java/>  
<https://www.geeksforgeeks.org/wrapper-classes-java/>  


---
#### 각주
[^1]:  Math.PI, Math.E…상수 항상 일정한 값을 유지하는 데이터, static final 상수로 선언된 값
