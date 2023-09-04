---
layout: post
title: "[MySQL] 내장 함수"
subtitle: "함수, 내장 함수, 문자열 함수, 집계 함수, 흐름 제어 함수, 수학 함수, 날짜 및 시간 함수"
description: "MySQL은 데이터에 대해 다양한 작업을 수행할 수 있도록 내장 함수를 제공합니다. MySQL의 내장 함수는 문자열 함수, 집계 함수, 흐름 제어 함수, 수학 함수, 날짜 및 시간 함수 등이 있습니다."
date: 2023-08-18 22:54:00+0900
categories: db
tags: mysql
comments: true
---

# 내장 함수

### 내장 함수

MySQL은 데이터에 대해 다양한 작업을 수행할 수 있도록 내장 함수를 제공합니다.

### 문자열 함수

MySQL은 문자열을 조작하고 작업할 수 있는 다양한 문자열 함수를 제공합니다.

#### CONCAT

`CONCAT()` 함수는 두 개 이상의 문자열을 연결합니다.

```sql
CONCAT(문자열1, 문자열2, ...);
```

```sql
SELECT CONCAT('짱구는', ' ', '못말려') AS RESULT;
-- 출력: 짱구는 못말려
```

#### CONCAT_WS

`CONCAT_WS()` 함수는 지정된 기호로 문자열을 연결합니다.

```sql
CONCAT_WS(구분 기호, 문자열1, 문자열2, ...);
```

```sql
SELECT CONCAT_WS('-', '2023', '08', '18') AS date;
-- 출력: 2023-08-18
```

#### SUBSTRING

`SUBSTRING()` 함수는 문자열에서 하위 문자열을 추출합니다.

```sql
SUBSTRING(문자열, 시작);
SUBSTRING(문자열, 시작, 길이);
```

```sql
SELECT SUBSTRING('짱구는 못말려', 5) AS RESULT;
-- 출력: 못말려
```

```sql
SELECT SUBSTRING('짱구는 못말려', 1, 2) AS RESULT;
-- 출력: 짱구
```

#### LEFT, RIGHT

`LEFT()`, `RIGHT()` 함수는 문자열의 왼쪽 또는 오른쪽에서 지정된 수의 문자를 추출합니다.

```sql
LEFT(문자열, 길이);
RIGHT(문자열, 길이);
```

```sql
SELECT LEFT('짱구는 못말려', 3) AS RESULT;
-- 출력: 짱구는
```

```sql
SELECT RIGHT('짱구는 못말려', 3) AS RESULT;
-- 출력: 못말려
```

#### UPPER, LOWER

`UPPER()`와 `LOWER()` 함수는 문자열을 대문자 또는 소문자로 변환합니다.

```sql
UPPER(문자열);
LOWER(문자열);
```

```sql
SELECT UPPER('Hello') AS RESULT;
-- 출력: HELLO
```

```sql
SELECT LOWER('Hello') AS RESULT;
-- 출력: hello
```

#### LENGTH, CHAR_LENGTH

`LENGTH()` 함수는 문자열의 바이트 길이를 반환합니다. `CHAR_LENGTH()` 함수는 문자열의 길이를 반환합니다.

```sql
LENGTH(문자열);
CHAR_LENGTH(문자열);
```

```sql
SELECT LENGTH('짱구는 못말려') AS RESULT;
-- 출력: 19
```

```sql
SELECT CHAR_LENGTH('짱구는 못말려') AS RESULT;
-- 출력: 7
```

#### TRIM

`TRIM()` 함수는 문자열의 좌우측 공백을 제거합니다.

```sql
TRIM(문자열);
```

```sql
SELECT TRIM('   짱구는 못말려    ') AS RESULT;
-- 출력: 짱구는 못말려
```

#### REPLACE

`REPLACE()` 함수는 문자열을 부분 교체합니다.

```sql
REPLACE(문자열, 기존 문자열, 교체 문자열);
```

```sql
SELECT REPLACE('짱구는 못말려', '짱구는', '짱아도') AS RESULT;
```

#### LOCATE

`LOCATE()` 함수는 다른 문자열 내에서 하위 문자열을 검색하고 해당 위치를 반환합니다.

```sql
LOCATE(검색 문자열, 문자열);
```

```sql
SELECT LOCATE('말려', '짱구는 못말려') AS RESULT;
-- 출력: 6
```

#### REPEAT

`REPEAT()` 함수는 지정된 횟수만큼 문자열을 반복합니다.

```sql
REPEAT(문자열, 반복 횟수);
```

```sql
SELECT REPEAT('부리 ', 3) AS RESULT;
-- 출력: 부리 부리 부리
```

### 집계함수

#### SUM

`SUM()` 함수는 컬럼 값의 합계를 계산합니다.

```sql
SELECT SUM(컬럼) FROM 테이블명;
```

#### AVG

`AVG()` 함수는 컬럼 값의 평균을 계산합니다.

```sql
SELECT AVG(컬럼) FROM 테이블명;
```

#### COUNT

`COUNT()` 함수는 레코드의 수를 계산합니다.

```sql
SELECT COUNT(컬럼) FROM 테이블명;
```

#### MIN, MAX

`MIN()`, `MAX()` 함수는 컬럼에서 최솟값, 최댓값을 검색합니다.

```sql
SELECT MIN(컬럼) FROM 테이블명; -- 최솟값
SELECT MAX(컬럼) FROM 테이블명; -- 최댓값
```

### 날짜 및 시간 함수

날짜 및 시간 함수는 데이터베이스 내에서 날짜 및 시간 값 작업을 위한 기능을 제공합니다.

#### DATE

`DATE()` 함수는 `DATE` 또는 `DATETIME` 표현식의 날짜 부분을 추출합니다.

