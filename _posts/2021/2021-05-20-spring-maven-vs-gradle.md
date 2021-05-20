---
layout: single
title: "[Spring] Maven VS Gradle 개념, 비교"
date: 2021-05-20 22:35:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Spring
tags:
- JAVA
- Maven
- Gradle
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/spring-maven-vs-gradle/"
---
빌드 자동화 도구로 maven 과 gradle 대표적인다.  
오랫동안 maven이 대세였다면 최근 몇년간 gradle로 추세가 변하고 있다고 한다.  
그러나 난 아직도 실무에서 써본적이 없다. 그래서 최근에 개인 프로젝트를 진행하면서 gradle을 써보았는데, 복잡한 maven과 달리 생각이상으로 편하다.  
환경설정이 헤매지 않고 이리도 쉬운거였다니..?  
build.gradle에 작성하는데, 이게 매우 쉽고 편하다보니 pom.xml을 작성할 생각하면 머리가 아플 지경이다.  
실무환경도 어서 한번 gradle을 만나보고 싶다.

# Maven VS Gradle

## Maven
- **maven 프로젝트 빌드/관리를 위한 모듈**
- maven은 **자바 빌드 도구**로서 Apache Ant를 대안으로 나옴
- 프로젝트 객체 모델(POM)의 개념을 기반으로 Maven은 중앙 정보에서 프로젝트의 빌드,보고 및 문서를 관리

#### 특징 
- 빌드도구(자원을 하나로 합치는데 집둘하는 애플리케이션) /ant(앤트)도 있음
- 컴파일,테스트,배포를 쉽게 해줌
- WAR나 JAR파일로 실행가능한 상태로 배포
- 복잡한 app이라면 Maven이나 Ant같은 빌드도구를 이용해 짧은 시간에 빌드를 만들면 됨
- 특히 maven은 규칙만 따르면 됨
- 앤트는 maven과 같은 규칙(디렉터리 구조등)은 없어서 유연하다는 장점이 있지만 표준화 되지않기 때문에 관리 해야 함
- 의존성 관리 용이
- 기본 규약 제공
- 유용한 여러 플러그인 
- maven 소프트웨어 도구는 자바 프로젝트를 위해 이러한 디렉터리 구조를 자동으로 생성
- C#, Ruby, Scala 등과 같은 다른 프로그래밍 프로젝트에도 사용


## Gradle
- **오픈 소스 빌드 자동화 도구**

#### 특징
- 구조화 된 build프레임워크 (구조의 전환이 가능)
- Maven, Ivy등의 기존 저장소 인프라 또는 pom.xml 파일과 ivy.xml 파일에 대한 migration의 편이성 제공
- 멀티 프로젝트 빌드 지원
- 의존성 관리의 다양한 방법 제공
- Build script를 xml이 아닌 Groovy 기반의 DSL(Domain Specific Language)[^1]을 사용
- 기존 Build를 구성하기 위한 풍부한 도메인 모델 제공
- Gradle 설치 없이 Gradle Wrapper를 이용하여 빌드 지원
- xml의 구조적인 틀을 벗어나 코딩에 의한 간결한 정의가 가능
- build.gradle 파일에 빌드정보를 정의하여 프로젝트에서 사용하는 환경 설정, 빌드방법, 라이브러리 정보 등을 기술함으로서 빌드 및 프로젝트의 관리환경을 구성
- Google은 Android 용 공식 빌드 도구로 Gradle을 선택
- Java, Scala, Android, C / C ++ 및 Groovy를 포함한 많은 언어 및 플랫폼에서 빌딩 자동화

## Gradle VS Maven

| Gradle  																	    | Maven 																 |
|:------------------------------------------------------------------------------|:-----------------------------------------------------------------------|
| Groovy 기반 DSL (도메인 특정 언어)을 사용하는 빌드 자동화 시스템					| 주로 자바 프로젝트에 사용되는 소프트웨어 프로젝트 관리 시스템	  			 |
| 프로젝트 구성을 선언하는데 XML 파일을 사용안함										| 프로젝트, 종속성, 빌드 순서 및 필수 플러그인을 선언하기 위해 XML 파일을 사용	 |
| 작업을 수행하는 작업 종속성의 그래프를 기반										| 고정 및 선형 모델의 단계를 기반											 |
| 주요 목표는 프로젝트에 기능을 추가하는 것							 				| 주요 목표는 프로젝트 단계와 관련											 |
| 입력 및 출력 작업을 추적하여 작업을 피하고 변경된 작업 만 실행,  더 빠른 성능을 제공 	| 빌드 캐시를 사용하지 않아 빌드 시간이 Gradle보다 느림 						 |
| 고도로 사용자 정의 > 광범위한 IDE 지원 사용자 지정 빌드를 제공		       			| 제한된 수의 매개 변수와 요구 사항이 있으므로 사용자 정의는 약간 복잡 			 |
| Java 컴파일을 방지																| 컴파일이 필수															 |



----
#### references
<https://maven.apache.org/what-is-maven.html>  
<https://docs.gradle.org/current/userguide/what_is_gradle.html>  
<https://www.egovframe.go.kr/wiki/doku.php?id=egovframework:dev3.6:dep:build_tool:gradle>  
<https://gradle.org/maven-vs-gradle/>  
<https://ko.wikipedia.org/wiki/IBATIS>  
<https://ko.wikipedia.org/wiki/%EB%A7%88%EC%9D%B4%EB%B0%94%ED%8B%B0%EC%8A%A4>  
<https://www.slideshare.net/jafarnesargi/java-bean>  
<https://ko.wikipedia.org/wiki/%EC%97%94%ED%84%B0%ED%94%84%EB%9D%BC%EC%9D%B4%EC%A6%88_%EC%9E%90%EB%B0%94%EB%B9%88%EC%A6%88>  
<https://www.javatpoint.com/gradle-vs-maven>  


-----
#### 주석
[^1]:특정한 도메인을 적용하는데 특화된 컴퓨터 언어
