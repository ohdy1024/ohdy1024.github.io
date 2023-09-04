---
layout: post
title: "[Java] 중첩 클래스"
subtitle: "중첩 클래스, 익명 클래스, nested 클래스"
description: "중첩 클래스란 다른 클래스 내에 정의된 클래스입니다. 자바는 정적 중첩 클래스, 비정적 중첩 클래스, 로컬 클래스, 익명 클래스 네 가지 유형의 중첩 클래스를 지원합니다. 정적 중첩 클래스는 외부 클래스의 인스턴스가 아닌 외부 클래스 자체와 연관됩니다. 정적이므로 외부 클래스의 비정적(인스턴스) 멤버에 접근할 수 없지만 정적 멤버에는 자유롭게 접근하고 사용할 수 있습니다. 비정적 중첩 클래스는 내부(Inner) 클래스라고도 불립니다. 다른 클래스 내에서 정의된 클래스이며 외부 클래스의 인스턴스와 연결됩니다. 정적 중첩 클래스와 달리 내부 클래스는 외부 클래스의 정적 멤버와 비정적(인스턴스) 멤버 모두 접근할 수 있습니다. 생성자 또는 메서드 내부에서 선언된 클래스를 로컬 클래스라고 합니다. 익명 클래스는 이름 없이 생성되고 다른 클래스 내에서 정의되는 중첩 클래스 유형입니다. 이를 통해 클래스를 동시에 선언하고 인스턴스화 할 수 있으므로 기존 클래스의 확장을 간결하게 구현할 수 있습니다."
date: 2023-07-25 12:05:00+0900
categories: java
comments: true
---

# 중첩 클래스(Nested Class)

### 중첩 클래스란?

중첩 클래스란 다른 클래스 내에 정의된 클래스입니다.

자바는 정적 중첩 클래스, 비정적 중첩 클래스, 로컬 클래스, 익명 클래스 네 가지 유형의 중첩 클래스를 지원합니다.

### 정적 중첩 클래스 (Static Nested Class)

정적 중첩 클래스는 외부 클래스의 인스턴스가 아닌 외부 클래스 자체와 연관됩니다. 정적이므로 외부 클래스의 비정적(인스턴스) 멤버에 접근할 수 없지만 정적 멤버에는 자유롭게 접근하고 사용할 수 있습니다.

```java
public class OuterClass {
    private static int staticData = 10;
    private int instanceData = 20;

    public static class StaticNestedClass {
        public void displayData() {
            System.out.println(staticData);
//            System.out.println(instanceData); 인스턴스 필드에 접근 불가
        }
    }
}

public class Main {
    public static void main(String[] args) {

        OuterClass.StaticNestedClass nested = new OuterClass.StaticNestedClass();

        nested.displayData(); // 10

    }
}
```

### 비정적 중첩 클래스 (Non-static Nested Class)

비정적 중첩 클래스는 내부(Inner) 클래스라고도 불립니다. 다른 클래스 내에서 정의된 클래스이며 외부 클래스의 인스턴스와 연결됩니다. 정적 중첩 클래스와 달리 내부 클래스는 외부 클래스의 정적 멤버와 비정적(인스턴스) 멤버 모두 접근할 수 있습니다.

```java
public class OuterClass {
    private static int staticData = 10;
    private int instanceData = 20;

    public class InnerClass {
        private int innerData = 30;

        public void displayData() {
            System.out.println(staticData);
            System.out.println(instanceData);
            System.out.println(innerData);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        OuterClass outer = new OuterClass();

        OuterClass.InnerClass nested = outer.new InnerClass();

        nested.displayData();

    }
}
```

```
// 실행 결과
10
20
30
```

### 로컬 클래스 (Local Class)

생성자 또는 메서드 내부에서 선언된 클래스를 로컬 클래스라고 합니다.

```java
public class OuterClass {
    private int outerField = 10;

    public void outerMethod() {
        final int localVar = 20;

        class LocalInnerClass {
            public void innerMethod() {
                System.out.println("Outer field: " + outerField);
                System.out.println("Local variable: " + localVar);
            }
        }

        LocalInnerClass localInner = new LocalInnerClass();
        localInner.innerMethod();
    }
}

public class Main {
    public static void main(String[] args) {
        OuterClass outer = new OuterClass();
        outer.outerMethod();
    }
}
```

```
// 실행 결과
Outer field: 10
Local variable: 20
```

### 익명 클래스 (Anonymous Class)

익명 클래스는 이름 없이 생성되고 다른 클래스 내에서 정의되는 중첩 클래스 유형입니다. 이를 통해 클래스를 동시에 선언하고 인스턴스화 할 수 있으므로 기존 클래스의 확장을 간결하게 구현할 수 있습니다. 익명 클래스는 명시적으로 생성자를 가질 수 없고 정적 멤버를 정의할 수 없으며 하나의 클래스만 확장하거나 하나의 인터페이스를 구현할 수 있습니다.

```java
public interface Message {
    void display();
}

public class Main {
    public static void main(String[] args) {
        Message message = new Message() {
            @Override
            public void display() {
                System.out.println("안녕하세요");
            }
        };

        message.display(); // 안녕하세요
    }
}
```