```sql
SELECT DATE('2023-08-18') AS RESULT;
-- 출력: '2023-08-18'

SELECT DATE('2023-08-18 14:30:00') AS RESULT;
-- 출력: '2023-08-18'
```

#### TIMESTAMP

`TIMESTAMP()` 함수는 단일 인수 또는 두 개의 인수를 받으며 `TIMESTAMP` 값을 반환합니다. 단일 인수로는 `DATE` 또는 `DATETIME` 표현식을 인수로 받습니다. 두 개의 인수는 첫 번째로 `DATE` 또는 `DATETIME` 표현식을 인수로 받으며, 두 번째 인수는 첫 번째 인수에 더할 `TIME` 표현식을 인수로 받습니다.

**단일 인수**

```sql
SELECT TIMESTAMP('2023-08-18') AS RESULT;
-- 출력: '2023-08-18 00:00:00'

SELECT TIMESTAMP('2023-08-18 14:30:00') AS RESULT;
-- 출력: '2023-08-18 14:30:00'
```

**두 개 인수**

```sql
SELECT TIMESTAMP('2023-08-18', '00:30:00') AS RESULT;
-- 출력: '2023-08-18 00:30:00';

SELECT TIMESTAMP('2023-08-18 14:30:00', '00:30:00') AS RESULT;
-- 출력: '2023-08-18 15:00:00'
```

#### NOW

`NOW()` 함수는 현재 날짜와 시간을 `YYYY-MM-DD hh:mm:ss` 또는 `YYYYMMDDHHMMSS` 형식으로 반환합니다.

```sql
SELECT NOW();
-- 출력: '2023-08-18 15:16:00'

SELECT NOW() + 0;
-- 출력: '20230818151600';
```

### 흐름 제어 함수

흐름 제어 함수는 순차적인 흐름을 제어할 때 사용하는 함수입니다.

#### IF

`IF()` 함수는 세 개의 인수를 받습니다. 첫 번째 인수가 참(true)이면 두 번째 인수를 반환하고, 거짓(false)이면 세 번째 인수를 반환합니다.

```sql
IF(표현식1, 표현식2, 표현식3);
```

```sql
SELECT IF(1>2, 2, 3) AS RESULT;
-- 출력: 3

SELECT IF(1<2, 'yes', 'no') AS RESULT;
-- 출력: 'yes'
```

#### IFNULL

`IFNULL()` 함수는 두 개의 인수를 받습니다. 첫 번째 인수가 NULL이 아니라면 첫 번째 인수를 반환하고, NULL일 경우 두 번째 인수를 반환합니다.

```sql
IFNULL(표현식1, 표현식2);
```

```sql
SELECT IFNULL(1, 0) AS RESULT;
-- 출력: 1

SELECT IFNULL(NULL, 1) AS RESULT;
-- 출력: 1
```

#### NULLIF

`NULLIF()` 함수는 두 개의 인수를 받아 첫 번째 인수와 두 번째 인수가 같은지 비교합니다. 같다면 NULL을 반환하고 같지 않으면 첫 번째 인수를 반환합니다.

```sql
NULLIF(표현식1, 표현식2);
```

```sql
SELECT NULLIF(1, 1) AS RESULT;
-- 출력: NULL

SELECT NULLIF(1, 2) AS RESULT;
-- 출력: 1

SELECT NULLIF(1>2, false) AS RESULT;
-- 출력: NULL
```

### 수학 함수

수학 함수는 수학 계산에 주로 사용되는 다양한 수학 함수를 제공합니다. 모든 수학 함수는 오류 발생 시 NULL을 반환합니다.

#### ABS

`ABS()` 함수는 인수의 절대값을 반환합니다. 인수가 NULL이면 NULL을 반환합니다.

```sql
ABS(인수);
```

```sql
SELECT ABS(1) AS RESULT;
-- 출력: 1

SELECT ABS(-1) AS RESULT;
-- 출력: 1

SELECT ABS(NULL) AS RESULT;
-- 출력: NULL
```

#### CEILING

`CEILING()` 함수는 인수보다 작지 않은 가장 작은 정수 값을 반환합니다. 인수가 NULL이면 NULL을 반환합니다.

```sql
CEILING(인수);
```

```sql
SELECT CEILING(1.00) AS RESULT;
-- 출력: 1

SELECT CEILING(1.23) AS RESULT;
-- 출력: 2
```

#### ROUND

`ROUND()` 함수는 두 개의 인수를 받습니다. 첫 번째 인수는 숫자를 받으며, 두 번째 인수는 반올림 할 자릿수를 받습니다. 두 번쨰 인수를 생략할 수 있으며 생략 시 기본값은 0입니다.

```sql
ROUND(숫자, 반올림 자릿수);
```

```sql
SELECT ROUND(1.23) AS RESULT;
-- 출력: 1

SELECT ROUND(1.23, 1) AS RESULT;
-- 출력: 1.2

SELECT ROUND(1.23, 2) AS RESULT;
-- 출력: 1.23
```

#### FLOOR

`FLOOR()` 함수는 인수보다 크지 않은 가장 큰 정수 값을 반환합니다.

```sql
FLOOR(인수);
```

```sql
SELECT FLOOR(1.23) AS RESULT;
-- 출력: 1

SELECT FLOOR(2) AS RESULT;
-- 출력: 2
```

#### POWER, POW

`POW()` 와 `POWER()` 함수는 거듭제곱 값을 반환합니다.

```sql
POW(밑, 지수);
POWER(밑, 지수);
```

```sql
SELECT POW(2, 3) AS RESULT;
-- 출력: 8
```

#### SQRT

`SQRT()` 함수는 인수의 제곱근을 반환합니다.

```sql
SQRT(인수);
```

```sql
SELECT SQRT(16) AS RESULT;
-- 출력: 4
```
