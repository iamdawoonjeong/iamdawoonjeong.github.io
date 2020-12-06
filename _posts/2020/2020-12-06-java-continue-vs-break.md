---
layout: single
title: "[JAVA] break VS continue"
date: 2020-12-06 17:20:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- break
- continue
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-break-vs-continue/"
---
# break VS continue

## break : 해당 조건에서 loop 문 중단

### for문에서 break

```java
for (int i = 0; i < 10; i++) {
    System.out.print(i + " ");
    if (i==5) {
        break;
    }
}
```

- output

```java
0 1 2 3 4 5
```


#### 중첩문일 경우 해당 조건에서 내부 loop만 빠져나옴 (종료)

```java
for (int i = 0; i < 10; i++) {

    System.out.println();
    System.out.println("(i) : "  + i);

    for (int j = 0; j < 10; j++) {
        System.out.print(j + " ");
        if (j==5) {
            break;
        }
    }
}
```

- output

```
(i) : 0
0 1 2 3 4 5
(i) : 1
0 1 2 3 4 5
(i) : 2
0 1 2 3 4 5
(i) : 3
0 1 2 3 4 5
(i) : 4
0 1 2 3 4 5
(i) : 5
0 1 2 3 4 5
(i) : 6
0 1 2 3 4 5
(i) : 7
0 1 2 3 4 5
(i) : 8
0 1 2 3 4 5
(i) : 9
0 1 2 3 4 5
```

### while문에서 break

```java
while (count > 0) {

    if (count == 5) {
        break;
    }
    System.out.print(count + " ");
    count--;
}
```

- output

```
10 9 8 7 6
```


#### 중첩문일 경우 해당 조건에서 내부 loop만 빠져나옴 (종료)

```java
int i = 10;
int j= 5;
while(i > 0 ) {
    System.out.println();
    System.out.println("(i) : "+ i);
    j=5;
    while (j > 0) {
        System.out.print(j + " ");
        if (j == 3) {
            break;
        }
        j--;
    }
    i--;
}
```

- output

```
(i) : 10
5 4 3
(i) : 9
5 4 3
(i) : 8
5 4 3
(i) : 7
5 4 3
(i) : 6
5 4 3
(i) : 5
5 4 3
(i) : 4
5 4 3
(i) : 3
5 4 3
(i) : 2
5 4 3
(i) : 1
5 4 3
```


## continue : 해당 조건은 skip   

### for문에서 continue

```java
for (int i = 0; i < 10; i++) {
    //해당 조건 건너뛰고 계속실행
    if (i==5) {
        continue;
    }
    System.out.print(i + " ");
}
```

- output

```
0 1 2 3 4 6 7 8 9
```

#### 중첩문일 경우 해당조건 건너 뛰고 실행

```java
for (int i = 0; i < 10; i++) {

    System.out.println();
    System.out.println("(i) : "  + i);
    //j==5일때는 건너뛰고 계속실행
    for (int j = 0; j < 10; j++) {
        System.out.print(j + " ");
        if (j==5) {
            continue;
        }

    }

}
```

- output

```
(i) : 0
0 1 2 3 4 5 6 7 8 9
(i) : 1
0 1 2 3 4 5 6 7 8 9
(i) : 2
0 1 2 3 4 5 6 7 8 9
(i) : 3
0 1 2 3 4 5 6 7 8 9
(i) : 4
0 1 2 3 4 5 6 7 8 9
(i) : 5
0 1 2 3 4 5 6 7 8 9
(i) : 6
0 1 2 3 4 5 6 7 8 9
(i) : 7
0 1 2 3 4 5 6 7 8 9
(i) : 8
0 1 2 3 4 5 6 7 8 9
(i) : 9
0 1 2 3 4 5 6 7 8 9
```

### while문에서 continue



```java
while (count > 0) {

    if (count == 5) {
        break;
    }
    System.out.print(count + " ");
    count--;
}
```

- output

```
10 9 8 7 6 4 3 2 1 0
```

#### 중첩문일 경우 해당조건 건너 뛰고 실행

```java
int i = 10;
int j= 5;
while(i > 0 ) {
    System.out.println();
    System.out.println("(i) : "+ i);
    j=5;
    while (j > 0) {
        System.out.print(j + " ");
        if (j == 3) {
            break;
        }
        j--;
    }
    i--;
}
```

- output

```
(i) : 10
5 4 2 1
(i) : 9
5 4 2 1
(i) : 8
5 4 2 1
(i) : 7
5 4 2 1
(i) : 6
5 4 2 1
(i) : 5
5 4 2 1
(i) : 4
5 4 2 1
(i) : 3
5 4 2 1
(i) : 2
5 4 2 1
(i) : 1
5 4 2 1

```

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-basic/src/loop/breakContinue.java)



---
#### references
<https://www.geeksforgeeks.org/decision-making-javaif-else-switch-break-continue-jump/>
<https://www.geeksforgeeks.org/break-statement-in-java/?ref=lbp>
<https://www.geeksforgeeks.org/continue-statement-in-java/>
