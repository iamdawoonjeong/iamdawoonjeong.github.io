---
layout: single
title: "[WEB] HTTP와 REST API"
date: 2021-04-22 22:20:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- web
tags:
- HTTP
- web
- RESTAPI
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/web-http-restapi/"
---
## HTTP (HyperText Transfer Protocol)
- W3 상에서 정보를 주고받을 수 있는 프로토콜
- HTTP는 클라이언트와 서버 사이에 이루어지는 요청/응답(request/response) 프로토콜

### 프로토콜
- TCP (Transmission Control Protocol) 전송 제어 프로토콜
	- 연결지향 : TCP 3 way handshake (SYN - SYN/ACK - ACK)
	- 데이터 전달 보증
	- 순서 보장
	- 신뢰할 수 있는 프로토콜
	- 현재는 대부분 TCP 사용
- UDP (User Datagram Protocol) 사용자 데이터그램 프로토콜
	- 단순
	- 서비스의 신뢰성이 낮음
	- 데이터의 도착 순서 예측 할 수 없음

### 특징
- Client–server 구조
- 무상태 프로토콜(Stateless), 비연결성
- HTTP 메시지
- 단순함, 확장 가능

### HTTP API
#### GET
- 리소스 표현 / 정보 만 검색
- 예) HTTP GET http://www.appdomain.com/users?size=20&page=5

#### POST
- 새 하위 리소스를 생성
- 예) HTTP POST http://www.appdomain.com/users

####  PUT
- 기존 리소스를 대체
- 클라이언트가 리소스를 식별
- 예) HTTP PUT http://www.appdomain.com/users/123

#### DELETE
- 리소스를 삭제 하는 데 사용
- 예) HTTP 삭제 http://www.appdomain.com/users/123

#### PATCH
- 리소스를 부분적으로 업데이트하는 것

### HTTP 메서드 속성
- Safe Methods 안전
	- HTTP 사양에 따라 GET 및 HEAD 메서드는 리소스 표현 검색에만 사용해야하며 서버의 리소스를 업데이트 / 삭제하지 않음 => 두 가지 방법 모두 "안전한" 것으로 간주
	- POST, PUT 및 DELETE은 사용자가 안전하지 않은 작업이 요청되고 있다는 사실을 사용자가 인식하고 서버에서 리소스를 업데이트 / 삭제할 수 있으므로 신중하게 사용해야 함
- Idempotent Methods 멱등
	- 멱 등성이라는 용어는 한 번 또는 여러 번 실행하면 동일한 결과를 생성 하는 작업
	- GET, HEAD, PUT 및 DELETE 메서드는 멱등 메서드

### 응답코드
- 1XX : Informational(정보)	정보 교환
- 2XX : Success(성공)	데이터 전송이 성공적으로 이루어졌거나, 이해되었거나, 수락되었음
- 3XX :	Redirection(방향 바꿈)	자료의 위치가 바뀌었음
- 4XX : Client Error(클라이언트 오류)	클라이언트 측의 오류 주소를 잘못 입력하였거나 요청이 잘못 되었음
- 5XX	Server Error(서버 오류)	서버 측의 오류로 올바른 요청을 처리할 수 없음

## REST API (RESTful API)
#### REST (REpresentational State Transfer)?
- 분산 하이퍼미디어 시스템을 위한 소프트웨어 아키텍처의 한 형식
- 확장 가능하고 내결함성이 있으며 쉽게 확장 가능한 시스템을 보장하는 일련의 제약 조건
	- REST 또는 RESTful API 디자인 (Representational State Transfer)은 기존 프로토콜을 활용하도록 설계되어 있음
- REST 아키텍처 스타일에서 데이터와 기능은 리소스로 간주되며 URI (Uniform Resource Identifier)를 사용하여 액세스
- REST 기반 시스템의 상호 작용은 인터넷의 HTTP (Hypertext Transfer Protocol)를 통해 발생

#### REST API
- REST 아키텍처 스타일을 따르는 웹 서비스를 RESTful 웹서비스라고 함
- REST API는 사용자 또는 클라이언트와 그들이 얻고자 하는 리소스 또는 웹 서비스 간의 중개자로 생각
- 클라이언트가 요청하는 내용에 따라 XML, JSON, YAML 또는 기타 형식을 반환 할 수 있음
- REST의 6가지 기본 원칙을 준수 할 때까지 RESTful 인터페이스를 호출 가능
- 요청 시스템은 균일하고 미리 정의 된 규칙 집합을 사용하여 웹 리소스에 액세스하고 조작가능

### REST웹 서비스를 진정한 RESTful API로 만드는 6가지 아키텍처 제약 조건
- Client–server (클라이언트-서버)
	-  클라이언트-서버의 각 파트가 독립적으로 개선될 수 있도록 해야 함
- Stateless (무상태)
	- 각 요청 간 클라이언트의 콘텍스트가 서버에 저장되어서는 안 됨
	- 세션 상태는 전적으로 클라이언트에 유지
- Cacheable  (캐시 가능)
	- 클라이언트는 응답을 캐싱할 수 있어야 함
- Uniform interface (균일한 인터페이스)
	- 일관적인 인터페이스로 분리되어야 함
	- REST는 네 가지 인터페이스 제약 조건으로 정의 : 리소스 식별, 표현을 통한 자원 조작, 자기 설명 메시지, 그리고 애플리케이션 상태의 엔진으로서의 하이퍼 미디어
- Layered system (계층형 시스템)
	- 계층 형 시스템 스타일을 사용하면 각 구성 요소가 상호 작용하는 직계 계층 너머를 볼수 없도록 구성 요소 동작을 제한하여 아키텍처를 계층 적 계층으로 구성 가능
- Code on demand (optional) – 요청시 코드 (선택 사항)
	- REST를 사용하면 애플릿 또는 스크립트 형식으로 코드를 다운로드하고 실행하여 클라이언트 기능을 확장 시킬수 있어야 함
	- 필요한 기능의 수를 줄여 클라이언트를 단순화 함


## REST! ​​= HTTP
- 웹 자체는 HTTP에서 실행되며, RESTful API도 동일한 작업을 수행
- REST 제약에는 전송 프로토콜로 HTTP를 필수로 사용하는 것이 없음
- RESTful API는 현재 HTTP를 전송 계층으로 사용


### 직렬화 Serialization
- 직렬화된 객치는 디스크레 기록 할 수도 있고, 네트워크가 아닌 다른 I/O인터페이스에 기록하는 과정
- JVM이서 자바 객체를 내보내는 간단한 방법

### JSON
- JSON (JavaScript Object Notation)은 경량의 DATA-교환 형식
- name/value 형태의 쌍으로 collection 타입
- 자바스크립트의 유래
- xml보다 구문이 적어 부담이 덜해 다른 언어용 라이브러리에서 많이 채택
- XSD(XML Schema Definition)를 이용한 XML과 비슷한 직렬화 접근 방법
- JSON을 자바에서 처리할때에는 Jackson이라는 라이브러리 사용 
- JSON은 사람이 읽을 수 있는 접근 방법을 사용하며 다양한 언어를 통해 파싱되고 처리될 수 있음


----
#### references
<https://ko.wikipedia.org/wiki/HTTP>  
<https://restfulapi.net/>  
<https://restcookbook.com/Miscellaneous/rest-and-http/>  
<https://www.mulesoft.com/resources/api/what-is-rest-api-design>  
<https://www.geeksforgeeks.org/rest-api-architectural-constraints/>  
<https://www.json.org/json-ko.html>  
