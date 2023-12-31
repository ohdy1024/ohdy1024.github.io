---
layout: post
title: "[Java] 변수"
subtitle: "변수"
descirption: "변수는 데이터의 저장과 참조를 위해 할당된 메모리 공간에 붙인 이름을 의미합니다. 자바의 변수는 다양한 타입의 값을 저장할 수 없습니다. 정수형 변수에는 정수값만 저장할 수 있고, 실수형
변수에는 실수값만 저장할 수 있습니다. 변수를 사용하려면 변수 선언이 필요합니다. 변수 선언은 어떤 타입의 데이터를 저장할 것인지 그리고 변수 이름이 무엇인지를 결정하는 것입니다. 자료형은 변수가 보유할 수 있는 값의 종류와 크기를 결정하는 기본 구성 요소입니다."
date: 2023-06-22 19:30:00+0900
categories: java
comments: true
---

# 변수(Variable)

## 변수

### 변수란?

변수는 데이터의 저장과 참조를 위해 할당된 메모리 공간에 붙인 이름을 의미합니다.

자바의 변수는 다양한 타입의 값을 저장할 수 없습니다. 정수형 변수에는 정수값만 저장할 수 있고, 실수형
변수에는 실수값만 저장할 수 있습니다.

변수를 사용하려면 변수 선언이 필요합니다. 변수 선언은 어떤 타입의 데이터를 저장할 것인지 그리고 변수 이름이 무엇인지를 결정하는 것입니다.

### 변수 이름 짓기

변수 이름은 문자(대문자, 소문자), 숫자, 달러 기호($) 및 밑줄 문자(\_)로 구성될 수 있습니다.

변수의 첫 문자는 문자, 밑줄 또는 달러 기호여야 합니다. 숫자로 시작하면 안 됩니다.

일반적으로 변수 이름은 문자로 시작하고 첫 문자를 소문자로 시작하는 카멜 케이스로 작성합니다.

카멜 케이스란 여러 단어로 변수 명을 지을 때 단어들을 공백없이 붙이고, 첫 단어의 첫 문자는 소문자로 시작하고 다음 단어들의 첫 단어는 대문자로 시작하는 표기법입니다.

```java
String var = "camelCase";
```

## 자료형

### 자료형이란?

자료형은 변수가 보유할 수 있는 값의 종류와 크기를 결정하는 기본 구성 요소입니다.

### 정수 타입

자바는 byte(1byte), char(2byte), short(2byte), int(4byte), long(8byte) 5가지 정수타입이 있습니다.

byte, short, int, long은 모두 부호가 있는 정수 타입입니다. 최상위 bit는 부호 bit로 사용되고, 나머지 bit는 값의 범위를 결정합니다.

long 타입은 보통 수치가 큰 데이터를 다루는 프로그램에서 사용됩니다. 자바에서 long 타입을 사용할 때 뒤에 소문자 'l'이나 'L'을 붙여 컴파일러에게 알려줘야 합니다.

```java
byte var1 = 15;
short var2 = 1000;
char var3 = 65;
int var4 = 10000000;
long var5 = 100000000000L;
```

### 문자 타입

