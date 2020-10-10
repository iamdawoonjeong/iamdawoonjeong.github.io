---
layout: single
title: "[JAVA] 스캐너(Scanner) VS 버퍼드리더(BufferedReader)"
date: 2020-10-10 13:32:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- JAVA
- Scanner
- BufferedReader
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-scanner-vs-buffered_reader/"
---
# Scanner VS BufferedReader

## Scanner
- **java.util.Scanner** 클래스
- **기본 유형과 문자열을 구문 분석 할 수 있는 간단한 텍스트 스캐너**
- 내부적으로 정규식을 사용하여 다른 유형을 읽기 가능
- Java 프로그램에서 입력을 읽는 가장 쉬운 방법
- 특정 데이터 유형을 읽기 위해 사용할 함수는 **nextXXX() (nextInt(), nextFloat(), nextByte(), nextShort(), nextDouble(), nextLong(), next()) 사용 가능**
- 문자열을 읽으려면 nextLine()을 사용
- 단일 문자를 읽으려면 next(), charAt(0)을 사용
- next() 함수는 입력의 다음 토큰 / 단어를 문자열로 반환하고, charAt(0) 함수는 해당 문자열의 첫 번째 문자를 반환

## BufferReader
- **Java.io.BufferedReader 클래스**
- Buffer를 이용해 입출력의 효율을 높혀줌
- **문자 입력 스트림**으로, 텍스트를 읽고 문자를 버퍼링하여, 문자 시퀀스를 효율적으로 읽을 수 있도록 함 (line단위의 입출력이 편리함)
- 버퍼 크기를 지정하거나 기본 크기를 사용할 수 있으며, 기본값은 대부분의 목적에 충분히 큼
- 일반적으로 Reader의 각 읽기 요청은 해당 읽기 요청이 기본 문자 또는 바이트 스트림으로 이루어 지도록 함
- 따라서 FileReaders 및 InputStreamReaders[^1]와 같이 read () 작업에 비용이 많이들 수 있는 판독기 주위에 BufferedReader를 래핑하는 것이 좋음
- 텍스트 입력에 DataInputStreams를 사용하는 프로그램은 각 DataInputStream을 적절한 BufferedReader로 대체하여 지역화 할 수 있음

### 생성자  
- BufferedReader (Reader in) : 기본 크기의 입력 버퍼를 사용하는 버퍼링 문자 입력 스트림을 만듦
- BufferedReader (Reader in, int sz) : 지정된 크기의 입력 버퍼를 사용하는 버퍼링 문자 입력 스트림을 만듦

### 문자 입력 스트림
- 입출력 단위가 2byte(JAVA에서는 문자를 의미하는 char형은 2byte)  (cf. 바이트 기반 스트림 : 입출력 단위가 1byte)
- 문자기반 스트림은 여러 종류의 인코딩과 자바에서 사용하는 유니코드간의 변환을 자동적으로 처리해주기 때문에 Reader는 특정 인코딩을 읽어서 유니코드로 변환하고,  Writer는 유티코드를 특정 인코딩으로 변환하여 자동 저장(한글 깨짐 방지)


## 비교 : nextXXX () 이후에 nextLine()을 사용할 때 Scanner 문제

### Scanner 예제

```java
Scanner sc = new Scanner(System.in);

System.out.println("Enter an integer");
int a = sc.nextInt();
System.out.println("Enter a String");
String b = sc.nextLine();
System.out.printf("You have entered:- "+ a + " " + "and name as " + b);
```

- input

```java
10
JAVA
```

- output : 첫째줄 int 타입받고 enter 누르고 바로 string 받지않고 다 출력 됨

```java
Enter an integer
Enter a String
You have entered:- 10 and name as
```


### BufferReader 예제

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
System.out.println("Enter an integer");

int a = Integer.parseInt(br.readLine());
System.out.println("Enter a String");
String b = br.readLine();
System.out.printf("You have entered:- " + a + " and name as " + b);
```

- input

```java
10
JAVA
```

- output

```java
Enter an integer
Enter a String
you have entered:- 10 and name as JAVA
```

- Scanner 클래스에서 nextXXX() 메서드 중 하나를 사용하여 nextLine() 메서드를 호출하면, nextLine()이 콘솔과 커서의 값을 읽지 않고 콘솔에 들어가지 않으면 해당 단계를 건너뛰게 되는데, 이 문제는 Scanner 클래스에서만 발생한다. 다음 XXX() 메서드는 newline 문자를 무시하고 nextLine()은 첫 번째 newline 문자까지만 읽기 때문이다. nextXXX()와 nextLine() 사이에 nextLine() 메서드를 한 번 더 사용하면 nextLine()이 newline 문자를 사용하기 때문에 이 문제가 발생하지 않으며, 이 문제는 여기에 나타난 바와 같이 문자열 입력을 위해 nextLine() 대신 next()를 사용함으로써도 해결할 수 있다.
- BufferReader 클래스에는 이러한 유형의 문제가 없음


## 기타 차이점
- BufferedReader는 동기식 이지만,  Scanner는 아님. 다중 스레드로 작업하는 경우 BufferedReader를 사용해야 함
- BufferedReader는 Scanner보다 훨씬 더 큰 버퍼 메모리를 가지고 있음
- Scanner에는 BufferedReader (8KB byte buffer)와 달리 작은 버퍼 (1KB char buffer)가 있지만 충분
- **Scanner가 입력 데이터를 구문 분석하고, BufferedReader는 단순히 문자 시퀀스를 읽기 때문에 스캐너에 비해 조금 더 빠름**


---
### references
<https://www.geeksforgeeks.org/scanner-class-in-java/?ref=rp>  
<https://www.geeksforgeeks.org/java-io-bufferedreader-class-java/>  
<https://www.geeksforgeeks.org/difference-between-scanner-and-bufferreader-class-in-java/>  


---
### 주석
[^1]: 입출력 단위가 1byte, JAVA에서는 문자를 의미하는 char형은 2byte
