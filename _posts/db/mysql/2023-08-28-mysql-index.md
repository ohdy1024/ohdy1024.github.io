---
layout: post
title: "[MySQL] 인덱스"
subtitle: "인덱스"
description: "MySQL에서는 키(KEY)와 인덱스(INDEX)를 같은 의미로 사용합니다. 인덱스는 데이터 검색을 빠르게 하기 위해서 사용됩니다. 인덱스가 없으면 데이터베이스 엔진은 원하는 데이터를 찾기 위해 테이블의 전체 데이터를 검색해야 합니다. 인덱스는 테이블의 모든 데이터를 검사하지 않고도 관련 데이터를 찾아내기에 쿼리 실행 시간이 빨라집니다."
date: 2023-08-28 12:20:00+0900
categories: db
tags: mysql
comments: true
---

# 인덱스

## 인덱스란?

MySQL에서는 키(KEY)와 인덱스(INDEX)를 같은 의미로 사용합니다. 인덱스는 데이터 검색을 빠르게 하기 위해서 사용됩니다. 인덱스가 없으면 데이터베이스 엔진은 원하는 데이터를 찾기 위해 테이블의 전체 데이터를 검색해야 합니다. 인덱스는 테이블의 모든 데이터를 검사하지 않고도 관련 데이터를 찾아내기에 쿼리 실행 시간이 빨라집니다.

인덱스의 단점으로는 인덱스를 저장하기 위해 추가 공간이 필요하기 때문에 저장 공간이 늘어날 수 있습니다. 또 다른 단점은 데이터 변경 작업(삽입, 수정, 삭제)이 자주 일어날 경우 성능이 저하될 수 있습니다.

## 인덱스 생성

### 기본 키(Primary Key) 생성

기본 키는 테이블 내에서 각 행이 고유한지 식별하는 데 사용됩니다. 한 테이블에 한 개만 존재할 수 있습니다. 일반적으로 기본 키는 테이블을 생성할 때 같이 생성합니다.

'컬럼1'을 기본 키로 가지는 테이블을 생성하려면 아래와 같이 작성하면 됩니다.

```sql
CREATE TABLE 테이블명 (
  컬럼1 데이터타입 PRIMARY KEY,
  ...
);

-- 또는

CREATE TABLE 테이블명 (
  컬럼1 데이터타입,
  ...,
  PRIMARY KEY (컬럼1)
);
```

인덱스를 조회하고 싶다면 `SHOW INDEX` 문을 사용하면 됩니다. 기본 키는 `Key_name` 필드의 값이 'PRIMARY'로 나옵니다.

```sql
CREATE TABLE PERSON (
  id INT PRIMARY KEY
);

SHOW INDEX FROM PERSON;
```

| Table  | Non_unique | Key_name | Seq_in_index | Column_name | …   |
| ------ | ---------- | -------- | ------------ | ----------- | --- |
| person | 0          | PRIMARY  | 1            | id          | …   |

### 보조 키(세컨더리 인덱스, Secondary key) 생성하기

보조 키는 기본 키를 제외한 나머지 인덱스입니다. 보조 키는 고유 인덱스, 비고유 인덱스 등이 있습니다.

**고유 인덱스**는 기본 키와 유사하게 고유성을 가지고 있지만 NULL값을 허용합니다. `UNIQUE` 제약 조건을 사용하거나 `CREATE UNIQUE INDEX` 문을 사용하여 생성합니다.

```sql
CREATE TABLE PERSON (
  id INT PRIMARY KEY,
  age INT UNIQUE
);

SHOW INDEX FROM PERSON;
```

| Table  | Non_unique | Key_name | Seq_in_index | Column_name | …   | Null | …   |
| ------ | ---------- | -------- | ------------ | ----------- | --- | ---- | --- |
| person | 0          | PRIMARY  | 1            | id          | …   |      | …   |
| person | 0          | age      | 1            | age         | …   | YES  | …   |

