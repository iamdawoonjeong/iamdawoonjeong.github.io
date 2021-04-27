---
layout: single
title: "[Spring] Spring Framework (DI/AOP)"
date: 2021-04-26 21:43:00.000000000 +09:00
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
permalink: "/spring-springframework/"
---
## Spring의 특징과 장점
- **애플리케이션 프레임워크**
- 스프링은 Struts같은 웹 애플리케이션 개발용 웹프레임워크와는 달리 어떤 애플리케이션에도 적용가능
- JEE대체하는 프레임워크
- **경량컨테이너** <-> EJB  
	- 복잡한 절차를 요구하는 'EJB(Enterprise Java Beans')에 비해 경랑 컨테이너
	- 자바객체를 담고 있고, 자바객체의 생성, 소멸과 같은 라이프 사이클 관리하며 필요한 객체를 가져와 사용 하면서 EJB기능 다수행하면서도 경량 
	- EJB에 대항하는 것이 바로 Spring
- 객체를 담고있는 컨테이너를 제공: 컨테이너에 객체를 담아두고 필요할때에 컨테이너로부터 객체를 가져와서 사용
- 트랜잭션 처리를 위한 일관된 방법을 제공 : 설정 파일을 통해 트랜잭션 관련 정보를 입력하기 때문에, 트랜잭션 구현에 상관없이 동일 한 코드를 여려 환경에서 사용할 수 있음
- 영속성과 관련된 다양한 API지원 (영속성;DB의 특징, 즉 DB를 가져다 쓰기 위한 API 지원) : JDBC를 비롯한 myBATIS, 하이버네이트, JPA등 데이터베이스 처리를 위해 널리 사용되는 라이브러리 연동을 지원
- 다양한 API 연동 지원 (DB뿐 아니라 보안 메일등의 API) : JMS,메일, 스케줄링 등 다양한 API를 설정파일과 어노테이션을 통해서 손쉽게 사용 가능 
- 독립적이고 테스트 가능한 컴포넌트들 작성가능
- POJO (Plain Old Java Objects) 작성한 후 애플리케이션 컨텍스트라는 핵심 컴포넌트를 통한 의존성 주입 (dependency injection)을 이용해 POJO를 연결
- **핵심: DI, AOP **


## DI (Dependency Injection) / IoC (Inversion of control)
### DI란?
- IoC(Inversion of Control)이라고도 함 (제어의 역전)
	- DI패턴을 지원해주는 프레임 워크(spring) 설정파일과 어노테이션을 이용하여 손쉽게 객체간의 의존 관계 설정 가능  
- 서비스 구현 클래스내 의존 객체를 직접 생성하지 않고, 생성자에서 의존하는 객체를 전달 받음
	- spring container(스프링내부에 있는 객체(Bean)들간의 관계를 관리)가 필요한 객체를 스스로 끌어들임(밖->안 setMethod 집어 넣음)
	- 외부 라이브러리 같은 의존 관계를 코드 내부에 기술하는 것이 아니라 외부 파일을 이용해서 설정하는 방식 
	- 객체는 의존하고 있는 객체를 직접 생성하거나 검색할 필요 없음
	- 불필요한 의존관계를 없애거나 줄일 수 있음
- 테스트 수행 수월 (단위 테스트 진행)
- 의존성 : 어떤 클래스가 자신의 임무를 다하기 위해 필요한 값이나 사용할 다른 클래스와의 관계
- 주입 : 어떤 클래스의 인스턴스에 대해 외부로부터 '의존성'을 설정하는 것.
- 의존관계 주입 컨테이너의 역할 : 
	- 어떤 클래스가 필요로 하는 값이나 인스턴스를 생성, 취득 그 클래스의 인스턴스에 대해 설정
	- 필요한 인스턴스를 생성, 취득하는 코드를 직접 만들지 않아도 됨
	- 클래스간 관계가 느슨한 결합이 되어 의존성은 약해짐 
- 내프로그램을 바꾸지 않으면서 쉽게 내가 하는 작업을 바꿀 수 있는 작업


### 의존관계 주입 방법
#### 생성자 주입
- 생성자를 통해서 의존 관계를 주입 받는 방법
- 생성자가 1개만 있으면 `@Autowired`를 생략해도 자동 주입
- 불변, 필수 의존관계에 사용
- 스프링에서 권장하는 방식

#### 수정자 주입
- setXXX() 형태의 setter라 불리는 필드의 값을 변경하는 수정자 메서드를 통해서 의존관계를 주입하는 방법
- 선택, 변경 가능성이 있는 의존관계에 사용

#### 필드 주입
- 필드에 바로 주입하는 방법

### 일반메서드 주입
- 일반 메서드를 통해서 주입하는 방법
- 한번에 여러 필드를 주입 받을 수 있음

### 어노테이션 기반 자동 설정
- `@Autowired` : 의존관계 자동 주입 (스프링 컨테이너가 자동으로 해당 스프링 빈을 찾아서 주입)
- 생성자에 적용, 설정메소드에 적용, 필드에 적용, 설정파일에 적용 하여 사용
- `import org.springframework.beans.factory annotation.Autowired;`

