---
layout: post
title: "[MySQL] 조인"
subtitle: "조인, join"
description: "조인은 관련 컬럼을 기반으로 여러 테이블의 데이터를 결합할 수 있는 기능입니다. 조인은 INNER JOIN, LEFT OUTER JOIN, RIGHT OUTER JOIN, FULL OUTER JOIN 등이 있습니다."
date: 2023-08-28 12:20:00 +0900
categories: db
tags: mysql
comments: true
---

# 조인(Join)

## 조인이란?

조인은 관련 컬럼을 기반으로 여러 테이블의 데이터를 결합할 수 있는 기능입니다. 조인은 `INNER JOIN`, `LEFT OUTER JOIN`, `RIGHT OUTER JOIN`, `FULL OUTER JOIN` 등이 있습니다.

## INNER JOIN(내부 조인)

`INNER JOIN`은 두 테이블이 조인을 하기 위해 사용된 컬럼의 값이 존재하는 행만 출력됩니다.

```sql
SELECT 컬럼1, ... FROM 기준테이블 [INNER] JOIN 참조테이블 ON 조인조건
```

**예시**

```sql
CREATE TABLE customers (
  customer_id INT PRIMARY KEY,
  customer_name VARCHAR(20),
  customer_age INT
);

INSERT INTO customers VALUES (1, '짱아', 1);
INSERT INTO customers VALUES (2, '짱구', 5);
INSERT INTO customers VALUES (3, '신형만', 35);
INSERT INTO customers VALUES (4, '봉미선', 29);

SELECT * FROM customers;
```

| customer_id | customer_name | customer_age |
| ----------- | ------------- | ------------ |
| 1           | 짱아          | 1            |
| 2           | 짱구          | 5            |
| 3           | 신형만        | 35           |
| 4           | 봉미선        | 29           |

```sql
CREATE TABLE orders (
  order_id INT PRIMARY KEY,
  order_price INT,
  customer_id INT
);

INSERT INTO orders VALUES (1, 2000, 1);
INSERT INTO orders VALUES (2, 3000, 2);
INSERT INTO orders VALUES (3, 4000, 3);

SELECT * FROM orders;
```

| order_id | order_price | customer_id |
| -------- | ----------- | ----------- |
| 1        | 2000        | 1           |
| 2        | 3000        | 2           |
| 3        | 4000        | 3           |

위의 두 테이블을 `cutomer_id` 컬럼 기반으로 내부 조인하면 다음과 같은 결과가 나옵니다.

```sql
SELECT * FROM customers INNER JOIN orders ON customers.customer_id = orders.customer_id;

-- 또는

SELECT * FROM customers JOIN orders ON customers.customer_id = orders.customer_id;
```

| customer_id | customer_name | customer_age | order_id | order_price | customer_id |
| ----------- | ------------- | ------------ | -------- | ----------- | ----------- |
| 1           | 짱아          | 1            | 1        | 2000        | 1           |
| 2           | 짱구          | 5            | 2        | 3000        | 2           |
| 3           | 신형만        | 35           | 3        | 4000        | 3           |

조인할 때 사용하는 컬럼명이 같다면 `USING` 문을 사용해 중복을 줄일 수 있습니다.

```sql
SELECT * FROM customers JOIN orders USING (customer_id);
```

| customer_id | customer_name | customer_age | order_id | order_price |
| ----------- | ------------- | ------------ | -------- | ----------- |
| 1           | 짱아          | 1            | 1        | 2000        |
| 2           | 짱구          | 5            | 2        | 3000        |
| 3           | 신형만        | 35           | 3        | 4000        |

## OUTER JOIN(외부 조인)

### LEFT OUTER JOIN

`LEFT OUTER JOIN`은 조인 조건이 되는 컬럼의 값이 있는 행만 반환하는 `INNER JOIN`과 달리 왼쪽(기준) 테이블의 모든 행도 함께 포함됩니다. 오른쪽(참조) 테이블에 일치하는 항목이 없으면 결과에는 NULL 값이 포함됩니다.

```sql
SELECT 컬럼1, ... FROM 기준테이블 LEFT [OUTER] JOIN 참조테이블 ON 조인조건
```

예시에 있는 두 테이블을 왼쪽 외부 조인하면 다음과 같은 결과가 나옵니다.

```sql
SELECT * FROM customers LEFT OUTER JOIN orders ON customers.customer_id = orders.customer_id;

-- 또는

SELECT * FROM customers LEFT JOIN orders ON customers.customer_id = orders.customer_id;
```

| customer_id | customer_name | customer_age | order_id | order_price | customer_id |
| ----------- | ------------- | ------------ | -------- | ----------- | ----------- |
| 1           | 짱아          | 1            | 1        | 2000        | 1           |
| 2           | 짱구          | 5            | 2        | 3000        | 2           |
| 3           | 신형만        | 35           | 3        | 4000        | 3           |
| 4           | 봉미선        | 29           | NULL     | NULL        | NULL        |

### RIGHT OUTER JOIN

`RIGHT OUTER JOIN`은 오른쪽(참조) 테이블의 모든 행이 포함됩니다.

```sql
SELECT 컬럼1, ... FROM 기준테이블 RIGHT [OUTER] JOIN 참조테이블 ON 조인조건
```

예시에 있는 두 테이블을 오른쪽 외부 조인하면 다음과 같은 결과가 나옵니다.

```sql
SELECT * FROM customers RIGHT OUTER JOIN orders ON customers.customer_id = orders.customer_id;

-- 또는

SELECT * FROM customers RIGHT JOIN orders ON customers.customer_id = orders.customer_id;
```

| customer_id | customer_name | customer_age | order_id | order_price | customer_id |
| ----------- | ------------- | ------------ | -------- | ----------- | ----------- |
| 1           | 짱아          | 1            | 1        | 2000        | 1           |
| 2           | 짱구          | 5            | 2        | 3000        | 2           |
| 3           | 신형만        | 35           | 3        | 4000        | 3           |

## CROSS JOIN(교차 조인)

`CROSS JOIN`은 두 테이블의 가능한 모든 행의 조합을 결합하는데 사용되는 조인입니다.

```sql
SELECT 컬럼1, ... FROM 기준테이블 CROSS JOIN 참조테이블;
```

예시의 두 테이블을 교차 조인하면 다음과 같은 결과가 나옵니다.

```sql
SELECT * FROM customers CROSS JOIN orders;
```

| customer_id | customer_name | customer_age | order_id | order_price | customer_id |
| ----------- | ------------- | ------------ | -------- | ----------- | ----------- |
| 1           | 짱아          | 1            | 3        | 4000        | 3           |
| 1           | 짱아          | 1            | 2        | 3000        | 2           |
| 1           | 짱아          | 1            | 1        | 2000        | 1           |
| 2           | 짱구          | 5            | 3        | 4000        | 3           |
| 2           | 짱구          | 5            | 2        | 3000        | 2           |
| 2           | 짱구          | 5            | 1        | 2000        | 1           |
| 3           | 신형만        | 35           | 3        | 4000        | 3           |
| 3           | 신형만        | 35           | 2        | 3000        | 2           |
| 3           | 신형만        | 35           | 1        | 2000        | 1           |
| 4           | 봉미선        | 29           | 3        | 4000        | 3           |
| 4           | 봉미선        | 29           | 2        | 3000        | 2           |
| 4           | 봉미선        | 29           | 1        | 2000        | 1           |