하나의 문자를 작은따옴표(')로 감싼 것을 문자 리터럴이라고 합니다. 문자 리터럴은 유니코드로 변환되어 저장되는데 자바는 이러한 유니코드를 저장할 수 있도록 char 타입을 제공합니다.

유니코드가 정수이므로 char 타입도 정수 타입에 속합니다. 그렇기 때문에 char 변수에 작은따옴표로 감싼 문자가 아니라 유니코드 숫자를 직접 대입할 수도 있습니다.

```java
char var1 = 'A';
char var2 = 65;
```

### 실수 타입

실수 타입에는 float과 double이 있습니다. float은 4byte의 크기를 가지고, double은 8byte의 크기를 가집니다. double은 float 타입보다 큰 실수를 저장할 수도 있고 정밀도 또한 높습니다.

컴파일러는 실수 리터럴을 기본적으로 double 타입으로 해석하기 때문에 double 타입 변수에 대입해야 합니다. float 타입에 대입하고 싶다면 리터럴 뒤에 소문자 'f나 대문자 'F'를 붙여 컴파일러가 float 타입임을 알 수 있도록 해야 합니다.

```java
double var1 = 3.14;
float var2 = 3.14f;
```

### 논리 타입

논리 타입은 참과 거짓을 표현하기 위한 타입입니다.

boolean 타입의 변수에 논리 리터럴 true 또는 false를 대입할 수 있습니다.

boolean 타입 변수는 보통 조건문과 제어문의 실행 흐름을 변경하는 데 사용됩니다. 연산식 중에서 비교 및 논리 연산의 산출값은 true 또는 false 이므로 이를 이용해 실행 흐름을 변경합니다.

```java
boolean var1 = true;
boolean var2 = false;

int num = 10;
boolean result = num > 5;

```

### 문자열 타입

큰따옴표(")로 감싼 문자들을 문자열이라고 합니다. 이런 문자열을 변수에 저장하고 싶다면 String 타입을 사용하여 문자열을 저장합니다.

```java
String var1 = "문자열입니다";
```

자바 13부터는 텍스트 블록 문법을 제공합니다.

```java
String str = """
  문자열
  입니다.
  """;
```

위와 같이 큰따옴표 3개로 감싸면 이스케이프 문자를 사용해서 줄바꿈을 할 필요없이 작성된 그대로 문자열이 저장됩니다.

## 타입 변환

### 타입 변환이란?

타입 변환이란 기존에 가지고 있던 자료형에서 다른 자료형으로 변환하는 프로세스를 나타냅니다.

### 자동 타입 변환

자동 타입 변환이란 말 그대로 자동으로 타입 변환이 일어나는 것을 말합니다. 자동 타입 변환은 값의 허용 범위가 작은 타입이 허용 범위가 큰 타입으로 대입될 때 발생합니다.

자료형의 크기에 상관없이 정수 타입보다 실수 타입이 우선됩니다. 이유는 정수 타입에 비해 실수 타입이 값의 표현 범위가 넓기 때문입니다.

**기본 타입 허용 범위 순**

```
byte < short, char < int < long < float < double
```

**자동 타입 변환**

```java
short var1 = 5;
int var2 = var1;
```

자동 타입 변환에서 예외가 있습니다. char 타입보다 허용 범위가 작은 byte 타입은 char 타입으로 자동 변환될 수 없습니다.

**연산식에서 자동 타입 변환**

자바에서는 byte, short 타입의 변수는 int 타입으로 자동 타입 변환되어 연산을 수행합니다. 변수에 저장할 값이 작더라도 연산이 동반되면 변수의 타입을 byte, short보다 int 타입으로 선언하는 것이 성능에 좋습니다.

```java
byte num1 = 10;
byte num2 = 10;
byte num3 = num1 + num2; //컴파일 에러
```

### 강제 타입 변환

허용 범위가 큰 타입을 허용 범위가 작은 타입으로 쪼개어서 저장하는 것을 강제 타입 변환이라고 합니다. 강제 타입 변환을 하면 범위가 큰 타입의 상위 바이트가 잘려 나가기 때문에 유효한 데이터가 존재하는 경우 알 수 없는 값으로 변환이 되므로 주의가 필요합니다.

```java
int num1 = 1000;
byte num2 = (byte) num1;

System.out.println(num2) // -24
```

### 상수

상수란 값이 변하지 않는 값을 의미합니다. 자바에서 상수를 선언할 때 `final`을 사용하여 선언합니다. `final`을 사용하면 값을 한 번만 할당할 수 있습니다.

```java
public class Main {
  public static void main(String[] args) {
    final String name = "철수";
    System.out.print(name);
  }
}
```

자바에서 상수는 보통 `static`과 함꼐 사용하여 선언합니다.

```java
public class Main {
  final static String name = "철수";

  public static void main(String[] args) {
    System.out.print(name);
  }
}
```
