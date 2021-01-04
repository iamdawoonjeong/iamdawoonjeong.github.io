---
layout: single
title: "[Problem Solving - Baekjoon] 1759 암호 만들기"
date: 2020-11-29 14:45:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Problem Solving
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
permalink: "/algorithm-problem-solving-baekjoon-1759/"
---
# [Baekjoon Online Judge] 1759 암호 만들기

## 문제
바로 어제 최백준 조교가 방 열쇠를 주머니에 넣은 채 깜빡하고 서울로 가 버리는 황당한 상황에 직면한 조교들은, 702호에 새로운 보안 시스템을 설치하기로 하였다. 이 보안 시스템은 열쇠가 아닌 암호로 동작하게 되어 있는 시스템이다.

암호는 서로 다른 L개의 알파벳 소문자들로 구성되며 최소 한 개의 모음(a, e, i, o, u)과 최소 두 개의 자음으로 구성되어 있다고 알려져 있다. 또한 정렬된 문자열을 선호하는 조교들의 성향으로 미루어 보아 암호를 이루는 알파벳이 암호에서 증가하는 순서로 배열되었을 것이라고 추측된다. 즉, abc는 가능성이 있는 암호이지만 bac는 그렇지 않다.

새 보안 시스템에서 조교들이 암호로 사용했을 법한 문자의 종류는 C가지가 있다고 한다. 이 알파벳을 입수한 민식, 영식 형제는 조교들의 방에 침투하기 위해 암호를 추측해 보려고 한다. C개의 문자들이 모두 주어졌을 때, 가능성 있는 암호들을 모두 구하는 프로그램을 작성하시오.

### 입력
첫째 줄에 두 정수 L, C가 주어진다. (3 ≤ L ≤ C ≤ 15) 다음 줄에는 C개의 문자들이 공백으로 구분되어 주어진다. 주어지는 문자들은 알파벳 소문자이며, 중복되는 것은 없다.

### 출력
각 줄에 하나씩, 사전식으로 가능성 있는 암호를 모두 출력한다.

### 예제

- input

```java
4 6
a t c i s w
```

- output

```java
acis
acit
aciw
acst
acsw
actw
aist
aisw
aitw
astw
cist
cisw
citw
istw
```

### 분류
- 브루트포스 알고리즘
- 백트래킹
- dfs

## 풀이

### 문제 파악
- l개의 문자들사이에서 c 개의 **조합**
- 최소 한 개의 모음(a, e, i, o, u), 최소 두 개의 자음으로 구성

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1759/Main.java)


- 암호를 사전순으로 출력해야 하기 때문에 정렬

```java   
Arrays.sort(arr);

dfs(l, arr, "" , 0);
```

- dfs 로 조합찾기

```java
public static void dfs(int l, String[] arr, String password, int index) {

	//길이가 l인 모든 조합 찾기  
	if (password.length() == l) {
	    if (check(password)) {
	        System.out.println(password);
	    }
	    return;
	}

	if (index >= arr.length) {
	    return;
	}

	dfs(l, arr, password+arr[index], index+1);
	dfs(l, arr, password, index+1);
}
```

- 모음은 최소 1개이상 들어가야 하는 조건 체크

```java
public static boolean check(String password) {

int vowel=0; //모음
int consonant=0;//자음
for(char arr : password.toCharArray()) {
    if(arr== 'a' || arr=='e' || arr=='i' || arr=='o' || arr=='u') {
        vowel++;
    }
    else {
        consonant++;
    }
}

// 모음 갯수 확인
return vowel>=1 && consonant>=2;
}

```

---

#### references
<https://www.acmicpc.net/problem/1759>
