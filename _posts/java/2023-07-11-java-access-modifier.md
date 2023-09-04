---
layout: post
title: "[Java] 접근 제어자"
subtitle: "접근 제어자, Access Modifier"
description: "자바에서는 객체를 외부에서 수정 및 접근하는 것을 제한하기 위한 기능으로 접근 제어자을 사용합니다. 접근 제어자는 private, default, protected, private가 있습니다. 클래스는 public, default를 가질 수 있으며, 멤버(필드, 생성자, 메서드)는 모든 접근 제어자를 가질 수 있습니다."
date: 2023-07-11 12:58:00+0900
categories: java
comments: true
---

# 접근 제어자

### 접근 제어자(Access Modifier)

자바에서는 객체를 외부에서 수정 및 접근하는 것을 제한하기 위한 기능으로 접근 제어자을 사용합니다.

접근 제어자는 `private`, `default`, `protected`, `private`가 있습니다.

범위는 `public` > `protected` > `default` > `private` 순으로 좁아집니다.

클래스는 `public`, `default`를 가질 수 있으며, 멤버(필드, 생성자, 메서드)는 모든 접근 제어자를 가질 수 있습니다.

`private`는 클래스 내부에서만 접근이 가능합니다.

```java
public class A {
  private int num = 1;

  public int getNum() {
    return num; // 내부에 있는 메서드는 private 선언된 필드에 접근 가능
  }
}

public class Main {
  public static void main(String[] args) {
    A a = new A();

    System.out.println(a.num); // 다른 클래스에서는 접근이 불가능해 오류 발생
    System.out.println(a.getNum()); // 1
  }
}

```

접근 제어자를 생략하면 `default` 접근 제어자를 가지며, 같은 패키지 내에서만 접근 가능합니다.

```java
package com.test;

public class A {
  int num = 5;
}
```

```java
package com.test.test1;

public class B {
  int num = 3;
}
```

```java
package com.test;

import com.test.test1.*;

public class Main {
  public static void main(String[] args) {
    A a = new A(); // 패키지 동일
    B b = new B(); // 패키지 다름
    System.out.println(a.num); // 5
    System.out.println(b.num); // 접근 불가
  }
}
```

`protected`는 같은 패키지와 자식클래스에서 접근이 가능합니다.

```java
package com.test.test1;

public class B {
  protected int num2 = 3;
}
```

```java
package com.test.test1;

public class C {
  int num3 = 8;

  public int getNum2() {
    B b = new B();
    return b.num2; // B 클래스와 같은 패키지이므로 접근 가능
  }
}

```

```java
package com.test;

import com.test.test1.B;

public class A extends B {
  int num1 = 5;

  public int getNum1() {
    return num1;
  }

  public int getNum2() {
    return num2; // B를 상속받아 num2 필드에 접근 가능
  }
}
```

```java
package com.test;

import com.test.test1.*;

public class Main {
  public static void main(String[] args) {
    A a = new A();
    B b = new B();
    C c = new C();
    System.out.println(a.getNum2()); // 3
    System.out.println(c.getNum2()); // 3
    System.out.println(b.num2); // 접근 불가
  }
}
```

`public`은 어디에서나 접근이 가능합니다.

```java
package com.test.test1;

public class B {
  public int num2 = 3;
}
```

```java
package com.test.test1;

public class C {
  int num3 = 8;

  public int getNum2() {
    B b = new B();
    return b.num2; // B 클래스와 같은 패키지이므로 접근 가능
  }
}

```

```java
package com.test;

import com.test.test1.B;

public class A extends B {
  int num1 = 5;

  public int getNum1() {
    return num1;
  }

  public int getNum2() {
    return num2; // B를 상속받아 num2 필드에 접근 가능
  }
}
```

```java
package com.test;

import com.test.test1.*;

public class Main {
  public static void main(String[] args) {
    A a = new A();
    B b = new B();
    C c = new C();
    System.out.println(a.getNum2()); // 3
    System.out.println(c.getNum2()); // 3
    System.out.println(b.num2); // 3
  }
}
```
