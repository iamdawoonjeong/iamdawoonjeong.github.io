---
layout: single
title: "[JAVA] Hash Map VS Hash Table, Hash set, Tree Map"
date: 2020-10-25 21:02:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- JAVA
tags:
- JAVA
- hash table
- hash map
- hash set
- tree set
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/java-hash_map-vs-hash_table/"
---
# Hash Map VS Hash Table, Hash set, Tree Map   

## Map
- Hash라고도 함
- 배열이나 사전과 관련있는 key-value 형태의 저장소
- elements와 관련된 값을 반환시키는 키를 통해 찾을 수 있음
- map 인터페이스 사용
- 자바 컬렉션 api일부


## HashMap
- HashMap클래스는 Hash Table을 자바로 구현한 것
- map인터페이스중 일반적으로 가장 많이 사용
- 클래스 구현에는 key-value 쌍을 나타내는 Entry라는 내부 클래스 존재
- 원소들은 Entry객체로 배열로 저장할 수 도 있고 배열대신 Entry객체의 리스트로 저장가능
- Map <K, V>, Cloneable 및 Serializable 인터페이스를 구현
- AbstractMap <K, V> 클래스를 확장
- java.util 패키지에 속함
- 단일 null key 와 여러 null value 허용
- 순서를 유지하지 않음
- key는 고유 한 요소
- 해싱 원칙에 따라 작동


## TreeMap
- TreeMap클래스는 map 인터페이스의 구현방법으로 구현하는데 **이진트리 자료구조 이용**
- 트리의 각 노드가 키-값 쌍이 됨
- 키를 정렬 가능한 순서에 따라 저장하기 때문에 hashCode 메서드는 전혀 사용되지 않음
- 균형맞춘 트리구조
- 검색.삭제.삽입같은 모든 동작은  항상 O(log n)의 처리성능 발휘
- TreeMap 클래스는 AbstractMap <K, V> 클래스를 확장 하고 NavigableMap <K, V> , Cloneable 및 Serializable 인터페이스를 구현
- TreeMap은 SortedMap의 예로  Red-Black tree에 의해 구현되며 이는 키의 순서가 정렬됨을 의미
- TreeMap에는 키에 기반한 값도 포함
- TreeMap은 키별로 정렬됨
- 고유 한 요소가 포함
- null key 허용 안 함
- null value는 허용
- 키는 오름차순
- object를 트리 구조에 저장


## Hash Map VS Hash Table   

| 구분 | Hash Map | Hash Table |
|:---:|:---|:---|
| null values | 하나의 null 키와 여러 개의 null 값을 허용 | null 키 또는 값을 허용하지 않음  |
| class | JDK 1.2 도입 | **legacy class** |
| 속도 | 빠름 | 느림 |
| traversal | Iterator (fail-fast)  | Enumerator(not fail-fast)[^1], Iterator |
| inherits  | AbstractMap 클래스를 상속  |  Dictionary 클래스를 상속  |
| synchronize | 안됨 | 동기화 됨 |


- **HashMap은 HashTable의 신버전 이므로 가능한 HashMap을 사용하는 것을 권유**


### 동기화 관련 추가 내용

- 동기화가 되지 않는 HashMap은 스레드로부터 안전하지 않으며 적절한 동기화 코드 없이는 여러 스레드간에 공유 할 수 없음.  Map m = Collections.synchronizedMap (hashMap);
- 동기화가 되는 Hastable은 스레드로부터 안전하며 많은 스레드와 공유 가능하면 비동기화는 할수 없음  


## Hash Map VS Hash Set

