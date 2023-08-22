---
layout: post
title: "[Java] 람다식"
subtitle: "람다, 람다식, Lambda"
description: "람다식(Lambda Expression)은 함수형 프로그래밍을 위해 자바 8에서 도입됐습니다. 람다식은 함수형 인터페이스를 간결한 방법으로 구현할 수 있습니다. 함수형 인터페이스는 하나의 추상 메서드가 있는 인터페이스입니다."
date: 2023-07-30 13:05:00 +0900
categories: java
comments: true
---

# 람다식(Lambda Expression)

### 람다식이란?

람다식(Lambda Expression)은 함수형 프로그래밍을 위해 자바 8에서 도입됐습니다. 람다식은 함수형 인터페이스를 간결한 방법으로 구현할 수 있습니다. 함수형 인터페이스는 하나의 추상 메서드가 있는 인터페이스입니다.

람다식의 사용 방법은 다음과 같습니다.

```java
(매개변수1, ...) => { 실행문1; ... };
```

```java
public interface Calculate {
    int add(int a, int b);
}


public class Main {
    public static void main(String[] args) {
        Calculate Calculate = (int a, int b) -> {
            return a + b;
        };

        int result = Calculate.add(1 , 2);
        System.out.println("result :" + result);
    }
}
```

```
// 실행 결과
result: 3
```

람다식을 사용할 때는 유추할 수 있는 값들은 생략해서 사용합니다.

#### 매개변수가 없는 람다식

매개변수가 없는 람다식은 다음과 같이 작성합니다.

```java
() -> { 실행문1; 실행문2; };
```

```java
public interface Message {
    void display();
}

public class Main {
    public static void main(String[] args) {
        Message msg = () -> {
            System.out.println("안녕하세요");
            System.out.println("감사해요");
        };

        msg.display();
    }
}
```

```
// 실행 결과
안녕하세요
감사해요
```

실행문이 하나일 경우 중괄호를 생략할 수 있습니다.

```java
() -> 실행문;
```

```java
public interface Message {
    void display();
}

public class Main {
    public static void main(String[] args) {
        Message msg = () -> System.out.println("안녕하세요");

        msg.display();
    }
}
```

```
// 실행 결과
안녕하세요
```

#### 매개변수가 있는 람다식

매개변수가 있는 람다식은 다음과 같이 작성합니다.

```java
(타입 매개변수1, ...) -> { 실행문1; 실행문2; };
(타입 매개변수1, ...) -> 실행문;
```

```java
public interface Message {
    void display(String str);
}

public class Main {
    public static void main(String[] args) {
        Message msg = (String str) -> System.out.println(str);

        msg.display("안녕하세요");
    }
}
```

```
// 실행 결과
안녕하세요
```

람다식의 매개변수 타입은 추상 메서드에서 유추 할 수 있기 때문에 보통 생략해서 작성합니다.

```java
public interface Message {
    void display(String str);
}

public class Main {
    public static void main(String[] args) {
        Message msg = (str) -> System.out.println(str);

        msg.display("안녕하세요");
    }
}
```

매개변수가 하나라면 소괄호를 생략할 수 있습니다.

```java
public interface Message {
    void display(String str);
}

public class Main {
    public static void main(String[] args) {
        Message msg = str -> System.out.println(str);

        msg.display("안녕하세요");
    }
}
```

### 리턴값이 있는 람다식

리턴값이 있는 경우 다음과 같이 작성합니다.

```java
(매개변수1, ...) -> { 실행문1; return 값;}
```

```java
public interface Calculate {
    int add(int a, int b);
}

public class Main {
    public static void main(String[] args) {
        Calculate calculate = (a, b) -> {
            System.out.println("함수 실행!");
            return a + b;
        };

        int result = calculate.add(1, 2);
        System.out.println("result: " + result);
    }
}
```

```
// 실행 결과
함수 실행!
result: 3
```

구현부가 `return`문 하나만 존재할 경우 중괄호와 `return` 키워드를 생략할 수 있습니다.

```java
public interface Calculate {
    int add(int a, int b);
}

public class Main {
    public static void main(String[] args) {
        Calculate calculate = (a, b) -> a + b;

        int result = calculate.add(1, 2);
        System.out.println("result: " + result);
    }
}
```

```
// 실행 결과
result: 3
```

### 함수형 인터페이스(Functional Interface)와 어노테이션

함수형 인터페이스는 하나의 추상 메서드만 포함하는 인터페이스입니다. 디폴트 또는 정적 메서드가 여러 개 있을 수 있지만 추상 메서드는 정확히 하나만 있어야 합니다.

`@FunctionalInterface` 은 함수형 인터페이스에 부합하는지 확인하기 위한 어노테이션이며, 둘 이상의 추상 메서드가 존재하면 컴파일 오류가 발생합니다.

```java
@FunctionalInterface
public interface Calculate {
    int add(int a, int b);
    default int mul(int a, int b) { return a * b; }
    static int sub(int a, int b) { return a / b; }

}

```

일반적인 함수형 인터페이스로는 `java.util.function` 패키지의 `Consumer`, `Supplier`, `Predicate`, `Function`이 있습니다.

#### Consumer\<T>

`Consumer` 인터페이스는 `accept()`라는 단일 추상 메서드가 있습니다. 이 메서드는 단일 인수를 받아 처리하고 결과를 반환하지 않습니다. (입력 데이터에 대해 특정 작업을 수행하지만 값을 반환할 필요가 없는 경우에 사용됩니다.)

