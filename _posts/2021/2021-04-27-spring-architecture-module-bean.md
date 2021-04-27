---
layout: single
title: "[Spring] 스프링 모듈 구성"
date: 2021-04-27 20:55:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Spring
tags:
- JAVA
- spring
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/spring-module/"
---
- 실행에 필요한 클래스를 스프링이 준비
- 인스턴스를 준비하는 역할은 스프링이 하기에 인스턴스 준비코드를 작성할 필요 없음
	- new를 사용해 인스턴스를 생성하거나 JNDI로 인스턴스를 취득하는 코드를 만들지 않아도 됨 =>클래스 결합이 약해져 의존관계가 약해짐
- 변경이 용이하고, 테스트가 간편하고, 컴포넌트 재사용성이 높은 유연한 애플리케이션을 만드는것이 가능함

## 모듈 구성 
- 필요할 때 필요한 모듈만 이용 할 수 있기 때문에 경량컨테이너

![spring_spring-overview.png]({{ site.baseurl }}/assets/images/posts/2021/spring_spring-overview.png)

### Core Container
- Core, Beans
	- 스프링의 핵심/기본 모듈
	- Bean 컨테이너 관련기능 제공
	-  DI, IoC 제공
	-  `BeanFactory` 구현
- Context 
	- Beans 모듈에서 기능을 상속
	- 국제화(예 : 리소스 번들 사용)나 JAVA E 가 제공하는 JNDI, EJB, JMX등을 지원
- Expression Language
	- 런타임에 개체 그래프를 쿼리하고 조작 할 수 있는 강력한 표현 언어를 제공
	- 목록 프로젝션 및 선택은 물론 공통 목록 집계도 지원

### AOP및 Aspects
- AOP : 구현하기 위하여 메소드 인터셉터 및 포인트 컷을 정의
- aspects : 별도의 aspects 모듈은 AspectJ와의 통합을 제공
- Instrumentation : 특정 애플리케이션 서버에서 사용할 클래스 계측 지원 및 클래스 로더 구현을 제공
	- spring-instrument-tomcat 모듈에는 Spring의 Tomcat 용 계측 에이전트가 포함

### Messaging
- 메시징 기반 애플리케이션의 기반 역할
- 메시지를 메소드에 매핑하기위한 주석 세트를 포함

### Data Access / Integration
- JDBC : JDBC 추상계층 기능을 제공하는 모듈. JDBC에 의한 데이터베이스 액세스를 지원
- ORM : Object Relational Mapping 기능 제공하는 모듈. ORM API(JPA, Hibernate, iBatis, JDO)를 지원
- OXM : JAXB, Castor, XMLBeans, JiBX, XStream에 대한 객체/XML매핑 구현을 지원하는 추상화 계층을 제공
- JMS : Java Messaging Service 모듈은 메시지를 생산하고 소비하는 기능을 포함(Spring Framework 4.1부터 spring-messaging모듈 과의 통합을 제공)
- Transaction : 특수 인터페이스를 구현하는 클래스와 모든 POJO의 클래스에 대한 프로그래밍 및 선언적 트랜잭션 관리를 지원

### Web
- Websocket
- Servlet : 웹 애플리케이션을 위한 **MVC 프레임 워크 기능 제공**
	- 웹 애플리케이션을위한 REST 웹 서비스의 구현
	- Spring의 MVC 프레임 워크는 도메인 모델 코드와 웹 양식 사이의 명확한 분리를 제공
	- Spring Framework의 다른 모든 기능과 통합
- Web : 웹 애플리케이션 이용에 편리한 기능을 제공 
	- 멀티 파트 파일 업로드 기능 및 Servlet 리스너 및 웹 지향 애플리케이션 컨텍스트를 사용하는 IoC 컨테이너 초기화와 같은 기본적인 웹 지향 통합 기능을 제공
	- HTTP 클라이언트와 Spring의 원격 지원의 웹 관련 부분도 포함
- Portlet : 포틀릿 환경 미러 서블릿 기반의 기능에 사용될 MVC 구현 제공

### Test
- JUnit , TestNG를 사용한 테스트 지원
- mock 객체 지원


## BeanFactory와 ApplicationContext

![spring_beanfactory-vs-applicationcontext.jpg]({{ site.baseurl }}/assets/images/posts/2021/spring_beanfactory-vs-applicationcontext.jpg)

### BeanFactory 인터페이스
- 의존관계 주입 컨테이너에서 핵심인 BeanFactory가 하는 역할은 Bean의 생성과 관리
- `BeanFactory`는 스프링 컨테이너에 액세스하기위한 루트 인터페이스
- Spring 컨테이너에 액세스하기 위해이 BeanFactory 인터페이스와 하위 인터페이스를 사용하여 Spring의 종속성 주입 기능을 사용
- 기능 : 빈 인스턴스화 / 연결
- 일반적으로 구현은 지연 로딩을 사용
	- 즉, Bean은 getBean () 메소드를 통해 직접 호출 할 때만 인스턴스화 됨

### ApplicationContext 인터페이스
- `ApplicationContex`t는 애플리케이션에 구성 정보를 제공하기위한 스프링 애플리케이션 내의 중앙 인터페이스
- `BeanFactory` 인터페이스를 구현 : **ApplicationContext 는 BeanFactory 의 모든 기능과 그 이상을 포함**
- 주요 기능은 대규모 비즈니스 응용 프로그램의 생성을 지원



----
#### references
<https://docs.spring.io/spring-framework/docs/3.0.x/spring-framework-reference/html/overview.html>  
<https://docs.spring.io/spring-framework/docs/4.3.13.RELEASE/spring-framework-reference/html/overview.html>  
<https://www.geeksforgeeks.org/introduction-to-spring-framework/>  
<https://www.javaguides.net/2019/01/beanfactory-vs-applicationcontext-in-spring.html>  
