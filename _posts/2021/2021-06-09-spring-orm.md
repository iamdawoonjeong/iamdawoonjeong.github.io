---
layout: single
title: "[Spring] ORM, JPA, hibernate, iBatis/MyBatis 개념 및 차이점"
date: 2021-06-09 22:37:00.000000000 +09:00
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
- hibernate
- mybatis
- orm
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/spring-spring-orm/"
---
ORM 기술도 트렌드가 변화하고있다. 한참동안은 MyBatis가 대세를 이루더니 요즘은 JPA+JPQL 이 대세라고 한다.  
MyBatis는 동적쿼리를 작성할 때 xml로 태그를 열고 닫아야 하는 귀찮은 부분이 분명 있었지만,   
SQL을 직접작성하다보니 쿼리를 볼 때 매우 직관적이고, Oracle의 내장함수를 이용할 수 있는 부분이 커다란 장점이였다.  
최근의 JPA+JPQL의 조합은 어떠한가. CRUD를 직접 작성하지 않아도 되고, DB가 바뀌어도 쿼리작성은 JPA의 몫이니 크게 신경쓰지 않아도 된다.  
그러나 JPA자체를 학습하는데는 또 다른 이해를 요구하는 일이다.   
그리고 사실 JPA는 ORM 기술의 명세일뿐 실제 사용하려면 Hibernater같은 프레임워크가 필요하니 또다른 학습이 늘어난다.  

무슨 기술이든 장단점은 존재하고 어떤 기술을 채택하여 사용할지를 결정하는 것 또한 프로그램에 큰 영향을 미치니  
무엇을 사용하는 것이 좋다라고 말하긴 보단 잘 선택해서 사용하기를..


# ORM이란?
- ORM의 표준 JPA와 JPA를 표준을 따르고 구현한 hibernate, iBatis/MyBatis
- ORM : JPA Hibernate, iBatis/MyBatis

## ORM (Object-relational mapping : 객체 관계 매핑)
- 자바객체와 데이터베이스 테이블간의 매핑처리
- 객체는 객체대로 설계
- 관계형 데이터베이스는 관계형 데이터베이스대로 설계
- ORM 프레임워크가 중간에서 매핑
- 대중적인 언어에는 대부분 ORM 기술이 존재
- 데이터베이스에 저장된 데이터와 개체를 매핑하는 것은 프로그래밍 전략입
- 데이터 생성, 데이터 조작 및 데이터 액세스를 단순화 함

### Java ORM Frameworks 종류
- Enterprise JavaBeans Entity Beans
- Java Data Objects
- Castor
- TopLink
- Spring DAO
- Hibernate

## JPA (Java Persistence API)
- 자바 진영의 ORM 기술 표준 (사양)
- JPA는 객체 지향 도메인 모델과 관계형 데이터베이스 시스템 간의 다리 역할
- JPA는 자체적으로 어떤 작업도 수행하지 않음(사양일 뿐)
- Hibernate, TopLink 및 iBatis와 같은 ORM 도구는 데이터 지속성을 위한 JPA 사양을 구현
- ORM 도구에서 다른 도구로 애플리케이션을 전환하려는 경우 쉽게 수행 가능
- javax.persistence 패키지에 정의
- 자바 지속성 쿼리 언어 데이터베이스 작업을 수행하는 객체 지향 쿼리 언어 (JPQL) 사용

### 동작 방법
- JAVA가 JDBC API에 명령을 내리는 것이라니라 JPA를 사용하면 JPA가 JDBC API를 사용해서 DB와 통신하고 SQL을 호출하고 반환
- 저장시 JPA가 Entity를 분석해서 SQL을 생성함
- 조회시 JPA가 SQL을 생성하여 SQL을 생성
- 패러다임 불일치 해결

### 장점
- 개발이 편리함 : 기본적인CRUD용 SQL을 직접 작성하지 않아도 됨
- 데이터베이스에 독립적 개발 가능 : JPA는 데이터베이스에 종속적이지 않아서 데이터베이스가 변경되더라도 JPA가 해당 데이터베이스에 맞는 쿼리 알아서 생성해줌
- 유지보수가 쉬움: 테이블 변경시 JPA의 엔티티만 수정하면 됨

### 단점
- 학습이 어려움
- 특정 데이터베이스의 함수를 사용하지 못함
- 테이블을 객체지향 설계가 필요

