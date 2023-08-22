---
layout: post
title: "[Java] 상속"
subtitle: "상속, Inheritance"
description: "상속은 부모가 자식에게 물려주는 것을 의미합니다. 자바에서도 마찬가지로 클래스가 다른 클래스에서 상속되면 부모 클래스에 정의된 모든 속성과 동작을 가져오게 됩니다. 상속하는 클래스를 상위 클래스 또는 부모 클래스라고 하고 상속받는 클래스를 하위 클래스 또는 자식 클래스라고 합니다. 자바에서는 extends 키워드를 사용하여 자식 클래스는 부모 클래스에서 멤버(필드 및 메서드)를 상속할 수 있습니다. 하위 클래스는 자체 멤버를 추가하거나 상속된 멤버를 재정의하여 동작을 수정할 수도 있습니다. 자바는 다중 상속을 허용하지 않습니다. 따라서 여러 개의 부모 클래스를 상속할 수 없습니다. 객체를 생성할 때 자동으로 생성자를 호출합니다. 자식 객체를 생성할 때 먼저 부모 객체를 생성 후 자식 객체가 생성되는데 자식 객체의 생성자뿐만 아니라 부모 객체의 생성자도 호출되어야 합니다."
date: 2023-07-08 14:20:00 +0900
categories: java
comments: true
---

# 상속

### 상속이란?

상속은 부모가 자식에게 물려주는 것을 의미합니다. 자바에서도 마찬가지로 클래스가 다른 클래스에서 상속되면 부모 클래스에 정의된 모든 속성과 동작을 가져오게 됩니다. 상속하는 클래스를 상위 클래스 또는 부모 클래스라고 하고 상속받는 클래스를 하위 클래스 또는 자식 클래스라고 합니다.

자바에서는 `extends` 키워드를 사용하여 자식 클래스는 부모 클래스에서 멤버(필드 및 메서드)를 상속할 수 있습니다. 하위 클래스는 자체 멤버를 추가하거나 상속된 멤버를 재정의하여 동작을 수정할 수도 있습니다.

자바는 다중 상속을 허용하지 않습니다. 따라서 여러 개의 부모 클래스를 상속할 수 없습니다.

```java
class 자식클래스 extends 부모클래스 {
  ...
}
```

```java
public class Vehicle {
  void drive() {
    System.out.println("부릉");
  }
}

public class Car extends Vehicle {
}

public class Main {
  public static void main(String[] args) {
    Car car = new Car();
    car.drive(); // 부릉
  }
}
```

### 상속과 생성자

객체를 생성할 때 자동으로 생성자를 호출합니다. 자식 객체를 생성할 때 먼저 부모 객체를 생성 후 자식 객체가 생성되는데 자식 객체의 생성자뿐만 아니라 부모 객체의 생성자도 호출되어야 합니다.

부모 객체의 생성자는 자식 객체의 생성자에서 `super` 키워드를 이용해 호출합니다. 자신이 직접 코드를 작성하지 않았다면 자동으로 추가가 됩니다.

```java
public class A {
  public A() {
    System.out.print("A ");
  }
}

public class B extends A {
  public B() {
    super(); // 생략 가능
    System.out.println("B");
  }
}

public class Main {
  public static void main(String[] args) {
    B b = new B(); // A B 출력
  }
}
```

부모 클래스의 기본 생성자가 없고 매개변수가 있는 생성자만 있다면 자식 클래스의 생성자에서 직접 호출을 해야 합니다.

```java
public class A {
  public int a;

  public A(int a) {
    this.a = a;
  }
}

public class B extends A {
  public B() {
    super(1); // 생략 불가능
  }
}

public class Main {
  public static void main(String[] args) {
    B b = new B();

    System.out.println(b.a); // 1
  }
}
```

`super` 키워드는 자식 클래스 생성자의 가장 윗부분에 있어야 합니다. 그렇지 않으면 컴파일 오류가 발생합니다.

```java
public class A {
  public A() {
    System.out.println("A 생성자");
  }
}

public class B extends A {
  public B() {
    System.out.println("B 생성자");
    super(); // 오류 발생
  }
}
```

### 오버라이딩(Overriding)

오버라이딩이란 부모 클래스에서 이미 정의된 메서드를 자식 클래스에서 재정의하는 것을 의미합니다.

메서드를 오버라이딩하기 위해선 부모 메서드의 선언부가 동일해야 하고, 접근 제어자는 부모 클래스보다 더 제한적인 접근 제어자를 가져서는 안됩니다.

메서드를 재정의할 떄 `@Override` 어노테이션을 사용하는 것이 일반적입니다. 이 어노테이션은 자식 클래스의 메서드 선언부와 부모 클래스의 선언부가 일치하지 않는 경우 컴파일 중에 오류를 감지하는 데 도움이 됩니다.

