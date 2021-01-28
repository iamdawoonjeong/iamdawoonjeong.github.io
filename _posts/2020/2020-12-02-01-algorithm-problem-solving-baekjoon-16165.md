---
layout: single
title: "[Problem Solving - Baekjoon] 16165 걸그룹 마스터 준석이"
date: 2020-12-02 22:10:00.000000000 +09:00
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
- baekjoon
- implementation
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-16165/"
---
# [Baekjoon Online Judge] 16165 걸그룹 마스터 준석이

## 문제
정우는 소문난 걸그룹 덕후이다. 정우의 친구 준석이도 걸그룹을 좋아하지만 이름을 잘 외우지 못한다는 문제가 있었다. 정우는 친구를 위해 걸그룹 개인과 팀의 이름을 검색하여 외우게 하는 퀴즈 프로그램을 만들고자 한다.

### 입력
첫 번째 줄에는 총 입력 받을 걸그룹의 수 N(0 < N < 100)과 맞혀야 할 문제의 수 M(0 < M < 100)을 입력받는다.

두 번째 줄부터는 각 걸그룹마다 팀의 이름, 걸그룹의 인원 수, 멤버의 이름을 한 줄씩 차례대로 입력받는다. 팀과 멤버의 이름은 최대 100글자이며, 모든 글자는 알파벳 소문자이다. 하나의 걸그룹이나 서로 다른 두 걸그룹에 이름이 같은 두 멤버가 있는 경우는 없다.

그 다음 줄부터는 M개의 퀴즈를 입력받는다. 각각의 퀴즈는 두 줄로 이루어져 있으며, 팀의 이름이나 멤버의 이름이 첫 줄에 주어지고 퀴즈의 종류를 나타내는 0 또는 1이 두 번째 줄에 주어진다. 퀴즈의 종류가 0일 경우 팀의 이름이 주어지며, 1일 경우 멤버의 이름이 주어진다.

### 출력
첫 번째 줄부터 차례대로 퀴즈에 대한 답을 출력한다. 퀴즈의 종류가 0일 경우 해당 팀에 속한 멤버의 이름을 사전순으로 한 줄에 한 명씩 출력한다. 퀴즈의 종류가 1일 경우 해당 멤버가 속한 팀의 이름을 출력한다.

### 예제

- input

```java
3 4
twice
9
jihyo
dahyeon
mina
momo
chaeyoung
jeongyeon
tzuyu
sana
nayeon
blackpink
4
jisu
lisa
rose
jenny
redvelvet
5
wendy
irene
seulgi
yeri
joy
sana
1
wendy
1
twice
0
rose
1
```

- output

```java
twice
redvelvet
chaeyoung
dahyeon
jeongyeon
jihyo
mina
momo
nayeon
sana
tzuyu
blackpink
```

### 분류
- 구현

## 풀이

### 문제 파악

- 걸그룹명 -  멤버수 - 멤버이름을 입력받고
- 문제 0 걸그룹명을 말하면 멤버수 오름차순 출력
- 문제 1 멤버이름 말하면 걸그룹명 출력


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem16165/Main.java)

- hashmap 으로 팀명 - 멤버명 받아서 구현
- hashmap  value 로 key 를 찾으려다 보다 for 문이 두번 사용되고 소스 전체로 봤을때 for문이 3번이나 됨

```java
HashMap<String, String[]> map = new HashMap<String, String[]>();

//걸그룹 입력받기
for (int i = 0; i < N; i++) {

    String team = br.readLine();  //팀의이름
    int number = Integer.parseInt(br.readLine()); //걸그룹 인원수

    String[] names = new String[number];
    for (int j = 0; j < number; j++) {
        names[j] = br.readLine();  //멤버들 이름

    }

    Arrays.sort(names);
    map.put(team, names);
}

//문제 맞추기
for (int i = 0; i < M; i++) {
     String problem = br.readLine();
     int type = Integer.parseInt(br.readLine());

    //팀명제시 : 멤버이름 순차적
    if (type == 0) {

        String[] resultNames = map.get(problem);
        for (int j = 0; j < resultNames.length; j++) {
            System.out.println(resultNames[j]);
        }

    }else if (type == 1) {
       // 멤버이름 제시 : 팀명 맞추기
        String resultTeam = "";

        //hashmap value로 key찾기
        for (String key : map.keySet()) {
            String[] names = map.get(key);
            for (String str : names) {
                if (str.equals(problem)){
                    resultTeam = key;
                    System.out.println(resultTeam);
                }
            }

        }
    }
}// end for
```

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem16165/Main2.java)

- hashmap 으로 팀명 - 멤버명 받아서 구현
- 두군데 받아야하지만, 찾을때는 확실히 간단

```java
//걸그룹 입력받기
for (int i = 0; i < N; i++) {

    String team = br.readLine();  //팀의이름
    int number = Integer.parseInt(br.readLine()); //걸그룹 인원수

    String[] names = new String[number];
    for (int j = 0; j < number; j++) {
        names[j] = br.readLine();  //멤버들 이름
        members.put(names[j], team);
    }

    Arrays.sort(names);
    teams.put(team, names);
}

//문제맞추기
for (int i = 0; i < M; i++) {
    String problem = br.readLine();
    int type = Integer.parseInt(br.readLine());

   //팀명제시 : 멤버이름 순차적
   if (type == 0) {
       String[] resultNames = teams.get(problem);
       for (int j = 0; j < resultNames.length; j++) {
           System.out.println(resultNames[j]);
       }
   }else if (type == 1) {
      // 멤버이름 제시 : 팀명 맞추기
       String resultTeam = members.get(problem);
       System.out.println(resultTeam);
   }

}

```


### 결과

- 구현의 차이일뿐 속도, 메모리는 둘 다 비슷함 (편한거 쓰면 됨)

| 구분 | for 3개 | hashmap 두개 |
|:----:|:----:|:----:|
| 메모리(KB) | 14325 | 14428 |
| 시간(ms) | 132 | 136 |
| 코드길이(B) | 2284 | 1983 |


---

#### references
<https://www.acmicpc.net/problem/16165>
