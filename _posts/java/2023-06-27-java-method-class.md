---
layout: post
title: "[Java] 클래스와 메소드"
subtitle: "Class, Method"
description: "메서드는 클래스 내에서 정의되며 어떠한 특정 작업을 수행하는 코드 블록입니다. 메서드는 몇 번이든 호출할 수 있기 때문에 재사용성이 높습니다. 메서드를 사용하기 위해서는 먼저 메소드를 선언 해야 합니다. 메소드 선언은 선언부와 구현부로 나뉩니다. main 메소드는 자바 프로그램 실행을 위한 진입점 역할을 하는 특수한 메소드입니다. 자바 프로그램이 실행되면 JVM(Java Virtual Machine)은 main 메서드를 호출하여 프로그램을 실행합니다. 자바에서 클래스는 객체를 생성하기 위한 설계도입니다."
date: 2023-06-27 21:30:00+0900
categories: java
comments: true
---

# 클래스와 메서드

## 메서드

### 메서드란?

메서드는 클래스 내에서 정의되며 어떠한 특정 작업을 수행하는 코드 블록입니다.

메서드는 몇 번이든 호출할 수 있기 때문에 재사용성이 높습니다.

메서드를 사용하기 위해서는 먼저 메소드를 선언 해야 합니다. 메소드 선언은 선언부와 구현부로 나뉩니다.

```java
접근제한자 반환타입 메서드이름(매개변수1, 매개변수2, ...) {  // 선언부

  실행문; // 구현부
  ...
}
```

접근 제한자는 메서드의 접근성을 결정합니다.

반환타입은 메서드의 실행이 끝나고 반환할 값의 타입을 나타냅니다. 반환값이 없으면 void로 작성하면 됩니다.

메서드의 이름은 카멜 케이스로 작성됩니다.

매개변수는 함수 내부에서 사용할 변수를 외부에서 전달받기 위해 사용합니다.

예시로 값을 두 개 전달받아 더한 결과를 반환하는 메소드를 선언해보겠습니다.

```java
// 메소드 선언
public int sum(int a, int b) {
  return a + b;
}
```

`return` 키워드는 메소드의 종료 및 값을 반환한다는 의미를 가집니다.

### 메소드 호출

메소드 호출이란 메소드 블록을 실행하는 것입니다.

위의 메소드를 호출해 보겠습니다.

```java
// 메소드 선언
public int sum(int a, int b) {
  return a + b;
}

int result = sum(1, 2); // 메소드 호출문
System.out.print(result); // 3
```

### main 메소드

main 메소드는 자바 프로그램 실행을 위한 진입점 역할을 하는 특수한 메소드입니다. 자바 프로그램이 실행되면 JVM(Java Virtual Machine)은 main 메서드를 호출하여 프로그램을 실행합니다.

```java
public static void main(String[] args) {}
```

`public`은 main 메서드를 프로그램 내 어디에서나 접근할 수 있도록 하는 접근 제한자입니다.

`static`은 클래스를 인스턴스화하지 않고 메소드를 호출할 수 있도록 해주는 키워드입니다. JVM이 인스턴스를 생성하지 않고 main 메서드를 호출하기 위해 사용합니다.

`void`는 main 메소드의 반환 타입으로, main 메소드가 어떤 값도 반환하지 않음을 나타냅니다.

`main`은 메서드의 이름입니다. JVM은 프로그램 실행을 시작하기 위해 main 이름을 가진 메서드를 찾습니다.

`String[] args`는 main 메서드에 전달되는 매개변수입니다.

## 클래스

### 클래스

자바에서 클래스는 객체를 생성하기 위한 설계도입니다.

클래스는 객체의 속성(필드)과 동작(메소드)으로 구성됩니다. 클래스명은 첫 문자를 대문자로 하는 파스칼 케이스로 정의합니다. 숫자를 포함해도 되지만 첫 문자는 숫자가 될 수 없고, 특수 문자 중 $, \_를 포함할 수 있습니다.

사람의 나이 정보(필드)와 나이를 알려주는 기능(메소드)이 있는 클래스를 만든다면 아래와 같이 나타낼 수 있습니다.

