---
layout: single
title: "[JAVA] WebApplication - Servlet"
date: 2021-04-22 22:20:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- java
- web
- servlet
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-webapplication-servlet/"
---
# Web Application - Servlet

## Web Application?
- 네트워크와 서버를 사용하여 통신하는 모든 프로그램을 의미
- 웹 브라우저를 사용하여 액세스하므로 브라우저를 사용자 클라이언트로 쉽게 사용가능

## JAVA Web Application
- 동적 자원 (예 : 서블릿, JavaServer 페이지, Java 클래스 및 jar) 및 정적 자원 (HTML 페이지 및 그림)의 모음
- 웹 컨테이너 내에서 실행
- WAR (Web ARchive) 파일로 배포 가능
    - WAR는 해당 웹 응용 프로그램의 전체 내용을 포함하는 zip 파일(자바의 JAR파일과 같은 역할)
- 서블릿을 기반으로 인기있는 Java 웹 프레임 워크는 GWT, JavaServer Faces, Struts 및 Spring 프레임 워크
- 콘솔애플리케이션
- 웹 애플리케이션 : 서블릿 
- c.f ) GUI 애플리케이션 : 스윙

## JAVA Web Application 기술
### Servlet  
#### Servlet 이란 ?
- 자바를 사용하여 웹페이지를 동적으로 생성하는 서버측 프로그램
- 자바 플랫폼에서 컴포넌트 기반의 웹애플리케이션 개발 기술
- 웹서버에 요청을 수신하고, 수신한 요청을 처리하고, 서버에 다시 응답하는 소프트웨어의 구성 요소 (일련의 모든 과정을 직접 개발 할 필요 없이 서블릿을 사용하면 아주 간편해짐)
- 자바 서블릿 API는 JVM위에서 실행되는 애플리케이션을 빌드하기 위한 인터페이스 집합과 파일 정의들
- 다양한 유형의 요청에 응답하며, 서버의 기능을 확장하고, 웹서버에서 웹 애플리케이션을 호스팅 하기 위한 웹컨테이너 처럼 작동
- 클라이언트-서버 프로토콜을 지원 하지만 HTTP Servlet 이라고도 함

#### Servelt 동작
- 서블릿 동작:  서블릿 컨테이터에 등록 후 -> 서블릿 컨테이너에 의해 init() 생성, service() 호출, destory() 소멸이 이루어짐
- c.f) 자바독립 실행 프로그램 동작 : public static void main(String[] args)  메서드가 시작되면 프로그램 수행을 시작

#### Servelt 구조
![JAVA-servlet-architecture]({{ site.baseurl }}/assets/images/posts/2021/JAVA-servlet-architecture.png)
- 사용자가 웹 서버에 HTTP 요청을 보냄
- 서버에는 데이터베이스에서 데이터를 수집하고 응답을 생성하는 서블릿이 포함 된 웹 컨테이너가 존재
- 서블릿에서 생성 된 응답은 HTTP 응답을 통해 클라이언트 브라우저로 전송

#### Servelt container
- 서블릿 객체를 관리하고 클라이언트에게 서비스 해주는 프로그램
- Tomcat, Jetty, JBoss 등의 오픈소스 기반
- WebLogic, WebSphere, Zeus, JBoss의 상용 서비스

![JAVA-servlet-webcontainer]({{ site.baseurl }}/assets/images/posts/2021/JAVA-servlet-webcontainer.png)

- 사용자가 웹 서버에 HTTP 요청을 보냄
- 웹 서버는 웹 컨테이너에 요청을 전달
- 웹 컨테이너는 요청 객체의 형태로 서블릿에 요청을 전달
- 서블릿은 응답 객체를 빌드하고 웹 컨테이너로 다시 보냄
- 웹 컨테이너는 응답 객체를 상응하는 HTTP 응답으로 변환하고 웹 서버로 보냄
- 웹 서버는 HTTP 응답을 통해 클라이언트로 응답을 보냄

#### Servlet LifeCycle
- init()
    - 한 번만 호출 -> 서블릿이 생성 될 때만 호출 -> 일회성 초기화에 사용
    - 일반적으로 서블릿은 사용자가 서블릿에 해당하는 URL을 처음 호출 할 때 생성되지만 서버가 처음 시작될 때 로드되어야하는 서블릿을 지정할 수도 있음
- service()
    - 실제 작업을 수행하는 주요 메서드
    - 웹 컨테이너 (서블릿 컨테이너)는 service () 메서드를 호출하여 클라이언트에서 오는 요청을 처리
    - 서버가 서블릿에 대한 요청을 받을 때마다 웹 컨테이너는 새 스레드를 생성하고 service ()를 호출
     - 이 메소드는 HTTP 요청 유형 (GET, POST, PUT, DELETE 등)을 확인하고 doGet, doPost, doPut, doDelete 등의 메소드를 적절하게 호출
- destroy()
    - 서블릿의 수명주기가 끝날 때 한 번만 호출
    - 이 방법은 서블릿에 데이터베이스 연결을 닫고 백그라운드 스레드를 중지하고 다른 정리 작업을 수행 할 수있는 기회를 제공
    - destroy() 메소드가 실행 된 후 서블릿 객체는 가비지 수집에 사용할 수 있는 것으로 표시


----
#### references
<https://www.edureka.co/blog/java-web-application/>  
<https://codeburst.io/understanding-java-servlet-architecture-b74f5ea64bf4>  
<https://ko.wikipedia.org/wiki/%EC%9E%90%EB%B0%94_%EC%84%9C%EB%B8%94%EB%A6%BF>  
