---
layout: single
title: "[Spring] Spring VS Spring boot VS Spring MVC 개념 및 차이점"
date: 2021-05-24 00:10:00.000000000 +09:00
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
- spring mvc
- spring boot
- EJB
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/spring-spring_mvc-vs-spring_boot-vs-spring_mvc/"
---
요즘 spring boot가 스프링진영에서 제일 많이 쓰인다고 한다.  
듣기만 했지 이것 또한 실무에서 만나본 적이 없다. (생각보다 한 번 개발된 서비스는 쉽게 변하지 않는다.)  
최근에 개인 프로젝트를 진행하면서 사용하고 있는데 셋팅도 쉽고 여러모로 스프링 보다 편한부분이 많다.  
앞으로는 더 많이 쓰일 것 같다고 하니 잘 익혀두고 알아두면 좋을 스프링 부트  

# Spring VS Spring boot VS Spring MVC 개념 및 차이점

## Spring
- 오픈 소스 경량 프레임 워크
- 자바 개발자가 간단하고 안정적이며 확장 가능한 엔터프라이즈 애플리케이션을 빌드 할 수 있도록 함
- 비즈니스 개체를 관리하는 데 도움이되는 다양한 방법을 제공하는 데 중점을 둠  
- Java 데이터베이스 연결 (JDBC), JavaServer Pages (JSP) 및 Java Servlet과 같은 기존 Java 프레임 워크 및 API (Application Programming Interface)에 비해 웹 애플리케이션 개발이 훨씬 쉬워짐  
- AOP (Aspect-Oriented Programming), POJO (Plain Old Java Object) 및 DI (dependency injection)와 같은 다양한 새로운 기술을 사용하여 엔터프라이즈 애플리케이션을 개발
	- 스프링 AOP 같은 서브 프레임 워크라고도 층의 집합
- Spring 개체 관계형 매핑 (Spring ORM). Spring Web Flow 및 Spring Web MVC 등이 있음
	- 웹 응용 프로그램을 구성하는 동안 이러한 모듈을 별도로 사용 가능
	- 모듈은 웹 응용 프로그램에서 더 나은 기능을 제공하기 위해 함께 그룹화 가능

## Spring MVC
- Spring은 확장 가능한 애플리케이션을 만드는 데 널리 사용 되는 Spring MVC 프레임 워크를 제공
- Spring MVC 프레임 워크는 Model View, Controller라는 모듈의 분리를 가능하게하고 애플리케이션 통합을 원활하게 처리
- 개발자는 일반 Java 클래스를 사용하여 복잡한 응용 프로그램을 만들 수 있음
- 모델 객체는 맵을 사용하여 뷰와 컨트롤러간에 전달

##  Spring Boot
- Spring Boot는 기존의 스프링 프레임 워크 위에 구축 (스프링 프레임 워크 기반)
- 스프링의 모든 기능을 제공하면서도 스프링보다 사용하기 쉬움
- Spring Boot는 마이크로 서비스 기반 프레임 워크이며 매우 짧은 시간에 프로덕션 준비 애플리케이션을 만듦
- Spring Boot에서는 모든 것이 자동으로 구성됨
- 특정 기능을 활용하기 위해 적절한 구성을 사용하기 만
- Spring Boot는 REST API를 개발하려는 경우 매우 유용
- Spring Boot는 프로젝트를 war 또는 jar 파일로 변환하는 기능을 제공
- Tomcat의 인스턴스는 클라우드에서도 실행 가능
- 자주 사용하는 라이브러리가 미리 조합되어있음
- 복잡한 설정이 자동 처리됨
- 내장서버를 포함 (톰캣) 서버를 추가로 설치하지 않아도 바로 개발 가능
- 톰캣, 제티와 같은 WAS에 배포하지 않고도 실행할 수 있는 jar 파일로 웹어플리케이션 개발 가능

### Spring boot의 4계층
- Presentation Layer : 이름에서 알 수 있듯이 view (예 : front-end 부분)로 구성
- Data Access Layer : 데이터베이스에 대한 CRUD (create, retrieve, update, delete)
- Service Layer : 서비스 클래스로 구성되며 데이터 액세스 계층에서 제공하는 서비스를 사용
- Integration Layer : 웹별 웹 서비스 (인터넷을 통해 사용 가능한 모든 서비스 및 XML 메시징 시스템 사용)로 구성


