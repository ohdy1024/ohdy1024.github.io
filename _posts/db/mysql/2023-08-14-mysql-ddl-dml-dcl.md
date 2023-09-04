---
layout: post
title: "[MySQL] DDL, DML, DCL"
subtitle: "DDL, DML, DCL"
date: 2023-08-14 13:45:00+0900
description: "DDL은 데이터베이스 구조를 정의하고 관리하는 데 사용되는 SQL 명령의 하위 집합을 나타냅니다. DDL 문은 테이블, 인덱스, 뷰 및 스키마와 같은 데이터베이스 개체를 생성, 변경 및 삭제하는 역할을 합니다. DML은 데이터베이스 내의 데이터를 조회, 삽입, 수정 및 삭제하는 작업을 수행하는데 사용됩니다. DCL은 데이터베이스 관리 시스템(DBMS)에서 데이터의 접근과 보안에 관련된 권한을 관리하고 제어하는 언어입니다. DCL은 데이터베이스 시스템 내에서 데이터의 무단 접근을 방지하거나 권한 있는 사용자에게 적절한 데이터 접근 권한을 부여하는 역할을 합니다"
categories: db
tags: mysql
comments: true
---

# DDL, DML, DCL

## DDL(Data Definition Language, 데이터 정의어)

### DDL이란?

DDL은 데이터베이스 구조를 정의하고 관리하는 데 사용되는 SQL 명령의 하위 집합을 나타냅니다. DDL 문은 테이블, 인덱스, 뷰 및 스키마와 같은 데이터베이스 개체를 생성, 변경 및 삭제하는 역할을 합니다.

MySQL의 DDL 문은 `CREATE`, `ALTER`, `DROP`, `RENAME`, `TRUNCATE` 등이 있습니다.

### CREATE

`CREATE` 문은 새 데이터베이스 개체를 만드는데 사용됩니다.

**데이터베이스(스키마) 생성**

```sql
CREATE DATABASE 데이터베이스명;
```

**테이블 생성**

테이블 생성 시 최소 하나의 컬럼이 필요합니다.

```sql
CREATE TABLE 테이블명 (
  컬럼명1 자료형,
  컬럼명2 자료형,
  ...
);
```

**인덱스 생성**

```sql
CREATE INDEX 인덱스명 ON 테이블명(컬럼명1,...);
```

### ALTER

`ALTER` 문은 기존 데이터베이스 개체를 수정하는데 사용됩니다.

**데이터베이스 속성(문자 집합, 콜레이션, ...) 변경**

```sql
ALTER DATABASE 데이터베이스이름 CHARACTER SET=문자집합이름;
ALTER DATABASE 데이터베이스이름 COLLATE=콜레이션이름;
```

**테이블 새 컬럼 추가**

```sql
ALTER TABLE 테이블명 ADD COLUMN 컬럼명 자료형;
```

**테이블 컬럼 자료형 수정**

```sql
ALTER TABLE 테이블명 MODIFY COLUMN 컬럼명 수정자료형;
```

**테이블 컬럼 삭제**

```sql
ALTER TABLE 테이블명 DROP COLUMN 컬럼명;
```

### RENAME

`RENAME` 문은 데이터베이스 개체의 이름을 변경하는데 사용됩니다.

**테이블 이름 변경**

```sql
RENAME TABLE 기존테이블명 TO 새테이블명;
```

MySQL에서 데이터베이스 이름을 변경하는 문을 제공하지 않기 때문에 데이터베이스 이름을 변경하려면 데이터를 백업한 다음 새 데이터베이스를 만들어 데이터를 복원하는 방법을 써야합니다.

### DROP

`DROP` 문은 데이터베이스 개체를 삭제하는데 사용됩니다. `DROP` 문은 데이터를 영구적으로 삭제하므로 신중하게 사용해야 합니다.

**데이터베이스 삭제**

```sql
DROP DATABASE 데이터베이스명;
```

**테이블 삭제**

```sql
DROP TABLE 테이블명;
```

### TRUNCATE

`TRUNCATE` 문은 특정 테이블의 모든 데이터를 삭제하는 SQL 문입니다. 테이블의 모든 행을 제거하고 테이블 구조는 그대로 유지하는 역할을 하며 롤백되지 않는다는 특징이 있습니다.

```sql
TRUNCATE TABLE 테이블명;
```

## DML(Data Manipulation Language, 데이터 조작어)

### DML이란?

DML은 데이터베이스 내의 데이터를 조회, 삽입, 수정 및 삭제하는 작업을 수행하는데 사용됩니다.

### SELECT

`SELECT` 문은 데이터베이스의 하나 또는 여러 테이블에서 데이터를 검색하는데 사용됩니다.

```sql
SELECT 컬럼1, 컬럼2, ... FROM 테이블명;
```

### INSERT

`INSERT` 문은 데이터베이스 테이블에 새로운 데이터를 추가하는 역할을 합니다.

**특정 컬럼에 값 직접 삽입**

```sql
INSERT INTO 테이블명 (컬럼1, 컬럼2, ...) VALUES (값1, 값2, ...);
```

**다른 테이블의 데이터를 가져와 삽입**

```sql
INSERT INTO 테이블명 (컬럼1, 컬럼2, ...) SELECT 컬럼a, 컬럼b, ...  FROM 다른테이블명;
```

### UPDATE

`UPDATE` 문은 테이블의 기존 레코드를 수정하는데 사용됩니다. `UPDATE` 문을 사용할 때 주의할 점은 모든 레코드가 수정될 수 있으니 조심해서 사용해야 합니다.

**테이블 레코드 수정**

```sql
UPDATE 테이블명 SET 컬럼1 = 값1, 컬럼2 = 값2, ...;
```

**테이블 특정 레코드 수정**

```sql
UPDATE 테이블명 SET 컬럼1 = 값1, ... WHERE 조건문;
```

### DELETE

`DELETE` 문은 테이블의 레코드를 제거할 때 사용합니다. `DELETE` 문도 `WHERE` 절과 함께 사용하지 않으면 모든 레코드가 삭제될 수 있으니 주의해야 합니다.

**모든 레코드 삭제**

```sql
DELETE FROM 테이블명;
```

**특정 레코드 삭제**

```sql
DELETE FROM 테이블명 WHERE 조건문;
```

## DCL(Data Control Language, 데이터 제어어)

### DCL이란?

DCL은 데이터베이스 관리 시스템(DBMS)에서 데이터의 접근과 보안에 관련된 권한을 관리하고 제어하는 언어입니다. DCL은 데이터베이스 시스템 내에서 데이터의 무단 접근을 방지하거나 권한 있는 사용자에게 적절한 데이터 접근 권한을 부여하는 역할을 합니다.

### GRANT

`GRANT` 문은 사용자에게 특정 데이터베이스 개체(테이블, 뷰 등)에 대한 권한을 부여합니다.

```sql
GRANT 권한 ON 개체 TO 사용자;
```

### REVOKE

`REVOKE` 문은 사용자로부터 특정 데이터베이스 개체에 대한 권한을 제거합니다.

```sql
REVOKE 권한 ON 개체 FROM 사용자;
```