```java
public class Person {

  private int age; // 필드

  public Person(int age) { // 생성자
    this.age = age;
  }

  public void displayInfo() { // 메소드
    System.out.print("나이는 : " + age + "입니다.");
  }
}
```

### 객체 생성

클래스를 선언했다고 바로 쓸 수 있는 것은 아닙니다. 클래스로부터 객체(인스턴스)를 생성해서 사용 해야 합니다.

객체를 생성하는 방법은 `new` 키워드를 사용해 생성합니다. `new` 키워드를 이용해 객체를 생성하는 것을 "인스턴스화"라고 하며, 생성된 객체를 "인스턴스"라고 부릅니다.

`new` 키워드는 객체를 생성 후 객체의 주소를 리턴하기 때문에 변수에 저장할 수 있습니다. 이 변수를 "참조 변수"라고 합니다.

```java
클래스 변수 = new 클래스();
```

```java
// Person.java
public class Person {

  private int age; // 필드

  public Person(int age) { // 생성자
    this.age = age;
  }

  public void displayInfo() { // 메소드
    System.out.print("나이는 : " + age + "입니다.");
  }
}
```

```java
// Main.java
public class Main {

  public static void main(String[] args) {
      Person person = new Person(15); // 객체 생성

      person.displayInfo(); // "나이는 15세입니다." 출력
  }
}
```

### 클래스의 구성

클래스의 구성 멤버로 생성자, 필드, 메소드가 있습니다.

**필드**는 객체의 데이터를 저장하는 역할을 합니다. 필드는 "인스턴스 변수" 또는 "멤버 변수"라고도 불립니다.

**메소드**는 객체가 수행하는 동작입니다.

**생성자**는 `new` 연산자로 객체를 생성할 때 객체의 초기화 역할을 담당합니다. 메소드와 비슷하게 생겼지만, 리턴 타입이 없고 클래스 이름과 같다는 차이점이 있습니다.

## 생성자

### 생성자 선언

모든 클래스는 생성자가 존재하고, 하나 이상을 가질 수 있습니다. 생성자가 없으면 컴파일 시 기본 생성자를 만들어줍니다. 하지만 생성자가 있다면 기본 생성자를 추가하지 않습니다.

생성자는 메소드와 비슷하지만 리턴 타입이 없고 클래스 이름과 동일합니다. 인스턴스 생성 시 값을 전달하면 생성자가 호출될 때 생성자의 매개변수로 값이 전달이 됩니다.

```java
// Person.java
public class Person {

  private int age; // 필드

  public Person(int age) { // 생성자
    this.age = age;
  }

  public void displayInfo() {
    System.out.print("나이는 " + age + "세입니다.");
  }
}

// Main.java
public class Main {

  public static void main(String[] args) {

    // 20이라는 값을 생성자로 전달합니다. 전달받은 20을 age라는 필드에 대입합니다.
    Person person = new Person(20);

    person.displayInfo() // "나이는 20세입니다." 출력
  }
}
```

`this` 키워드는 매개변수명과 필드명이 동일할 때 필드를 구분하기 위해서 사용합니다.

### 생성자 오버로딩

생성자 오버로딩이란 매개변수가 다른 여러 생성자를 선언하는 것입니다. 생성자를 오버로딩하는 이유는 객체의 필드를 다양하게 초기화하기 위해서입니다.

```java
// Person.java
public class Person {

  private int age;
  private String name;

  public Person(String name) { // 생성자1
    this.name = name;
  }

  public Person(String name, int age) { // 생성자2
    this.name = name;
    this.age = age;
  }

  public void displayInfo() {
    System.out.println(name + "님의 나이는 " + age + "세입니다.");
  }
}

// Main.java
public class Main {

  public static void main(String[] args) {

    Person person1 = new Person("철수");
    Person person2 = new Person("짱구", 5);

    person1.displayInfo(); // "철수님의 나이는 0세입니다." 출력
    person2.displayInfo(); // "짱구님의 나이는 5세입니다." 출력
  }
}

```
