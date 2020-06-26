---
layout: single
title: "[JAVA] 오버로딩 (Overloading) VS 오버라이딩 (Overriding)"
date: 2020-06-26 19:07:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- JAVA
- exception
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-overlading-vs-overriding/"
---
#  오버로딩 Overloading VS 오버라이딩 Overriding

![java-OverridingVsOverloading]({{ site.baseurl }}/assets/images/posts/2020/java-OverridingVsOverloading.png)

## 오버로딩 Overloading
- 시그니처[^1] 중 메서드 이름은 같지만 아규먼트 타입이나 개수가 다른메서드를 오버로딩 한 메서드
- 같은 일을 하는 함수에 대해 다른 이름을 만들고 기억할 필요가 없음
- 다른 정적 메서드와 마찬가지로 main ()을 오버로드 가능
- 컴파일러 시간 다형성의 예
- 아큐먼트 타입, 개수는 같으면서 return type만 바꾸는 것은 안됨 -> compile error 발생  
- 가독성을 높히기 위해서 같은 클래스내에서 사용 됨


```java
class OverloadingExample{  
    static int add(int a,int b){return a+b;}  
    static int add(int a,int b,int c){return a+b+c;}  
}  
```


## 오버라이딩 Overriding
- 상속관계의 두 클래스 에서 메서드 이름, 아규먼트 타입과 개수가 동일하게 선언된 메서드
- 런타임 다형성의 예
- 실행 되는 메소드의 버전은 메소드를 호출하는 데 사용되는 오브젝트에 의해 결정
- static 메소드는 override 할수 없으며, main()도 static 메소드 이기 때문에 override 불가
- 수퍼 클래스가 이미 제공 한 메소드 의 특정 구현을 제공하는 데 사용

```java
class Animal{  
    void eat(){System.out.println("eating...");}  
}  
class Dog extends Animal{  
   void eat(){System.out.println("eating bread...");}  
}  
```

![java-overriding-in-java]({{ site.baseurl }}/assets/images/posts/2020/java-overriding-in-java.png)


---
#### references
<https://www.geeksforgeeks.org/overloading-in-java/>  
<https://www.geeksforgeeks.org/overriding-in-java/?ref=lbp>  
<https://www.javatpoint.com/method-overloading-in-java>  
<https://www.javatpoint.com/method-overriding-in-java>  
<https://www.javatpoint.com/method-overloading-vs-method-overriding-in-java>  


----
#### 주석
[^1]: 메서드 리턴타입, 메서드 이름, 아규먼트
