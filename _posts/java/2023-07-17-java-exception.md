---
layout: post
title: "[Java] 예외처리"
subtitle: "예외처리, 예외, exception"
description: "자바에서 예외는 프로그램이 예상하고 복구할 수 있는 요인으로 인해 발생하는 반면, 에러는 일반적으로 프로그램이 제어할 수 없는 심각한 문제를 나타냅니다. 예외는 Checked Exception, Unchecked Exception 2가지로 나뉩니다."
date: 2023-07-17 14:15:00+0900
categories: java
comments: true
---

# 예외처리

### 에러(Error)와 예외(Exception)

예외는 프로그램이 예상하고 복구할 수 있는 요인으로 인해 발생하는 반면, 에러는 일반적으로 프로그램이 제어할 수 없는 심각한 문제를 나타냅니다.

### Exception의 2가지 종류

예외는 `Checked Exception`, `Unchecked Exception` 2가지로 나뉩니다.

**Checked Exception**: `Checked Exception`은 컴파일러에서 프로그래머가 명시적으로 처리하도록 요구하는 예외입니다. 이러한 예외는 컴파일 시점에서 확인되며, `try-catch` 블록을 사용하여 예외를 처리하거나 `throws` 키워드를 사용하여 예외를 떠넘깁니다. 예로는 `IOException`, `SQLException`, `ClassNotFoundException` 등이 있습니다.

**Unchecked Exception**: `Unchecked Exception`은 명시적으로 처리하지 않아도 되는 예외입니다. 일반적으로 프로그래밍 오류나 예상치 못한 상황으로 인해 발생하며 프로그램 실행 중에 발생합니다. 예로는 `NullPointerException`, `ArrayIndexOutOfBoundsException` 등이 있습니다. `Unchecked Exception`을 처리하는 것이 의무 사항은 아니지만 프로그램의 안정성을 보장하기 위해 처리하는 것이 좋습니다.

### 예외 처리 코드

예외는 `try-catch` 블록으로 처리할 수 있습니다. 예외를 던질 수 있는 코드는 `try` 블록 내에 배치되고, 발생하는 예외는 `catch` 블록에서 처리됩니다.

```java
public class Main {
    public static void main(String[] args) {
        int num = 5;
        int result = num / 0; // ArithmeticException 예외 발생
        System.out.println(result); // 출력 x
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        try {
            int num = 5;
            int result = num / 0; // ArithmeticException 예외 발생
            System.out.println(result); // 출력 x
        } catch (Exception e) {
            System.out.println("0으로 나눌 수 없습니다."); // 출력 o
        }
    }
}
```

`try` 블록에서는 몇 가지의 예외가 발생할 수 있습니다. 각 예외마다 처리하는 코드가 다르다면, `catch` 블록을 여러 번 사용하여 예외 처리 코드를 다르게 작성할 수 있습니다.

```java
public class Main {
    public static void main(String[] args) {
        String[] test = {"10", "십"};

        for(int i = 0; i <= test.length; i++) {
            try {
                int value = Integer.parseInt(test[i]);
                System.out.println(value);
            } catch (NumberFormatException e) {
                System.out.println(e);
            } catch (ArrayIndexOutOfBoundsException e) {
                System.out.println(e);
            }
        }
    }
}
```

```
// 실행 결과
10
java.lang.NumberFormatException: For input string: "십"
java.lang.ArrayIndexOutOfBoundsException: Index 2 out of bounds for length 2
```

둘 이상 예외의 예외 처리 코드가 같다면 "\|"를 사용하여 하나의 `catch` 블록으로 처리할 수 있습니다.

```java
public class Main {
    public static void main(String[] args) {
        String[] test = {"10", "십"};

        for(int i = 0; i <= test.length; i++) {
            try {
                int value = Integer.parseInt(test[i]);
                System.out.println(value);
            } catch (NumberFormatException | ArrayIndexOutOfBoundsException e) {
                System.out.println(e);
            }
        }
    }
}
```

```
// 실행결과
10
java.lang.NumberFormatException: For input string: "십"
java.lang.ArrayIndexOutOfBoundsException: Index 2 out of bounds for length 2
```

주의할 점은 예외가 발생하면 위에서부터 검사 대상이 되기 때문에 처리해야 할 예외 클래스들이 상속 관계에 있다면 하위 클래스는 `catch` 블록을 위에 작성해야 합니다.

