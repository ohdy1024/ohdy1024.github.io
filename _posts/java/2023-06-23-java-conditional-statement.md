---
layout: post
title: "[Java] 조건문"
subtitle: "조건문 if문 if-else문 switch문"
description: "조건문이란 코드를 조건에 따라 코드의 실행 흐름을 제어하는 기능을 가진 제어문입니다. 조건문에는 if 문, if-else 문, switch 문이 있습니다."
date: 2023-06-23 12:00:00 +0900
categories: java
comments: true
---

# 조건문

### 조건문이란?

조건문이란 코드를 조건에 따라 코드의 실행 흐름을 제어하는 기능을 가진 제어문입니다.

### if 문

if 문은 조건의 결과에 따라 블록 실행 여부가 결정됩니다.

조건식에는 true 또는 false 값을 반환하는 연산식이나 boolean 타입의 변수가 올 수 있습니다. 조건식이 true이면 블록을 실행하고 false이면 블록을 실행하지 않습니다. 블록 안에 실행문이 하나라면 중괄호를 생략할 수 있습니다.

```java
if (조건식) {
  실행문;
  ...
}

if (조건식)
  실행문;
```

```java
int num = 10;

if (num > 5) {
  System.out.println("5보다 크다.");
}
// 또는
if (num > 5)
  System.out.println("5보다 크다.");
```

### if-else 문

if 문으로만 복잡한 내용을 처리하는 데 한계가 있습니다. if-else 문은 조건식이 true이면 if 문 블록이 실행되고, false이면 else 블록이 실행됩니다.

```java
if (조건식) {
  // 조건식이 true일 때 실행
  실행문;
  ...
} else {
  //조건식이 false일 때 실행
  실행문;
  ...
}
```

```java
int num = 5;

if (num > 5) {
  System.out.println("5보다 크다."); // 실행 x
} else {
  System.out.println("5보다 작거나 같다."); // 실행 o
}
```

### else if 문

else if문은 2개 이상의 조건식을 사용하여 흐름을 제어할 수 있습니다.

```java
if (조건식1) {
  // 조건식1이 true이면 실행
  실행문;
} else if (조건식2) {
  // 조건식2가 true이면 실행
} else {
  // 조건식이 모두 false이면 실행
}
```

```java
int num = 5;

if (num > 5) {
  System.out.println("5보다 크다.");
} else if (num == 5) {
  System.out.println("5와 같다."); // 실행 o
} else {
  System.out.println("5보다 작다.");
}
```

### switch 문

switch 문도 if 문과 마찬가지로 흐름을 제어할 때 사용됩니다.

switch 문은 괄호 안의 변수값에 따라 해당 case로 가서 실행문을 실행시킵니다. 만약 변수값과 동일한 값을 갖는 case가 없으면 default로 가서 실행문을 실행시킵니다. default는 생략이 가능합니다.

`break` 키워드는 switch문 밖으로 빠져나가는 기능을 하는 키워드입니다.

```java
switch(변수) {
  case 값1:
    실행문1;
    break;
  case 값2:
    실행문2;
    break;
  default:
    실행문3;
}
```

```java
int num = (int)(Math.random()*6) + 1;

switch(num) {
  case 1:
    System.out.println("1 입니다.");
    break;
  case 2:
    System.out.println("2 입니다.");
    break;
  case 3:
    System.out.println("3 입니다.");
    break;
  case 4:
    System.out.println("4 입니다.");
    break;
  case 5:
    System.out.println("5 입니다.");
    break;
  default:
    System.out.println("6 입니다.");
}
```

만약 `break` 키워드를 사용하지 않는다면 변수값에 맞는 case가 실행된 후 `break` 키워드를 만나기 전까지 다음 case들도 실행이 됩니다.

```java
int num = 1;

switch(num) {
  case 1:
    System.out.println("1 입니다."); // 실행 o
  case 2:
    System.out.println("2 입니다."); // 실행 o
  case 3:
    System.out.println("3 입니다."); // 실행 o
  case 4:
    System.out.println("4 입니다."); // 실행 o
    break;
  case 5:
    System.out.println("5 입니다."); // 실행 x
    break;
  default:
    System.out.println("6 입니다."); // 실행 x
}
```

자바 14 이후부터 Switch Expressions을 사용하면 값을 변수에 바로 대입할 수도 있습니다. 단일 값이라면 화살표 오른쪽에 값을 기술하면 되고, 중괄호를 사용할 경우에는 `yield` 키워드로 값을 지정하면 됩니다. 이 경우에는 default가 존재해야 합니다.

1~4 사이의 값을 Switch Expressions 을 이용해서 모두 5로 변환시켜 보겠습니다.

```java
int num1 = (int)(Math.random()*4) + 1;

int num2 = switch(num1) {
  case 1 -> {
    System.out.println("num1은 1입니다.");
    yield num1 + 4;
  }
  case 2 -> {
    System.out.println("num1은 2입니다.");
    yield num1 + 3;
  }
  case 3 -> {
    System.out.println("num1은 3입니다.");
    yield num1 + 2;
  }
  default -> {
    System.out.println("num1은 4입니다.");
    yield num1 + 1;
  }
};

System.out.println(num2);

```