| 구분 | HashMap | HashSet |
|:---:|:---|:---|
| Definition | Map 인터페이스의 구현을 기반으로하는 hash table | 저장을 위해 해시 테이블을 사용하는 set[^2]컬렉션을 만듦  |
| Implementation | Map, Cloneable 및 Serializable 인터페이스를 구현 | Set, Cloneable, Serializable, Iterable 및 Collection 인터페이스를 구현 |
| Stores | **key-value** 쌍을 저장하고 매핑을 유지 | **객체**를 저장 |
| Duplicate values | key는 중복 안됨. value는 중복 허용 | 중복 안됨 |
| Null values | 하나의 null key 와 여러 개의 null value 허용  | null 값을 허용 |
| Method of insertion |  put ()  |  add () |
| Performance | 고유 key와 연결되어 있기 때문에 HashSet보다 빠름 | HashSet은 HashMap보다 느림 |
| The Number of objects | 하나의 객체만 생성 | put oeration 중에 생성 된 두 객체에 대해 하나의 키 와 하나의 값 생성됨  |
| Storing Mechanism | 내부적으로 **해싱을 사용** 하여 객체를 저장 |  내부적으로 **HashMap 객체를 사용**하여 객체를 저장 |
| Uses | 고유성을 유지하지 않을 때 선호 | 데이터의 고유성을 유지해야 할 때 사용|
| Example | {a-> 4, b-> 9, c-> 5} 여기서 a, b, c 는 키 이고 4, 9, 5 는 키와 관련된 값  | {6, 43, 2, 90, 4} 집합 |


## Hash Map VS Tree Map

### 유사점 ?
- HashMap 및 TreeMap 클래스는 Cloneable 및 Serializable 인터페이스를 구현
- 두 클래스 모두 AbstractMap <K, V> 클래스를 확장
- Map은 key-value 쌍을 저장하는 객체이며, 각 key는 고유하지만 값이 중복 가능
- 두 클래스 모두 key에서 value로 매핑을 나타냄
- 두 Map 모두 동기화 되지 않음
- put() 메서드를 사용 하여 요소를 추가
- Iterator는 Map이 어떤 식 으로든 수정되면 ConcurrentModificationException을 발생시킴


### 차이점?
#### 순서유지 여부
- **HashMap은 순서 유지 안함** : HashMap클래스에서는 순서가 보존 되지 않음   
- **TreeMap** 은 compareTo() 메서드 또는 TreeMap의 생성자에 설정된 비교기를 사용하여 **순서를 유지** : 컬렉션이 순서대로 저장되므로 전체 컬렉션을 반복해서 순회할 때 키의 순서가 보존



| 구분 | HashMap | TreeMap |
|:---:|:---|:---|
| Definition | Map 인터페이스의 해시 테이블 기반 구현 | Map 인터페이스의 트리 구조 기반 구현 |
| Interface Implements |  Map, Cloneable 및 Serializable 인터페이스를 구현 |  NavigableMap, Cloneable 및 Serializable 인터페이스를 구현 |
| Null Keys/ Values | 단일 null key와 여러 null value를 허용 | null key를 허용하지 않음. null value 허용 |
| Homogeneous/ Heterogeneous | key에 대해 정렬을 수행하지 않기 때문에 heterogeneous 요소를 허용 | 정렬로 인해 homogeneous 값을 키로 허용 |
| Performance |  get () 및 put ()과 같은 기본 작업에 대해 O(1)인 일정한 시간 성능을 제공하기 때문에 TreeMap보다 빠름 | add (), remove () 및 contains ()와 같은 대부분의 작업에 대해 O(logn의 성능을 제공하기 때문에 HashMap에 비해 느림 |
| Data Structure |  해시 테이블을 사용 | 내부적 으로 자체 균형 이진 검색 트리 인 Red-Black 트리를 사용 |
| Comparison Method | 사용 등호 () 의 방법 개체 키를 비교하는 클래스. Map 클래스의 equals () 메소드가이를 재정의 |  compareTo () 비교 키 방법. |
| Functionality |  get (), put (), KeySet () 등과 같은 기본 함수 만 포함 | tailMap (), firstKey (), lastKey (), pollFirstEntry (), pollLastEntry () 와 같은 함수를 포함하기 때문에 기능이 풍부 |
| Order of elements | 순서를 유지 안함 |  오름차순로 정렬 |
| Uses | HashMap은 정렬 된 순서로 key-value가 필요하지 않을 때 사용 | 정렬된 (오름차순) 순서로 key-value가 필요할 때 사용 |



----
#### references
<https://www.javatpoint.com/difference-between-hashset-and-hashmap>  
<https://www.javatpoint.com/difference-between-hashmap-and-hashtable>  
<https://www.javatpoint.com/difference-between-hashmap-and-treemap>  

----
#### annotation
[^1]: Enumeration은 Iterator의 구버전, Iterator의 접근성을 향상 시킨 것이 ListIterator
[^2]: 중복을 허용하지 않는 순서없는 객체들의 모음, hash set에서 순서를 유지하고자 한다면 LinkedHashSet클래스 사용
