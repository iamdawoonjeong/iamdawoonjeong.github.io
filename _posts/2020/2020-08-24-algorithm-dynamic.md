---
layout: single
title: "[Algorithm] 동적 프로그래밍 (Dynamic Programming)"
date: 2020-08-24 21:51:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Algorithm
tags:
- data structure
- algorithm
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-dynamic/"
---
# Dynamic Programming (DP : 동적 프로그래밍)
-  최적화 문제를 해결하기위한 가장 강력한 설계 기술
-  bottom-up (상향식 접근 방식) : 제일 작은 문제부터 상위에있는 문제로 풀어 올라감 (c.f: top-down 방식(예:분할정복))
-  동일한 입력에 대한 반복 호출이있는 재귀 솔루션을 볼 때마다 동적 프로그래밍을 사용하여 최적화 가능

### 연산
1. 문제를 부분 문제로 나눔
2. 가장 작은 부분 문제부터 해를 구한 뒤 테이블에 저장
3. 테이블에 저장되어 있는 부분 문제의 해를 이용하여 점차적으로 상위 문제의 최적해를 구함


![algorithm-Dynamic-Programming-1]({{ site.baseurl }}/assets/images/posts/2020/algorithm-Dynamic-Programming-1.png)


### 종류
- Fibonacci number series (피보나치 수열)
- Knapsack problem (배낭 문제)
- Tower of Hanoi (하노이의 탑)
- All pair shortest path by Floyd-Warshall (Floyd-Warshall의 모든 페어 최단 경로)
- Shortest path by Dijkstra (Dijkstra의 최단 경로)
- Project scheduling (프로젝트 일정)
- 0/1 Knapsack Problem


### 자바를 이용하여 동적계획법 - fibonacci 수열 구현
- **점화식으로 피보나치 수열을 정의 할 수 있고 아래와 같은 전제로 동적계획법 코드를 작성**

- F<sub>0</sub>=0
- F<sub>1</sub>=1
- F<sub>n+2</sub>=F<sub>n+1</sub>+F<sub>n</sub>


[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-theory/src/dynammic/fibonacci/fibonacciDynamic.java)


```java
public static int fibonacci(int n) {
    // fibonacci를 저장할 배열 선언
    int f[] = new int[n+1];
    int i;

    //점화식으로 f(0)=1, f(1)=1을 미리 정의
    f[0] = 0;
    f[1] = 1;

    for (i = 2; i <= n ; i++) {
        // 위에서 저장한 0,1번째 수를 제외하고 2번째 부터 저장
        f[i] = f[i-1] + f[i-2];
        System.out.println("i = " + i + " : "  +f[i] + " = "  +  f[i-1] + " + " + f[i-2]);
    }
    return f[n];
}
```

---

#### references
<https://www.javatpoint.com/dynamic-programming-introduction>  
<https://www.geeksforgeeks.org/dynamic-programming/>  
<https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/>  
<https://www.tutorialspoint.com/data_structures_algorithms/dynamic_programming.htm>  
