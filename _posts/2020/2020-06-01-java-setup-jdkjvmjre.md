---
layout: single
title: "[JAVA] JAVA 설치 및 JDK, JVM, JRE"
date: 2020-06-01 23:49:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- JAVA
- JDK
- JVM
- JRE
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-setup-jdkjvmjre/"
---
윈도우 자바 설치의 핵심(?)은 환경변수 설정이고, 맥은 설치하고나서 안해줬던 것 같은데, 찾아보니 맥도 해주는 거다.  
왜 난 기억이 나지 않지만 설정이 되어있는건가.  
기본 중에 기본인, 자바 책을 사면 맨 앞 챕터에서 만날 수 있는 자바설치방법과 jdk, jvm 그리고 jre까지 간략하게 훝어보기

<!--excerpt_separator-->


## 자바 설치, 환경변수 설정

### 자바 설치
#### 1. Oracel 홈페이지에서 JAVA를 다운받기
<https://www.oracle.com/java/>  

#### 2. 자바 설치는 NEXT 계속

---


### Windows 환경변수 설정
#### - 내컴퓨터에서 오른쪽버튼 클릭 / 제어판 > 속성 > 고급시스템 설정 > [고급] TAB > "환경변수" 클릭

```
- 변수이름 : JAVA_HOME  
- 변수값 : C:\Program Files\Java\jdk-13.0.2\ (본인 컴퓨터에 자바설치한 경로)  
톰캣과 같은 웹 컨테이너는 JDK설치경로를 필요로 하는데 이때 사용하는 환경변수의 이름
```

```
- 변수이름 : PATH (라는 변수이름 찾아서 편집)  
- 변수값 : %JAVA_HOME%\bin;  (오라클 설치경로 앞에 붙여주기)  
운영체제가 명령어를 실행하면서 해당 명령어에 맞는 실행파일을 찾아가는 순서 명시한 환경변수
```

---
### MAC OS 환경변수 설정

```
# bash_profile 편집
vi .bash_profile

# bash_profile에 아래와 같이 두개의 변수 추가
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.7.0_80.jdk/Contents/Home
export PATH=$PATH:$JAVA_HOME/bin

# 수정된 내용 적용
sourc .bash_profile
```


---
### 자바 설치 확인 및 환경변수 설정 확인
- 윈도우는 cmd창, 맥은 terminal 확인
- 환경변수가 제대로 설정 있다면 아무 위치에서다 명령어가 실행되어야 하며, 환경변수를 미설정시 자바 설치 경로로 이동해서 확인 가능  

```
java -version   

javac -version
```

##### 참고
- Javac     : 자바 컴파일러
- Java      : 자바 실행, 바이트 코드 인터프리터
- Javadoc   : 자바 API문서(도큐먼트) 생성기
- Jab       : 자바 디버거
- Javap     : 자바 디 어셈블러 (역 컴파일), Javap java.lang.Object/Javap java.lang.String
- Javaw     : GUI용 자바실행, 콘 솔에 출력을 보이지 않는 바이트 코드 인터프리터





## JDK, JRE, JVM

### JDK (Java Developmnet Kit) : 자바 개발도구
- JDK와 SDK는 같은 의미 (SDK(Software Development Kit)는  JDK의 이전)
- 자바 프로그램을 위한 기본 클래스나 컴파일, 실행, 배포 등 개발을 위한 전반적인 환경(도구)


### JRE (Java Runtime Environment) : 자바 런타임 환경, 자바 실행도구
- 자바를 사용하여 쉽게 구연할 수 있도록 한 클래스 라이브러리의 집합
- 사용자에 부담을 최소화하는 반면에 입출력, 화면구성, 이미지, 네트워크와 같은 복잡하지만 필요한 클래스들을 미리 구연하여 사용자가 쉽게 구연하도록 하는 API

### JVM  (Java Virtual Machine) 자바 가상 머신
- 자바 프로그램이 실행될 수 있도록 가상으로 CPU와 OS를 만듦
- 자바는 OS에 영향을 받지 않으므로 호환성이 좋음
- 컴파일 된 프로그램은 OS에 상관없이 실행 (플랫폼에 독립적)


![JDK_JRE_JVM_x]({{ site.baseurl }}/assets/images/posts/2020/java-JDK_JRE_JVM_x.jpg)


## 자바프로그램 실행
### 자바파일 직접 compile 후 실행
1. 컴파일 : javac 클래스이름.java
```  
   javac Example.java
```

2. 자바 실행 : java 클래스이름
```
   java Example
```

![JRE_JDK_JVM]({{ site.baseurl }}/assets/images/posts/2020/java-JRE_JDK_JVM.jpg)


### 자바파일 실행원리
1. JDK에서 Compile을 하면서 .class 가 생성 되면서 bytecode가 만들어짐
2. compile이 제대로 되었다면 bytecode는 JVM에서 실행되며 이때 native code로 컴파일 되면서 실행결과가 나옴   

![JRE_JDK_JVM_4]({{ site.baseurl }}/assets/images/posts/2020/java-JRE_JDK_JVM_4.jpg)

---
##### References
<https://neoitstory.blogspot.com/2014/06/java.html>  
<https://www.geeksforgeeks.org/differences-jdk-jre-jvm/>
