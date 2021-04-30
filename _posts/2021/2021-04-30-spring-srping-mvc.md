---
layout: single
title: "[Spring] Spring MVC"
date: 2021-04-30 22:22:00.000000000 +09:00
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
permalink: "/spring-spring-mvc/"
---
- Spring MVC는 웹 애플리케이션을 빌드하는 데 사용되는 Java 프레임 워크
- MVC 디자인 패턴
- Inversion of Control, Dependency Injection과 같은 핵심 스프링 프레임 워크의 모든 기본 기능을 구현
- DispatcherServlet의 도움으로 Spring 프레임 워크에서 MVC를 사용하는 우아한 솔루션을 제공
	- DispatcherServlet은 들어오는 요청을 수신하여 컨트롤러, 모델 및 뷰와 같은 올바른 리소스에 매핑하는 클래스

## Model-View-Controller
### Model
- 모델에는 애플리케이션의 데이터가 포함됨
- 데이터는 단일 개체 또는 개체 모음

### Controller
- 컨트롤러에는 애플리케이션의 비즈니스 로직이 포함
- `@Controller` 주석은 클래스를 컨트롤러로 표시하는 데 사용됨

### View
- 보기는 제공된 정보를 특정 형식으로 나타냄
- 일반적으로 JSP + JSTL은보기 페이지를 만드는 데 사용됨
- Spring은 Apache Velocity, Thymeleaf 및 FreeMarker와 같은 다른 뷰 기술도 지원

### FrontController
- Spring Web MVC에서 DispatcherServlet 클래스는 프론트 컨트롤러로 작동
- Spring MVC 애플리케이션의 흐름을 관리

![spring_mvc]({{ site.baseurl }}/assets/images/posts/2021/spring_mvc.png)

## Spring MVC 흐름  

### Dispather Servlet
- 모든 요청이 프론트 컨트롤러로 작동하는 DispatcherServlet에 전달 받음

### HandlerMapping
- 클라이언트의 요청 URL을 어떤 컨트롤러가 처리할지 결정
- HandlerAdapter : 각 타입의 컨트롤러 구현체를 알맞게 호출하기 위해 사용

### Controller
- 클라이언트의 요청을 처리한 뒤 ModelAndView의 개체를 반환

### ModelAndView
- Controller가 처리한 결과 정보 및 뷰선택에 필요한 정보를 담음

### ViewResolver
- 컨트롤러의 처리 결과를 생성할 뷰를 결정

### View
- 컨트롤러의 처리 결과를 화면에 생성
- JSP, Velocity, Thymeleaf 템플릿을 뷰로 사용

![spring_flow-of-spring-web-mvc]({{ site.baseurl }}/assets/images/posts/2021/spring_flow-of-spring-web-mvc.png)

1. 처리 요청 URL전달 받음
2. 요청 URL와 매핑되는 Controller 검색
3. 처리요청
4. ModelAndView 리턴  
5. Controller의 실행 결과를 보여줄 View 검색
6. 응답 출력 요청


## 특징
- 분리 된 역할 : Spring MVC는 모델 객체, 컨트롤러, 명령 객체, 뷰 리졸버, DispatcherServlet, 유효성 검사기 등이 특수 객체에 의해 수행 될 수있는 각 역할을 분리
- 경량 : 경량 서블릿 컨테이너를 사용하여 애플리케이션을 개발, 배포
- 강력한 구성 : 웹 컨트롤러에서 비즈니스 개체 및 유효성 검사기까지 컨텍스트 전반에 걸쳐 쉽게 참조 할 수있는 프레임 워크 및 애플리케이션 클래스 모두에 대한 강력한 구성을 제공
- 신속한 개발 : Spring MVC는 빠르고 병렬적인 개발을 용이하게 함
- 재사용 가능한 비즈니스 코드 : 새 개체를 만드는 대신 기존 비즈니스 개체를 사용 가능
- 쉬운 테스트 : Spring에서는 일반적으로 setter 메서드를 사용하여 테스트 데이터를 주입 할 수있는 JavaBeans 클래스를 만듦
- 유연한 매핑 : 페이지를 쉽게 리디렉션하는 특정 주석을 제공


## 구성
### 구조
#### pom.xml 파일에 프로젝트 정보 및 구성을 제공
- Maven을 사용하는 경우 maven 종속성 추가

#### web.xml 파일에 컨트롤러 항목 제공
- Spring Web MVC에서 프론트 컨트롤러 역할을하는 서블릿 클래스 DispatcherServlet을 지정
- html 파일에 대한 모든 수신 요청은 DispatcherServlet으로 전달됨
- 공통으로 사용할 어플리케이션 컨텍스트 설정

#### 컨트롤러 클래스 만들기
- 컨트롤러 클래스를 생성하기 위해 두 개의 주석 `@Controller` 및 `@RequestMapping`을 사용
- `@Controller` : 클래스를 Controller로 표시함
- `@Requestmapping` : 지정된 URL 이름으로 클래스를 매핑하는데 사용

#### spring-servlet.xml 파일에 빈 정의
- 스프링 컨테이너에서 컨트롤러 객체를 검색하기 때문에 스프링 설정파일에 컨트롤러를 빈으로 등록
- View 구성 요소를 지정해야하는 중요한 구성 파일
- context : component-scan 요소는 DispatcherServlet이 컨트롤러 클래스를 검색 할 기본 패키지를 정의
- WEB-INF 디렉토리에 있어야 함

#### 참고
- 의존관계는 인터페이스를 통해 이루워짐  
	- 구상 클래스에 대해서는 기술 할 필요가 없음 -> 객체간의 결합이 약해짐

- Tightly coupled 
	- 구현 클래스 변경시 동작방법이 없음
	- 클래스 이름, 생성자나 호출메소드의 형태(입출력 파라미터,리턴형을)을 변경시에는 호출하는 클래스의 수정 후 재 컴파일 필요
	- 텍스트 작업부담이 증가
	- 인터페이스 사용으로 해결 

- Loosely coupled
	- 인터페이스를 상속함으로써 인터페이스와 구현 부분을 분리해서 코딩 
	- 인터페이스 변경이 없다면 구현부분이 바뀌어도 이용하는 쪽이 받는 영향을 최소화 함 => 객체지향프로그래밍은 구현하지 않고 인터페이스를 사용하는 것을 추천
	- 코딩상 규약으로서의 기능을 하기 때문에 변경에 강한 애플리케이션을 만들 수 있음

- 구현 클래스 변경시 동작보장됨 
	- 구현 객체 이름 변경 요구 됨
	   => 해결방안 : Factory Method 디자인패턴 혹은 스프링으로 해결 가능 
	   => 인터페이스 기반 설계와 스프링을 활용하는 것으로 변경이 용이한 애플리케이션 만들 수 있음

#### 참고
- Spring 1.x에 있는 설정파일은 DTD(Document Type Definition, 문서 형식 정의) 기반 스키마 정의
- Spring 2.0 이후 설정파일은 XML 스키마 기반 스키마 정의


----
#### references
<https://docs.spring.io/spring-framework/docs/3.2.x/spring-framework-reference/html/mvc.html>  
<https://docs.spring.io/spring-framework/docs/3.0.0.RC3/spring-framework-reference/html/ch15s02.html>  
<https://www.javaguides.net/2020/07/how-spring-mvc-works-internally.html>  
<https://www.javatpoint.com/spring-mvc-tutorial>  
