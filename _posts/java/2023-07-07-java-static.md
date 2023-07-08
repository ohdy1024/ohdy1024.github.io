---
layout: post
title: "[Java] 클래스 메서드와 클래스 변수"
subtitle: "클래스 메서드, 클래스 변수, static, 정적 변수"
date: 2023-07-07 16:10:00 +0900
categories: java
comments: true
---

# 클래스 변수와 클래스 메소드

### 인스턴스 변수와 클래스 변수

선언 방법에 따라 인스턴스 변수와 클래스 변수로 나뉩니다. 인스턴스 변수는 객체 생성 후 사용할 수 있고, 클래스 변수는 객체 생성 없이 사용할 수 있는 차이점이 있습니다.

### 인스턴스 변수

인스턴스 변수는 객체를 생성한 후 사용할 수 있습니다. 인스턴스 변수는 생성된 각 개체마다 값이 다를 수 있습니다.

```java
public class Main {
  public static void main(String[] args) {

    Person person1 = new Person(15);
    Person person2 = new Person(20);

    person1.display(); // 15
    person2.display(); // 20

  }
}

public class Person {
  public int age;

  public Person(int age) {
    this.age = age;
  }

  public void display() {
    System.out.print("age: " + age);
  }
}
```

### this

객체 내부에서 인스턴스 변수에 접근하기 위해 `this`를 사용합니다. 주로 생성자에서 인스턴스 변수의 값을 할당할 때 인스턴스 변수와 매개변수 명이 동일하면 인스턴스 변수임을 나타내기 위해 사용합니다.

```java
public class Person {
  public int age;

  public Person(int age) {
    this.age = age; // this.age는 인스턴스 변수를 가르킵니다.
  }
}
```

### 클래스 변수

클래스 내에 선언된 변수 앞에 `static`을 붙이면 "클래스 변수"가 됩니다. 클래스 변수는 모든 인스턴스 간에 공유되는 변수입니다. 객체를 생성할 필요 없이 클래스를 통해 바로 사용이 가능합니다.

모든 인스턴스 간에 공유되기 때문에 일반적으로 여러 인스턴스에서 공유해야 하는 상수 또는 변수는 클래스 변수로 선언하는 것이 좋습니다.

```java
public class Circle {
  static double PI = 3.14;
}

public class Main {
  public static void main(String args) {
    System.out.print(Circle.PI); // 3.14
  }
}
```

객체를 생성해서 사용할 수 있지만 일반적으로 클래스 변수는 객체를 생성하지 않고 사용합니다.

```java
public class Circle {
  static double PI = 3.14;
}

public class Main {
  public static void main(String args) {
    Circle circle = new Circle();
    System.out.print(circle.PI); // 3.14
  }
}
```

### 클래스 메서드

클래스 메서드도 앞에 `static` 키워드를 붙인 메서드입니다.

```java
public class Circle {
  static double PI = 3.14;

  static double area(double radius) {
    return (radius * radius) * PI;
  }
}

public class Main {
  public static void main(String[] args) {
    System.out.print(Circle.area(2.0)); // 12.56
  }
}
```

### 클래스 메소드에서 인스턴스 변수, 인스턴스 메서드 접근 불가

인스턴스 변수, 인스턴스 메서드는 인스턴스가 생성 되어야 사용이 가능합니다. 반면 클래스 메서드는 인스턴스 생성 이전부터 호출이 가능합니다. 그렇기 때문에 클래스 메서드에서 인스턴스 변수, 메서드를 사용할 수 없습니다.

```java
public class Person {
  private int age;

  public Person(int age) {
    this.age = age;
  }

  static void display() {
    System.out.println("age: " + age); // 에러 발생
  }
}
```

클래스 메서드에서 인스턴스 변수 및 인스턴스 메서드를 사용하고 싶다면 객체를 먼저 생성한 후 접근해야 합니다.

```java
public class Person {
  private int age;

  public Person(int age) {
    this.age = age;
  }

  static void display() {
    Person person = new Person(15);
    System.out.println("age: " + person.age);
  }
}

public class Main {
  public static void main(String[] args) {
    Person.display(); // age: 15 출력
  }
}
```

### static 블록

복잡한 초기화 작업이 필요할 떄 static 블록을 이용하면 됩니다. static 블록은 클래스가 메모리로 로딩될 떄 자동으로 실행됩니다. 여러 개가 선언되어 있을 경우에는 순서대로 실행됩니다.

```java
import java.time.LocalDate;

public class Main {
  static String date;

  static {
    date = LocalDate.now().toString();
  }

  public static void main(String[] args) {
    System.out.print(date); // 2023-07-07
  }
}
```
