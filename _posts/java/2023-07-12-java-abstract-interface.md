---
layout: post
title: "[Java] 추상 클래스와 인터페이스"
subtitle: "추상 클래스, 인터페이스, abstract, interface"
date: 2023-07-12 12:58:00 +0900
categories: java
comments: true
---

# 추상 클래스와 인터페이스

## 추상 클래스

### 추상 클래스

추상 클래스는 `abstract` 키워드로 선언된 클래스입니다. 추상 클래스의 주요 목적은 여러 하위 클래스에서 공유할 수 있는 공통 특성 및 동작을 정의하는 것입니다.

추상 클래스는 직접 객체를 생성할 수 없습니다. 대신 다른 클래스에 의해 상속되도록 설계되어 추상 메서드에 대한 구현을 제공할 수 있습니다.

```java
public abstract class Animal {
}

public class Main {
  public static void main(String[] args) {
    Animal animal = new Animal(); // 생성 불가
  }
}

```

추상 클래스도 필드, 메서드를 선언할 수 있습니다. 그리고 추상 클래스도 객체이기 때문에 생성자가 필요합니다.

```java
public abstract class Animal {
  private int age;

  public Animal(int age) {
    this.age = age;
  }

  public void getAge() {
    System.out.println("age: " + age);
  }
}

public class Dog extends Animal {

  public Dog(int age) {
    super(age);
  }
}

public class Main {
  public static void main(String[] args) {
    Dog dog = new Dog(3);

    dog.getAge(); // 3
  }
}
```

### 추상 메서드

추상 클래스는 하나 이상의 추상 메서드를 포함할 수 있습니다. 추상 메서드는 자식 클래스들마다 선언부는 같지만 구현부는 다른 메서드가 있을 때 사용합니다. 추상 메서드는 `abstract` 키워드를 붙여 메서드를 선언합니다. 일반 메서드와 다르게 구현부가 없습니다.

```java
abstract 반환타입 메서드명(매개변수1, ...);
```

추상 클래스를 상속받은 자식 클래스는 부모 클래스가 추상 메서드가 있다면, 반드시 추상 메서드의 구현부를 작성해야 합니다.

```java
public abstract class Animal {
  abstract void sound();
}

public class Dog extends Animal {

  @Override
  void sound() {
    System.out.println("멍멍");
  }
}

public class Cat extends Animal {

  @Override
  void sound() {
    System.out.println("야옹");
  }
}

public class Main {
  public static void main(String[] args) {
    Dog dog = new Dog();
    Cat cat = new Cat();
    dog.sound(); // 멍멍
    cat.sound(); // 냐옹
  }
}
```

## 인터페이스

### 인터페이스

인터페이스는 구현 클래스가 준수해야 하는 가이드라인입니다. 인터페이스는 추상 메서드와 상수만 포함하기 때문에, 무엇을 해야 하는지 정의하지만 어떻게 해야 하는지는 정의하지 않습니다.

### 인터페이스 선언

인터페이스는 선언 시 `interface` 키워드를 사용합니다.

```java
interface 인터페이스명 {
  ...
}
```

### 인터페이스 구현

인터페이스를 구현하려면 `implemnets` 키워드 뒤에 구현하려는 인터페이스 이름을 사용해야 합니다. 여러 인터페이스를 구현하려는 경우 쉼표를 사용하여 구분할 수 있습니다.

```java
public class 클래스 implements 인터페이스1, 인터페이스2, ... {
  ...
}
```

인터페이스를 구현하는 클래스를 선언한 후에는 인터페이스에 선언된 모든 메서드에 대한 구현을 제공해야 합니다.

```java
public interface AInterface {
  void method1();
}

public class A implements AInterface {

  @Override
  public void method1() {
    System.out.println("method1");
  }
}
```

인터페이스를 구현한 클래스는 객체 생성 시 그 인터페이스를 참조 타입으로 쓸 수 있습니다.

```java
public interface AInterface {
  void method1();
}

public class A implements AInterface {

  @Override
  public void method1() {
    System.out.println("method1");
  }
}

public class Main {
  public static void main(String[] args) {
    AInterface a = new A();
    a.method1(); // method1
  }
}
```

### 인터페이스 필드