|  spring 											        | spring boot			                                            | spring MVC														           |
|:----------------------------------------------------------|:------------------------------------------------------------------|:----------------------------------------------------------------------------|
| 엔터프라이즈 애플리케이션을 개발하는 오픈 소스 경량 프레임 워크	| REST API를 개발하는 데 널리 사용되는 기존의 스프링 프레임 워크 위에 빌드	| Model View이며 웹 애플리케이션 개발에 널리 사용되는 Controller 기반 웹 프레임 워크 |
| 의존성 주입 												| 자동 구성														    | 수동으로 빌드                                                                 |
| 명시 적으로 서버를 설정										| Tomcat 및 Jetty 등과 같은 임베디드 서버를 제공						|				                                                               |
| 실행 시 배치 디스크립터가 필요								| 배치 디스크립터에 대한 요구 사항은 없음 								| 배치 디스크립터가 필요                                                          |
| 개발자는 많은 코드를 작성								    | 코드 줄일 수 있음 , 개발 시간을 줄이고 생산성을 높임 					| 개발에 더 많은 시간이 걸림														 |
| 메모리 내 데이터베이스에 대한 지원을 제공하지 않음 				| H2와 같은 메모리 내 데이터베이스에 대한 지원을 제공						| 																				|
|															| Presentation Layer, Data Access Layer, Service Layer, Integration Layer  | Model, View, Controller, Front Controller								|



----
추가로 spring이전의 엔터프라이즈 프레임워크인 EJB에 대한 개념을 알아보겠다.  
아직도 오래된 프로젝트, 공공기관에서 간혹가다 만날 수 있으며, 나도 잠깐 만난적이 있다.

## EJB (Enterprise Java Beans)
- 엔터프라이즈 자바빈즈(Enterprise JavaBeans; EJB)는 기업환경의 시스템을 구현하기 위한 서버측 컴포넌트 모델
- 이제까지는 상속받으면 부모가 내꺼되고 해서 상속을 받고받고 하면 내가 없어짐 내가 상속으로 이미 결정됨 (EJB)
- 즉, EJB는 애플리케이션의 업무 로직을 가지고 있는 서버 애플리케이션
- EJB 사양은 Java EE의 자바 API 중 하나로, 주로 웹 시스템에서 JSP는 화면 로직을 처리하고, EJB는 업무 로직을 처리하는 역할
- 애플리케이션의 비즈니스 로직을 요약하는 서버 측 소프트웨어 구성 요소
- EJB 컨테이너는 컴퓨터 안정성, JSL (Java Servlet Lifecycle) 관리, 트랜잭션 절차 및 기타 웹 서비스를 포함한 웹 관련 소프트웨어 요소에 대한 런타임 환경을 제공
- EJB 응용 프로그램을 실행하려면 Jboss, Glassfish, Weblogic, Websphere 등과 같은 응용 프로그램 서버가 필요
    - Life Cycle Management, Object Pooling, Transaction Processing, Security 등을 수행


### EJB 세 가지 유형

#### Session Bean
- 세션 빈은 로컬, 원격 또는 웹 서비스 클라이언트에 의해 호출 될 수있는 비즈니스 로직을 포함
- Stateful 세션 빈 및
- Stateless 세션 빈

#### Message Driven Bean
- Session Bean과 마찬가지로 비즈니스 로직을 포함하고 있지만 메시지를 전달하여 호출

#### Entity Bean
- 데이터베이스에서 지속될 수있는 상태를 요약
- Bean Managed Persistence
- 컨테이너 관리 지속성

### 특징
- Java EE의 사양
- EJB 데이터 소스, JMS 리소스 및 JPA 리소스를 포함하여 컨테이너에 모든 것을 삽입 가능

----
#### references
<https://www.geeksforgeeks.org/difference-between-spring-and-spring-boot/?ref=rp>  
<https://www.geeksforgeeks.org/difference-between-spring-mvc-and-spring-boot/?ref=rp>  
<https://www.geeksforgeeks.org/difference-between-ejb-and-spring/?ref=rp>  