#### 정리
- **객체 지향 원리 적용**
- DI는 OCP(The Open-Closed Principle)
```
A dependency B
A -----> B
```
- A의 구조는 바꾸지 못함 (A의 구조는 closed 됨)
- A 내용은 바꾸게(open, extend) 하고 싶으면 밖에서 수정하여 주입 => DI 


## AOP(Aspect-Oriented Programming: 관점지향 프로그래밍)
### AOP란?
- Aspect란 소프트웨어가 갖는 다양한 특징이나 성질
- 공통관심사항(CCC:Cross Cutting Concern)을 구현한 모듈에 의존 관계를 갖지 않음
	- 공통관심사항 적용으로 인한 의존 관계의 복잡성과 코드 중복을 해소
	- 핵심로직을 핵심관심사항이라고 함 CC(Core Concern)
- 횡단적 관심사의 분리
	- 일반적으로 하나의 소프트웨어는 복수모듈로 구성
	- 어떤 관심사가 이러한 복수모듈에 산재하는 것을 '횡단적'이라고 하는데,  횡단적 관심사의 구체적인 예로 "LOG 출력"
- an Advanced Separation of Concern 분리된 관심사는 AOP프레임워크에 의해 관리되고, 필요에 따라 필요한 시점에 각 모듈에 삽입
- **각 모듈에서 분리된 기능을 사용하기 위한 코드를 기술할 필요 없음**
	- 모듈 개발자는 횡단적 관심사에 대해 젼혀 관여안함
	- 고도로 분리된 관심사는 객체 지향보다 한층 독립성이 강해지는 것은 물론 재사용성과 보존성이 향상
	- 코드에 손대지 않고도 새로운 기능  추가 가능
- **트랜잭션이나 로깅, 보안과 같이 여러 모듈에서 공통으로 필요로 하지만 실제 모듈의 핵심은 아닌 기능들을 분리해서 각 모듈에 적용 가능**
- 공통관심사항을 구현한 Aspect 클래스를 작성하고, 설정파일을 이용하여 Aspect를 핵심 로직을 구현한 클래스에 적용


### Spring 에서 AOP
- **객체 지향에 의존 관계 주입과 AOP를 조합함으로써, 보다 유연하고 보존성인 높은 견고한 소프트웨어를 개발 가능**
	- 객체지향에서는 기능과 데이터를 하나의 클래스 단위로 묶어 모듈로 부터 분리하여 재사용성과 보존성을 높임
- 핵심로직을 구현한 클래스를 실행하기 전 후에 Aspect를 적용, spring AOP는 핵심로직 수정하지 않고 적용이 가능 함
	- CC/CCC를 따로 구현하면, Spring 돌면서 실행은 섞여서 돌아가는 것처럼 보이게 됨
- 순수 Java로 구현
- 현재 메소드 실행 조인 포인트만 지원

### AOP 용어
- Aspect (관점) : 여러 클래스에 걸쳐있는 관심사의 모듈화
	- Spring AOP에서 aspect는 일반 클래스 (스키마 기반 접근) 또는 주석이 달린 일반 클래스 `@Aspect`(@AspectJ 스타일)를 사용
- Advice (어드바이스)
	- 관점으로서 분리되고 실행시 모듈에 위빙된 구체적인 처리
	- 언제 공통관심 기능을 핵심로직에 적용할 지를 정의
	- 메서드를 호출하기전에(언제) 트랙잭션을 시작한다(공통기능) 기능을 적용한다는 것을 정의
	- Around Advice : Joinpoint 앞과 뒤에서 실행되는 Advice
	- Before Advice :  Joinpoint 앞에서 실행되는 Advice
	- After Returning Advice : Joinpoint 메서드 호출이 정상적으로 종료된 뒤 실행되는 Advice
	- After Throwing Advice : 예외가 던져질 때 실행되는 Advice
	- Instroduction : 클래스에 인터페이스와 구현을 추가하는 특수한 Advice
- Joinpoint (조인포인트)
	- Advice를 위빙하는 포인트(적용 가능한 지점)
	- 특정 이름을 가진 메서드 실행하는 지점
- Pointcut (포인트컷)
	- 하나또는 복수의 joinpoint를 하나로 묶은 것
	- Jointpoint의 부분 집합으로서 실제로 Advice가 적용되는 Jointpoint나타냄
- Advisor (어드바이저)
	- Advice와 Pointcut을 하나로 묶어 다루는 것
	- 특정 결합 지점에서 측면에 의해 취해진 조치
- Weaving (위빙)
	- Advice를 핵심 로직 코드에 적용하는 것
	- 관심사를 다시 모듈에 삽입하는 것
	- Spring AOP는 런타임에 위빙을 수행
- AOP 프록시 : aspect 계약을 구현하기 위해 AOP 프레임 워크에 의해 생성 된 객체


### POJO (Plain Old Java Object) 
- 보통의 Java의 객체
- 자바코드를 이용해서 객체를 구성하는 방식을 그대로 스프링에서 사용
- 특정한 인터페이스를 구현하거나 클래스를 상속받지 않은 객체
- 기존에 작성한 코드 수정없이 사용 


----
#### references
<https://docs.spring.io/spring-framework/docs/3.0.x/spring-framework-reference/html/overview.html>  
<https://docs.spring.io/spring-framework/docs/current/reference/html/core.html>