## Hibernate (하이버네이트)
- 2001 년 Gavin King이 만든 오픈 소스 영구 프레임 워크
- 데이터베이스와 상호 작용하는 Java 애플리케이션의 개발을 단순화하는 Java 프레임 워크
- 오픈 소스, 경량의 ORM (Object Relational Mapping) 도구
- 데이터 지속성을 위해 JPA (Java Persistence API) 사양을 구현(JPA 구현 중 하나 )
- 자바 객체와 데이터베이스 테이블사이의 매핑을 관리하려고 만들어진 도구 ORM
- 개체들의 도메인 객체가 있어야 하는데 단순한 POJO이고 각 객체는 데이터테이블과 간단하게 연결
- JDBC의 한계를 극복하는 데 사용
- org.hibernate 패키지에 정의 됨

### 동작방법
- Java Application내 Hibernate의 Configuration 파일(Hibernate.Properties)과 Hibernate XML Mapping 파일을 사용하여 데이터베이스에 대한 특정 작업을 수행하는 지속성 논리를 작성하여 특정 클래스의 객체(영속성 객체)를 만듦
- Hibernate Framework 내부의 SessionFactory, Session , Transaction 등과 같은 많은 객체를 사용하여 Java Application과 상호작용
- JDBC (Java Database Connectivity), JTA (Java Transaction API) 및 JNDI (Java Naming Directory Interface)와 같은 기존 Java API를 통해서 데이터베이스로 이동하여 지속성 논리를 수행하는 상호작용  
- 데이터베이스와 상호작용 (CRUD 지속성 논리를 수행)

### 장점
- 오픈 소스 및 경량 : LGPL 라이선스하에 오픈 소스이며 경량임
- 빠른 성능 : 최대 절전 프레임 워크에서 캐시가 내부적으로 사용되기 때문에 최대 절전 프레임 워크의 성능이 빠름
- 데이터베이스 독립 쿼리 : HQL (Hibernate Query Language)은 SQL의 객체 지향 버전데이터베이스 독립적 인 쿼리를 생성 > 특정 쿼리를 작성할 필요가 없음
- 자동 테이블 생성 : Hibernate 프레임 워크는 데이터베이스 테이블을 자동으로 생성하는 기능을 제공 > 데이터베이스에 수동으로 테이블을 만들 필요가 음
- 복잡한 조인 단순화 : 하이버 네이트 프레임 워크에서는 여러 테이블에서 데이터를 가져 오는 것이 쉬움
- 쿼리 통계 및 데이터베이스 상태 제공 :Hibernate는 쿼리 캐시를 지원하고 쿼리 및 데이터베이스 상태에 대한 통계를 제공


## MyBatis
- 오픈 소스, 경량의 지속성 프레임 워크
- 가장 간단한 지속성 프레임 워크

### iBatis
- iBatis는 SQL에 기반한 데이터베이스와 자바, 닷넷(.NET), 루비(Ruby) 등을 연결시켜 주는 역할을 하는 영속성 프레임워크(Persistence Framework)
- 연결은 프로그램의 소스코드에서 SQL 문장을 분리하여 별도의 XML 파일로 저장하고 이 둘을 서로 연결시켜주는 방식으로 작동
- iBatis는 사용자가 SQL 문장을 만들면 그에 적합한 객체모델을 생성하는 방식으로 작동
	- 모든 SQL을 XML로 작성하고 SQL문을 사용하는 DAO클래스를 설계해서 SQL호출하는 방식
- 팀 전원이 아파치 소프트웨어 재단에서 구글 코드로 이전하면서 중단됨
- 새로운 프레임워크 MyBatis로 변경

### 장점
- 인터페이스와 애노테이션을 통해서 **SQL문 설정하고 처리**할 수 있음
- XML만을 이용해서 SQL문을 설정 
- DAO에서는 xml찾아서 실행하는 코드 작성하는 방식 
- SQL수정 유지보수적합하나 복잡성 증가
- 동적 Query 지원
- ORM 지원

### 결론  

| MyBatis | Hibernate  |
|:--------:|:--------:|
|   SQL을 생성하고 싶을 경우	| SQL 을 생성하고 싶지않을 경우	|
|	데이터베이스에 따라 달라질 수 있는 SQL을 사용	| 데이터베이스와 독립적인 HQL을 사용	|
|	ResultSet을 POJO 객체에 매핑하므로 테이블 구조에 대해 신경 쓸 필요 없움 	|	Java POJO 객체를 데이터베이스 테이블에 매핑	|
|	Deletion	|	θ(1)	|



----
#### references
<https://practice.geeksforgeeks.org/problems/what-is-orm>
<https://www.javatpoint.com/hibernate-tutorial>
<https://www.geeksforgeeks.org/introduction-to-hibernate-framework/>
<https://www.tutorialspoint.com/hibernate/orm_overview.htm>
<https://www.geeksforgeeks.org/difference-between-jdbc-and-hibernate-in-java/>
<https://www.javatpoint.com/jpa-vs-hibernate>
<https://www.tutorialspoint.com/mybatis/mybatis_overview.htm>