```java
void accept(T t);
```

```java
import java.util.function.Consumer;

public class Main {
    public static void main(String[] args) {
        Consumer<String> printer = str -> System.out.println(str);

        printer.accept("출력");
    }
}
```

```
// 실행 결과
출력
```

#### Supplier\<T>

`Supplier` 인터페이스는 `get()`이라는 단일 추상 메서드가 있습니다. 이 메서드는 인수를 받지 않고 지정된 유형 T의 값을 반환합니다. (외부 입력 없이 데이터를 생성할 때 사용됩니다.)

```java
T get();
```

```java
import java.util.function.Supplier;

public class Main {
    public static void main(String[] args) {
        Supplier<Integer> randomNumberSupplier = () -> (int) (Math.random() * 100);

        int randomNumber = randomNumberSupplier.get();
        System.out.println("무작위 숫자: " + randomNumber);
    }
}
```

```
// 실행 결과
무작위 숫자: 31
```

#### Predicate\<T>

`Predicate` 인터페이스는 `test()`라는 단일 추상 메서드가 있습니다. 이 메서드는 지정된 유형의 인수를 받으며 부울 값을 반환합니다. (데이터에 대한 필터링 또는 유효성 검사를 수행할 때 사용됩니다.)

```java
boolean test(T t);
```

```java
import java.util.function.Predicate;

public class Main {
    public static void main(String[] args) {
        Predicate<Integer> isEven = number -> number % 2 == 0;

        int num = 10;
        boolean result = isEven.test(num);
        System.out.println(num + "은(는) 짝수인가? " + result);
    }
}
```

```
// 실행 결과
10은(는) 짝수인가? true
```

#### Function<T, R>

`Function` 인터페이스는 `apply()`라는 단일 추상 메서드가 있습니다. 이 메서드는 지정된 유형의 인수를 받으며 다른 지정된 유형의 값을 반환합니다. (입력 데이터를 출력 데이터로 변환하는 동작을 정의할 때 사용됩니다.)

```java
R apply(T t);
```

```java
import java.util.function.Function;
public class Main {
    public static void main(String[] args) {
        Function<Integer, String> intToString = number -> "숫자는 " + number + "입니다.";

        int num = 10;
        String result = intToString.apply(num);
        System.out.println(result);
    }
}
```

```
// 실행 결과
숫자는 10입니다.
```

### 메서드 참조

메서드 참조는 람다식을 사용할 때 불필요한 상용구 코드를 제거하여 코드 가독성을 높이기 위해 사용됩니다.

#### 정적 메서드 참조

정적 메서드를 참조할 경우에는 클래스 이름 뒤에 :: 기호를 붙인 다음 정적 메서드명을 기술합니다.

```java
className::staticMethodName
```

```java
public class StringUtils {
    public static String convertToUpperCase(String str) {
        return str.toUpperCase();
    }
}

```

```java
import java.util.function.Function;
public class Main {
    public static void main(String[] args) {
        // 람다식
        Function<String, String> upperCaseConverter1 = str -> StringUtils.convertToUpperCase(str);
        // 정적 메서드 참조
        Function<String, String> upperCaseConverter2 = StringUtils::convertToUpperCase;

        String input = "hello";

        String result1 = upperCaseConverter1.apply(input);
        String result2 = upperCaseConverter2.apply(input);

        System.out.println("Uppercase: " + result1);
        System.out.println("Uppercase: " + result2);
    }
}
```

```
// 실행 결과
Uppercase: HELLO
Uppercase: HELLO
```

#### 인스턴스 메서드에 대한 참조

인스턴스 메서드를 참조하는 경우 객체를 생성한 다음 참조 변수 뒤에 :: 기호를 붙인 다음 인스턴스 메서드명을 기술합니다.

```
object::instanMethodName
```

```java
public class Converter {
    public String convertToString(int number) {
        return "숫자는 " + number + "입니다.";
    }
}
```

```java
import java.util.function.Function;

public class Main {
    public static void main(String[] args) {
        Converter converter = new Converter();

        Function<Integer, String> lambdaConverter = number -> converter.convertToString(number);
        System.out.println(lambdaConverter.apply(10));

        Function<Integer, String> methodReference = converter::convertToString;
        System.out.println(methodReference.apply(10));
    }
}
```

```
// 실행 결과
숫자는 10입니다.
숫자는 10입니다.
```

#### 생성자에 대한 참조

생성자 참조는 클래스 이름 뒤에 :: 기호를 붙이고 `new` 연산자를 기술합니다.

```java
클래스::new
```

```java
@FunctionalInterface
public interface PersonFactory {
    Person createPerson(String name, int age);
}
```

```java
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void display() {
        System.out.println(name + "은(는) " + age + "살");
    }
}
```

```java
public class Main {
    public static void main(String[] args) {

        PersonFactory lambdaFactory = (name, age) -> new Person(name, age);
        Person personLambda = lambdaFactory.createPerson("짱구", 5);
        personLambda.display();

        PersonFactory referenceFactory = Person::new;
        Person personReference = referenceFactory.createPerson("마르코", 9);
        personReference.display();
    }
}
```

```
// 실행 결과
짱구은(는) 5살
마르코은(는) 9살
```
