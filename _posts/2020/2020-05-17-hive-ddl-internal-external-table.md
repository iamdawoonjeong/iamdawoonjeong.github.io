---
layout: single
title: "[HIVE] HIVE DDL, Internal-External Table"
date: 2020-05-17 16:37:00.000000000 +09:00
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
permalink: "/hive-ddl-internal-external-table/"
---
## DDL(Data Definition Language)
하이브 DDL은 아래와 같이 지원되는데, 거의 SQL와 비슷하다.
- **CREATE** DATABASE/SCHEMA, TABLE, VIEW, FUNCTION, INDEX
- **DROP** DATABASE/SCHEMA, TABLE, VIEW, INDEX
- **TRUNCATE** TABLE
- **ALTER** DATABASE/SCHEMA, TABLE, VIEW
- **MSCK** REPAIR TABLE (or **ALTER** TABLE RECOVER PARTITIONS)
- **SHOW** DATABASES/SCHEMAS, TABLES, TBLPROPERTIES, VIEWS, PARTITIONS, FUNCTIONS, INDEX[ES], COLUMNS, CREATE TABLE
- **DESCRIBE** DATABASE/SCHEMA, table_name, view_name, materialized_view_name  

<!--excerpt_separator-->

## Internal VS External
SQL와 다르게 관리테이블, 외부 테이블라고 테이블이 분류 되어있다.  
테이블의 종류에 따라 사용할 수 있는 DDL도 다르고, 저장되는 위치, 데이터 파일 관리도 다르게 된다.  
주로 위험성이 낮은(?) 외부 테이블로 사용한다고 한다.


#### Internal(내부테이블) = Managed (관리테이블)
- HDFS의 기본디렉토리 /user/hive/warehouse/databasename.db/tablename/.
- 하이브의 테이블의 모든 데이터는 기본디렉토리에 저장
- 모든 테이블의 생명주기 관리
- 내부테이블이 삭제되면 외부테이블도 삭제됨


#### External (외부테이블)
- LOCATION 속성에서 외부테이블 명세
- 외부테이블은 메타데이터, 스키마 명세   
- 외부테이블 삭제되면, 메타테이블은 삭제되지만 데이터는 유지


#### Internal vs External   
- ARCHIVE/UNARCHIVE/TRUNCATE/MERGE/CONCATENATE 오직 내부 테이블에서만 작동  
- 외부테이블 삭제시, 데이터는 유지되고 오직 메타테이블은 삭제
- ACID는 오직 내부 테이블에서만 작동
- 쿼리결과 캐싱은 오직 내부 테이블에서만 작동
- 외부테이블은 RELY 제약조건만 허락함
- 일부 구체화된 뷰 기능은 오직 내부 테이블에서만 작동  

![hive-internal-external]({{ site.baseurl }}/assets/images/posts/2020/hive-tables-managed.png)


---
##### References
<https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL>  
<https://cwiki.apache.org/confluence/display/Hive/Managed+vs.+External+Tables>  
<https://docs.cloudera.com/HDPDocuments/HDP3/HDP-3.1.5/using-hiveql/content/hive_create_an_external_table.html>  
<https://data-flair.training/blogs/hive-internal-tables-vs-external-tables/>
