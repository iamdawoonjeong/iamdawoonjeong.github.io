---
layout: single
title: "[JAVA] 프로세스(Process) VS 스레드(Thread), 멀티태스킹(Multitasking)"
date: 2020-06-25 18:37:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- JAVA
- process
- thread
- multitasking
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-process-vs-thread/"
---
## process vs thread

### process
- 실행중인 프로그램
- 자원과 쓰레드로 구성됨

### thread
- 프로세스 내에서 실행되는 흐름의 단위
- 가장 작은 처리 단위 인 경량 하위 프로세스
- 프로세스내에서 실제 작업을 수행
- 모든 프로세스는 하나 이상의 쓰레드를가지고 있음
- 한 번에 하나의 스레드 만 실행

![java-thread-life-cycle]({{ site.baseurl }}/assets/images/posts/2020/java-thread-life-cycle.png)

## 멀티 태스킹 Multitasking


### Process-based Multitasking (Multiprocessing)
- 각 프로세스에는 메모리에 주소가 존재. 즉, 각 프로세스는 별도의 메모리 영역을 할당
- 프로세스는 무겁움
- 프로세스 간 통신 비용이 높음
- 한 프로세스에서 다른 프로세스로 전환하려면 레지스터, 메모리 맵, 업데이트 목록 등 을 저장하고 로드하는 데 약간의 시간이 필요

### Thread-based Multitasking (Multithreading)
- 여러 쓰레드를 동시에 실행하는 프로세스
- 쓰레드가 독립적이며 동시에 여러 작업을 수행 할 수 있기 때문에 사용자를 차단하지 않음
- 많은 작업을 함께 수행 할 수 있으므로 시간이 절약
- 쓰레드는 독립적 이므로 단일 스레드에서 예외가 발생하면 다른 스레드에 영향을 미치지 않음
- 쓰레드는 동일한 주소 공간을 공유
- 가벼움
- 쓰레드 간의 통신 비용이 낮음


![java-multithreading]({{ site.baseurl }}/assets/images/posts/2020/java-multithreading.png)


---
#### references
<https://www.geeksforgeeks.org/multithreading-in-java/?ref=lbp>  
<https://www.javatpoint.com/multithreading-in-java#multitasing>
