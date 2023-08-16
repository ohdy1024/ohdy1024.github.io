---
layout: post
title: "[MySQL] SELECT 문 (데이터 조회하기)"
subtitle: "SELECT, 데이터 조회"
date: 2023-08-16 13:04:00 +0900
categories: db
tags: mysql
comments: true
---

# SELECT 문 (데이터 조회)

## SELECT

### SELECT

`SELECT` 문은 데이터베이스의 테이블에서 데이터를 조회하는 SQL 문입니다.

```sql
SELECT 컬럼1, 컬럼2, ... FROM 테이블명;
```

### WHERE

`WHERE` 절은 `SELECT` 문에서 특정 조건을 충족하는 데이터를 조회합니다. 다양한 연산자를 함께 사용하여 더 자세하게 데이터를 조회할 수 있습니다.

**기본 문법**

```sql
SELECT 컬럼1, ... FROM 테이블명 WHERE 조건문;
```

**컬럼 값이 a보다 큰 데이터 조회**

```sql
SELECT * FROM 테이블명 WHERE 컬럼 > a;
```

**컬럼 값이 a 또는 b와 일치하는 데이터 조회**

```sql
SELECT * FROM 테이블명 WHERE 컬럼 = a OR 컬럼 = b;

-- OR

SELECT * FROM 테이블명 WHERE 컬럼 IN (a, b);
```

**컬럼 값이 a ~ b 사이의 값을 가지는 데이터 조회**

```sql
SELECT * FROM 테이블명 WHERE 컬럼 >= a AND 컬럼 <= b;

-- OR

SELECT * FROM 테이블명 WHERE 컬럼 BETWEEN a AND b;
```

**컬럼 값이 a로 시작하는 데이터 조회**

```sql
SELECT * FROM 테이블명 WHERE 컬럼 LIKE 'a%';
```

**컬럼 값이 a로 시작하는 두 글자인 데이터 조회**

```sql
SELECT * FROM 테이블명 WHERE 컬럼 LIKE 'a_';
```

### ORDER BY

`ORDER BY` 절은 쿼리 결과를 특정 순서로 출력할 수 있습니다.

```sql
SELECT 컬럼1, 컬럼2, ... FROM 테이블명 ORDER BY 컬럼1 [ASC | DESC], 컬럼2 [ASC | DESC], ...;
```

`WHERE` 절과 함께 사용하면 순서를 주의해야 합니다. `ORDER BY` 절은 `WHERE` 절 뒤에 나와야 합니다.

```sql
SELECT 컬럼1, 컬럼2, ... FROM 테이블명 WHERE 조건문 ORDER BY 컬럼1 [ASC | DESC], ...;
```

**컬럼1을 기준으로 오름차순 정렬**

```sql
SELECT * FROM 테이블명 ORDER BY 컬럼1 ASC;
```

**컬럼1을 기준으로 내림차순 정렬**

```sql
SELECT * FROM 테이블명 ORDER BY 컬럼1 DESC;
```

### LIMIT

`LIMIT` 절은 쿼리에서 반환되는 행의 수를 제한하는데 사용됩니다. `LIMIT` 절은 첫 번째 데이터를 0번으로 시작하며, 0번부터 조회할 경우 생략이 가능합니다.

```sql
SELECT 컬럼1, 컬럼2, ... FROM 테이블명 LIMIT 시작, 개수

-- OR

SELECT 컬럼1, 컬럼2, ... FROM 테이블명 LIMIT 개수 OFFSET 시작;
```

**첫 번째 데이터를 포함하는 세 개의 데이터 출력**

```sql
SELECT * FROM 테이블명 LIMIT 3;

-- OR

SELECT * FROM 테이블명 LIMIT 0, 3;

-- OR

SELECT * FROM 테이블명 LIMIT 3 OFFSET 0;
```

### DISTINCT

`DISTINCT` 절은 쿼리 결과에서 중복 데이터를 1개만 남깁니다.

```sql
SELECT DISTINCT 컬럼1, ... FROM 테이블명;
```

### GROUP BY

`GROUP BY` 절은 하나 이상의 컬럼을 기반으로 행을 그룹화하는데 사용됩니다. `GROUP BY` 절은 보통 집계 함수와 함께 사용합니다.

```sql
SELECT 컬럼1, ..., 집계 함수(컬럼) FROM 테이블명 GROUP BY 컬럼1, ...;
```

**컬럼1을 그룹화 후, 컬럼1 그룹이 컬림2을 가지고 있는 개수**

```sql
SELECT 컬럼1, COUNT(컬럼2) FROM 테이블명 GROUP BY 컬럼1;
```

### HAVING

`HAVING` 절은 `GROUP BY` 절과 함께 사용되며, 집계된 값에 조건을 적용하여 쿼리 결과를 필터링합니다. `WHERE` 절은 행이 그룹화되기 전에 행을 필터링하는 반면 `HAVING` 절은 `GROUP BY` 작업의 결과를 필터링합니다.

```sql
SELECT 컬럼1, ..., 집계 함수(컬럼) FROM 테이블명 GROUP BY 컬럼1, ... HAVING 조건문;
```

**컬럼1을 그룹화 후, 컬럼1 그룹이 컬림2을 가지고 있는 개수가 두 개 이상일 경우**

```sql
SELECT 컬럼1, COUNT(컬럼2) FROM 테이블명 GROUP BY 컬럼1 HAVING COUNT(컬럼2) >= 2;
```