고유 인덱스를 조회하면 `Non_unique` 필드 값은 0, `Null` 필드는 'YES' 값을 가집니다.

**비고유 인덱스**는 중복된 값을 가질 수 있으며 NULL 값도 허용하는 인덱스입니다. `CREATE INDEX` 문을 사용하여 생성합니다. 인덱스를 조회하면 고유 인덱스와 다르게 `Non_unique` 필드의 값이 1로 나타납니다.

```sql
CREATE TABLE PERSON (
  id INT PRIMARY KEY,
  age INT UNIQUE,
  name VARCHAR(20)
);

CREATE INDEX  name ON PERSON (name);

SHOW INDEX FROM PERSON;
```

| Table  | Non_unique | Key_name | Seq_in_index | Column_name | …   | Null | …   |
| ------ | ---------- | -------- | ------------ | ----------- | --- | ---- | --- |
| person | 0          | PRIMARY  | 1            | id          | …   |      | …   |
| person | 0          | age      | 1            | age         | …   | YES  | …   |
| person | 1          | name     | 1            | name        | …   | YES  | …   |

## 인덱스 스캔

### 인덱스 레인지 스캔

인덱스 레인지 스캔은 검색해야 할 인덱스의 범위가 결정됐을 때 사용하는 방식입니다. 실행 계획을 확인하는 방법은 `EXPLAIN` 문을 실행하고자하는 쿼리 앞에 붙여 실행하면 됩니다. `type` 필드 값이 'range'일 경우 인덱스 레인지 스캔을 사용하여 데이터를 검색한 것입니다.

```sql
CREATE TABLE PERSON (
  id INT PRIMARY KEY AUTO_INCREMENT,
  age INT,
  name VARCHAR(20),
  index age_name (age, name)
);

INSERT INTO person (age, name) VALUES (5, '짱구');
INSERT INTO person (age, name) VALUES (1, '짱아');
INSERT INTO person (age, name) VALUES (35, '신형만');
INSERT INTO person (age, name) VALUES (29, '봉미선');

EXPLAIN SELECT * FROM person WHERE age > 5;
```

| id  | select_type | table  | partitions | type  | possible_keys | key      | key_len | ref  | rows | filtered | Extra                    |
| --- | ----------- | ------ | ---------- | ----- | ------------- | -------- | ------- | ---- | ---- | -------- | ------------------------ |
| 1   | SIMPLE      | person | NULL       | range | age_name      | age_name | 5       | NULL | 2    | 100      | Using where; Using index |

### 인덱스 풀 스캔

인덱스 풀 스캔은 인덱스를 사용하지만 인덱스 레인지 스캔과는 달리 인덱스를 처음부터 끝까지 모두 읽는 방식입니다. 쿼리의 조건절에 사용된 컬럼이 인덱스의 첫 번째 컬럼이 아닌 경우 인덱스 풀 스캔 방식을 사용합니다. 인덱스 풀 스캔은 `EXPLAIN` 문을 사용하면 `type` 값이 'index'로 나옵니다.

```sql
CREATE TABLE PERSON (
  id INT PRIMARY KEY AUTO_INCREMENT,
  age INT,
  name VARCHAR(20),
  index age_name (age, name)
);

INSERT INTO person (age, name) VALUES (5, '짱구');
INSERT INTO person (age, name) VALUES (1, '짱아');
INSERT INTO person (age, name) VALUES (35, '신형만');
INSERT INTO person (age, name) VALUES (29, '봉미선');

EXPLAIN SELECT * FROM person WHERE name LIKE '짱_';
```

| id  | select_type | table  | partitions | type  | possible_keys | key      | key_len | ref  | rows | filtered | Extra                    |
| --- | ----------- | ------ | ---------- | ----- | ------------- | -------- | ------- | ---- | ---- | -------- | ------------------------ |
| 1   | SIMPLE      | person | NULL       | index | age_name      | age_name | 88      | NULL | 4    | 25       | Using where; Using index |
