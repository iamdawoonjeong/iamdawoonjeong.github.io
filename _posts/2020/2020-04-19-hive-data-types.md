---
layout: single
title: "[HIVE] HIVE 데이터 타입 (primitive, complex)"
date: 2020-04-19 09:00:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- HIVE
tags:
- database
- HADOOP
- HIVE
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/hive-data-types/"
---

하이브 데이터 타입 중에서 primitive types, complex types에 대해서 정리해보겠다.  
primitive types은 sql을 알고 있다면 크게 어려울 것이 없지만, complex types 이라는 것이 sql에서는 지원하지 않았던 부분이다.  
말 그대로 복잡한 타입인데 array, map 을 들었을때는 java와 비슷하지 않을까 했고, struct 를 들었을 때는 C와 비슷하지 않을까 생각했다.  
다행히 찾아보니 맞는 것 같다.  array, map은 java와 유사하다고 설명되어있고, struct는 c와 유사하다.  
갈수록 지원해주는 데이터의 형태가 다양해 지면서 표현할 수 있는 범위(?)가 넓어지는 것이 신기할 따름이다.
<!--excerpt_separator-->


## Primitive Types
기존 sql 을 썼던 사람이라면 누구나가 쉽게 익힐 수 있는 타입들  


### Numeric Types
- TINYINT : 1-byte signed integer,  -128 ~ 127
- SMALLINT : 2-byte signed integer,  -32,768 ~ 32,767
- INT/INTEGER : 4-byte signed integer,  -2,147,483,648 ~ 2,147,483,647
- BIGINT : 8-byte signed integer,  -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807
- FLOAT : 4-byte single precision floating point number
- DOUBLE : 8-byte double precision floating point number
- DOUBLE PRECISION (alias for DOUBLE)
- DECIMAL
- NUMERIC (same as DECIMAL)

### Date/Time Types
- TIMESTAMP
- DATE
- INTERVAL

### String Types
- STRING
- VARCHAR
- CHAR

### Misc Types
- BOOLEAN
- BINARY


## Complex Types

### Arrays
- 자바에서의 array 와 비슷한 방식으로 쓰임

```sql
ARRAY<data_type>
```

- index 사용하여 접근가능

```sql
-- array(‘Data’,’Flair’) 값이 있을 경우, 값 Flair를 인덱스로 접근가능
SELECT column_name[1] FROM table_name;
```

### Maps
- 자바에서의 map과 비슷한 방식으로 쓰임
- <key,value>가 한 쌍
- key는 중복 될 수 없음

```sql
MAP<primitive_type, data_type>
```

- key 값으로 접근가능

```sql
-- map(‘first’, ‘John’, ‘last’, ‘Deo’)값이 있을 경우, 값 'John'을 key 값으로 접근가능
SELECT column_name[‘first’] FROM table_name;
```


### Structs
- C의 STRUCT와 비슷한 방식으로 쓰임

```sql
STRUCT<col_name : data_type [COMMENT col_comment], ...>
```

- column_name.field_name 으로 접근 가능

```sql
-- STRUCT {c1 INTEGER; c2 INTEGER} 값이 있을 경우, 컬럼 이름뿐 아니라 각 필드로도 접근 가능
SELECT column_name.c1, column_name.c2 FROM table_name;
```

### Union Types
- C의 UNION와 비슷한 방식으로 쓰임
- 자주사용되지는 않는 타입
- 다른 여러종류의 타입들이 합쳐진 형식

```sql
UNIONTYPE<int, double, array<string>, struct<a:int,b:string>>
```

- 아래와 같이 다양한 형태로 값이 존재
```sql
{0:1}
{1:2.0}
{2:["three","four"]}
{3:{"a":5,"b":"five"}}
{2:["six","seven"]}
{3:{"a":8,"b":"eight"}}
{0:9}
{1:10.0}
```


---
#### References
<https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Types>  
<https://www.tutorialspoint.com/hive/hive_data_types.htm>  
<https://wikidocs.net/23556>  
<https://data-flair.training/blogs/hive-data-types/>