인터페이스의 필드는 상수로 취급되며, `public static final`로 선언됩니다. 생략하더라도 자동적으로 컴파일 과정에서 붙게 됩니다.

```java
[public static final] 타입 상수명 = 값;
```

```java
public interface AInterface {
  int VALUE = 10;
}

public class A implements AInterface {
}


public class Main {
  public static void main(String[] args) {
    // static이 붙어 객체 생성 안하고 접근 가능
    System.out.println(A.VALUE); // 10

    A.VALUE = 15; // final로 선언되어 재할당 불가
  }
}
```

### 추상 메서드

인터페이스는 구현 클래스가 재정의해야 하는 추상 메서드를 가질 수 있습니다. 인터페이스의 추상 메서드는 앞에 `public` 과 `abstract`가 선언되어야 합니다. 생략하더라도 컴파일 과정에서 자동으로 붙게 됩니다.

추상 메서드가 있는 인터페이스를 구현한 클래스가 있다면 추상 메서드를 반드시 재정의해야 합니다.

```java
public interface AInterface {
  void method1();
}

public class A implements AInterface {
    @Override
    public void method1() { // 재정의 안하면 오류 발생
        System.out.println("method1");
    }
}

public class Main {
    public static void main(String[] args) {
        AInterface a = new A();
        a.method1(); // method1
    }
}
```

메서드를 재정의할 때 주의할 점은 인터페이스의 추상 메서드는 `public` 접근 제어자를 갖기 때문에 `public`보다 더 낮은 접근 제한은 할 수 없습니다.

```java
public interface AInterface {
  void method1();
}

public class A implements AInterface {
    @Override
    protected void method1() { // 오류 발생
        System.out.println("method1");
    }
}

public class Main {
    public static void main(String[] args) {
        AInterface a = new A();
        a.method1(); // method1
    }
}
```

### 디폴트 메서드

자바 8부터 인터페이스가 메서드에 대한 기본 구현을 제공할 수 있도록하는 디폴트 메서드가 추가되었습니다. `default` 키워드를 사용하여 선언하면 됩니다.

```java
public interface AInterface {

    default void method1() {
        System.out.println("method1");
    }
}

public class A implements AInterface {
}

public class Main {
    public static void main(String[] args) {
        AInterface a = new A();
        a.method1(); // method1
    }
}
```

디폴트 메서드도 재정의가 가능합니다. 주의할 점은 디폴트 메서드도 `public` 접근 제어자를 갖기 때문에 더 제한된 접근 제어자를 사용할 수 없으며, `default` 키워드를 생략해야 합니다.

```java
public interface AInterface {

    default void method1() {
        System.out.println("method1");
    }
}

public class A implements AInterface {
    @Override
    public void method1() {
        System.out.println("method1 재정의!");
    }
}

public class Main {
    public static void main(String[] args) {
        AInterface a = new A();
        a.method1(); // method1 재정의!
    }
}
```

### 정적 메서드

정적 메서드도 자바 8에서 도입되었습니다. 정적 메서드는 구현 객체가 없어도 인터페이스만으로 호출할 수 있는 메서드입니다.

인터페이스의 정적 메서드는 `static` 키워드를 사용하여 선언합니다. 정적 메서드는 인터페이스 자체 내에서 구현하면 됩니다. 접근 제어자는 `public`을 가지며 생략 가능합니다.

```java
public interface AInterface {

    static void method1() {
        System.out.println("method1");
    }
}

public class Main {
    public static void main(String[] args) {
        AInterface.method1(); // method1
    }
}
```

### private 메서드

자바 9부터 `private` 접근 제어자를 가지는 메서드를 선언할 수 있습니다.

```java
public interface AInterface {

    private static void staticMethod() {
        System.out.println("private static method");
    }

    private void defaultMethod() {
        System.out.println("private method");
    }

    default void call() {
        staticMethod();
        defaultMethod();
    }
}

public class A implements AInterface {
}

public class Main {
    public static void main(String[] args) {
        AInterface a = new A();
        a.call();
    }
}
```

### 인터페이스 상속

인터페이스도 다른 인터페이스를 상속할 수 있으며, 클래스와 다르게 다중 상속이 가능합니다.

```java
public interface 인터페이스1 extends 인터페이스2, 인터페이스3 {
  ...
}
```