**오류**

```java
public class Animal {
  public void sound() {
    System.out.println("동물 소리");
  }
}

public class Dog extends Animal {

  @Override
  private void sound() { // 부모 클래스의 메서드보다 더 제한적인 접근 제한자로 인한 오류 발생
    System.out.println("멍멍");
  }
}
```

```java
public class Animal {
  public void sound() {
    System.out.println("동물 소리");
  }
}

public class Dog extends Animal {

  @Override
  public void sonud() { // 잘못된 선언부로 인한 오류 발생
    System.out.println("멍멍");
  }
}
```

**성공**

```java
public class Animal {
  public void sound() {
    System.out.println("동물 소리");
  }
}

public class Dog extends Animal {

  @Override
  public void sound() {
    System.out.println("멍멍");
  }
}

public class Main {
  public static void main(String[] args) {
    Animal animal = new Animal();
    Dog dog = new Dog();

    animal.sound(); // 동물 소리
    dog.sound(); // 멍멍
  }
}
```

### 부모 클래스의 메서드 호출

자식 클래스에서 부모 클래스의 메서드를 사용하고 싶다면 `super` 키워드와 도트(.) 연산자를 이용해 사용할 수 있습니다. 위치는 어디든지 올 수 있기 때문에 처리해야 하는 순서대로 작성하면 됩니다.

```java
public class A {
  public void method1() {
    System.out.println("A method1");
  }
}

public class B extends A {
  @Override
  public void method1() {
    super.method1();
    System.out.println("B method1");
  }
}

public class Main {
  public static void main(String[] args) {
    B b = new B();

    /*
    * A method1
    * B method1 출력
    */
    b.method1();
  }
}
```

### final 클래스

클래스를 선언할 때 class 앞에 `final` 키워드를 붙이면 상속할 수 없는 클래스가 됩니다.

```java
public final class A {

}

public class B extends A { // 상속할 수 없어 오류 발생

}
```

### final 메소드

메서드를 선언할 때 `final` 키워드를 붙이면 오버라이딩을 할 수 없는 메서드가 됩니다.

```java
public class A {
  public final void method1() {
    System.out.println("A method1");
  }
}

public class B extends A {

  @Override // 오버라이딩할 수 없기 때문에 오류 발생
  public void method1() {
    System.out.println("B method1");
  }
}
```

### 자동 타입 변환

자바에서는 자식 클래스의 객체를 생성할 때 참조 타입을 부모 클래스로 할 수 있습니다. 생성된 자식 객체는 부모 클래스에 선언된 멤버(필드와 메서드)만 접근이 가능합니다.

```java
public class Parent {
  void method1() {
    System.out.println("Parent method1");
  }
}

public class Child extends Parent {

  @Override
  void method1() {
    System.out.println("Child method1");
  }

  void method2() {
    System.out.println("Child method2");
  }
}

public class Main {
  public static void main(String[] args) {
    Parent child = new Child();

    child.method1(); // 호출 O, Child method1 출력
    child.method2(); // 호출 X, 오류 발생
  }
}
```

### 강제 타입 변환

부모 클래스 타입에서 자식 클래스 타입으로 강제 타입 변환을 할 수 있습니다. 강제 타입 변환을 하기 위해서는 자식 객체가 부모 타입으로 자동 변환된 후 다시 자식 타입으로 변환해야 합니다.

```java
public class Parent {
  void method1() {
    System.out.println("Parent method1");
  }
}

public class Child extends Parent {

  @Override
  void method1() {
    System.out.println("Child method1");
  }

  void method2() {
    System.out.println("Child method2");
  }
}

public class Main {
  public static void main(String[] args) {
    Parent child1 = new Child();

    child1.method1(); // Child method1
    // child.method2();

    Child child2 = (Child) child1;

    child2.method1(); // Child method1
    child2.method2(); // Child method2
  }
}
```

### instanceof 연산자

`instanceof` 연산자는 "참조 변수"가 참조하는 인스턴스의 ‘클래스’나 참조하는 인스턴스가 ‘상속하는 클래스’를 묻는 연산자입니다. 결괏값으로 불린 값을 반환합니다.

```java
boolean result = 객체 instanceof 타입;
```

```java
public class Parent {
}

public class Child extends Parent {
}

public class Main {
  public static void main(String[] args) {
    Parent parent = new Parent();
    Child child = new Child();

    System.out.println(parent instanceof Parent); // true
    System.out.println(parent instanceof Child); // false
    System.out.println(child instanceof Parent); // true
    System.out.println(child instanceof Child); // true
  }
}
```