```java
public class Main {
    public static void main(String[] args) {
        try {
            int num = 5;
            int result = num / 0;
            System.out.println(result);
        } catch (ArithmeticException e) {
            System.out.println("ArithmeticException");
        } catch (Exception e) { // 상위 클래스는 밑에 작성
            System.out.println("Exception");
        }
    }
}
```

### finally

`try-catch` 블록에서 예외와 상관없이 실행되어야 하는 코드가 있다면 `finally` 블록을 사용하면 됩니다.

```java
public class Main {
    public static void main(String[] args) {
        int num = 5;
        try {
            int result = num / 0;
            System.out.println(result);
        } catch (ArithmeticException e) {
            System.out.println("ArithmeticException");
        } finally {
            System.out.println("num: " + num);
        }
    }
}
```

```
// 실행 결과
ArithmeticException
num: 5
```

### 리소스 자동 닫기

자바에서는 리소스를 사용한 후에 닫지 않으면 계속 할당된 상태로 남아 있기 때문에 닫는 것이 중요합니다.

자바에서 리소스를 사용하다가 예외가 발생하는 경우가 있습니다. 이 경우 리소스를 안전하게 닫기 위해서 `finally` 블록에 리소스를 닫는 코드를 작성하면 됩니다.

```java
import java.io.FileWriter;
import java.io.IOException;

public class Main {
    public static void main(String[] args) {
        FileWriter fileWriter = null;
        try {
            fileWriter = new FileWriter("file.txt");
            fileWriter.write("안녕");
        } catch (IOException e) {
            System.out.println(e.getMessage());
        } finally {
            if (fileWriter != null) {
                try {
                    fileWriter.close();
                } catch (IOException e) {
                    System.out.println(e.getMessage());
                }
            }
        }
    }
}
```

`try-with-resources` 문을 이용하면 리소스를 쉽게 처리할 수 있습니다. `try-with-resources` 문은 `try` 괄호에 리소스를 여는 코드를 작성하면 예외가 발생하더라도 리소스가 자동으로 해제되도록 합니다.

```java
import java.io.FileWriter;
import java.io.IOException;

public class Main {
    public static void main(String[] args) {
        try (FileWriter fileWriter = new FileWriter("file.txt")) {
            fileWriter.write("안녕");
        } catch (IOException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

### 예외 던지기(throws)

메서드 내에서 예외가 발생하면 `try-catch` 블록으로 처리할 수 있지만, 메서드 내에서 예외 처리를 하지 않고 메서드를 호출한 곳에서 예외를 처리하도록 할 수 있습니다.

예외를 넘기기 위해선 `throws` 키워드를 사용하면 됩니다.

```java
접근제어자 리턴타입 메소드명(매개변수, ...) throws 예외클래스, ... {
  ...
}
```

```java
public class Main {
    public static void main(String[] args) {
        try {
            int result = divide(10, 0);
            System.out.println(result);
        } catch (Exception e) {
            System.out.println("0으로 나눌 수 없습니다.");
        }
    }

    private static int divide(int a, int b) throws ArithmeticException {
        return a / b;
    }
}
```

```
// 실행 결과
0으로 나눌 수 없습니다.
```

### 예외 발생 시키기

`throw` 키워드를 이용해서 강제로 예외를 발생시킬 수 있습니다.

```java
public class Main {
    public static void main(String[] args) {
        try {
            throw new Exception("예외 강제로 발생!");
        } catch (Exception e) {
            System.out.println(e.getMessage()); // "예외 강제로 발생!" 출력
        }
    }
}
```

### 사용자 정의 예외

직접 정의하여 사용하는 예외를 사용자 정의 예외라고 합니다. 사용자 정의 예외 클래스를 만들 때 컴파일러가 체크하는 예외이면 `Exception`을 체크하지 않는 예외이면 `RuntimeException`을 상속하면 됩니다.

```java
public class SomeException extends [ Exception | RuntimeException ] {
  public SomeException() {}
  public SomeException(String message) { super(message); }
}
```

생성자는 보통 두개를 선언합니다. 하나는 매개 변수가 없는 기본 생성자이고, 다른 하나는 예외 메시지를 전달하기 위해 부모 생성자을 호출합니다.

```java
// SomeException.java
public class SomeException extends RuntimeException {
    public SomeException() {};

    public SomeException(String message) {
        super(message);
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        try {
            throw new SomeException("사용자 정의 예외!");
        } catch (Exception e) {
            System.out.println(e.getMessage()); // "사용자 정의 에외!" 출력
        }
    }
}
```
