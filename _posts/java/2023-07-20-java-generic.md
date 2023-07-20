---
layout: post
title: "[Java] 제너릭"
subtitle: "제너릭, Generic, 래퍼 클래스"
date: 2023-07-20 11:23:00 +0900
categories: java
comments: true
---

# 제너릭

### 래퍼 클래스(Wrapper 클래스)

래퍼 클래스는 기본 타입(int, boolean 등)을 객체로 사용할 수 있도록하는 클래스입니다.

| 기본 클래스 | 래퍼 클래스 |
| ----------- | ----------- |
| boolean     | Boolean     |
| byte        | Byte        |
| char        | Character   |
| short       | Short       |
| int         | Integer     |
| long        | Long        |
| float       | Float       |
| double      | Double      |

### 박싱(boxing)과 언박싱(unboxing)

기본 타입의 값을 래퍼 클래스 객체로 변환하는 것을 박싱, 래퍼 클래스 객체에서 기본 값을 추출하는 것을 언박싱이라고 합니다.

```java
public class Main {
    public static void main(String[] args) {
        int num1 = 10;
        Integer num2 = new Integer(num1); // 박싱
        int num3 = num2.intValue(); // 언박싱
    }
}
```

자바에서는 명시적으로 박싱, 언박싱을 할 수 있고 자동으로 박싱, 언박싱을 할 수도 있습니다.

```java
public class Main {
    public static void main(String[] args) {
        // 명시적 박싱, 언박싱
        int value = 10;
        Integer num1 = (Integer) value;
        int num2 = (int) num1;

        // 자동 박싱, 언박싱
        Integer num3 = 10;
        int num4 = num1;
    }
}
```

### 제너릭(Generic)

제네릭은 타입을 미리 정해놓지 않고 외부에서 필요한 타입을 지정할 수 있는 기능입니다.

선언 방법은 "<>" 괄호와 괄호 안에 타입 파라미터명을 작성하면 됩니다. 타입 파라미터명은 어떠한 문자를 사용해도 되며, 여러 개일 경우 쉼표로 구분하여 작성하면 됩니다. 보통 타입 파리미터명은 아래와 같이 작성합니다.

| 타입 | 설명    |
| ---- | ------- |
| \<T> | Type    |
| \<E> | Element |
| \<K> | Key     |
| \<V> | Value   |
| \<N> | Number  |

클래스 및 인터페이스에서 선언 시 이름 뒤에 선언하면 됩니다.

```java
접근제어자 class 클래스명 <T> {...}
접근제어자 interface 인터페이스명 <T> {...}
```

```java
public class Box <T> {
    private T content;

    public void setContent(T content) {
        this.content = content;
    }

    public T getContent() {
        return content;
    }
}
```

제네릭 클래스를 생성할 때는 실제 타입을 명시해야 합니다. 타입을 명시할 때 주의할 점은 기본 타입은 사용할 수 없습니다.

```java
public class Box <T> {
    private T content;

    public void setContent(T content) {
        this.content = content;
    }

    public T getContent() {
        return content;
    }
}

public class Main {
    public static void main(String[] args) {
        // Box<int> box = new Box<>(); // 에러 발생
        Box<Integer> box = new Box<>();

        box.setContent(10);
        int content = box.getContent();
    }
}
```

메서드에서 선언 시 리턴타입 앞에 선언합니다. 선언된 타입 파라미터는 리턴타입, 매개변수에서 사용됩니다.

```java
접근제어자 <T> 리턴타입 메서드명(매개변수, ...) {...}
```

```java
public class Box {
    public Object content;

    public <T> void setContent(T content) {
        this.content = content;
    }
}

public class Main {
    public static void main(String[] args) {
        Box box = new Box();

        box.setContent(new Integer(10));
        System.out.println(box.content); // 10
        box.setContent("안녕");
        System.out.println(box.content); // 안녕
    }
}
```

제네릭을 사용하면 타입에 대한 유연성과 안정성을 확보할 수 있고, 타입 변환 및 타입 검사에 들어가는 노력을 줄일 수 있습니다.

예로 `Box` 클래스의 `content` 필드가 있습니다.

```java
public class Box {
    public Object content;
}

public class Main {
    public static void main(String[] args) {
        Box box = new Box();

        box.content = new Integer(10);
        System.out.println(box.content); // 10

        box.content = new String("안녕");
        System.out.println(box.content); // 안녕
    }
}
```

`content` 필드는 `Object` 타입으로 선언되어 모든 타입의 값을 대입할 수 있습니다. 대입만 한다면 불편한 점은 없지만 `content`의 값을 추출하거나 특정 메서드를 사용한다면, Object 타입에 어떠한 객체가 대입되었는지 불확실하기 때문에 강제 타입 변환 후 사용해야 하는 번거로움이 있습니다.

```java
public class Main {
    public static void main(String[] args) {
        Box box = new Box();

        box.content = new String("안녕");
//        String content2 = box.content; // 에러 발생
        String content2 = (String) box.content; // String 타입으로 값을 대입하기 위해선 강제 타입 변환 필요
        String[] strings = ((String) box.content).split(""); // String 클래스에 정의된 메서드를 사용하기 위해선 강제 타입 변환 필요
    }
}
```

제네릭을 사용하면 강제 타입 변환하는 노력을 줄일 수 있습니다.

```java
public class Box <T> {
    public T content;
}

public class Main {
    public static void main(String[] args) {
        Box<String> box = new Box();

        box.content = new String("안녕");
        String content = box.content;
        String[] strings = box.content.split("");
    }
}
```

### 와일드카드

와일드카드(<?>)란 모든 타입으로 대체할 수 있는 타입입니다.

```java
public class Main {
    public static void printList(List<?> list) {
        for (Object element : list) {
            System.out.println(element);
        }
    }

    public static void main(String[] args) {
        List<Integer> intList = List.of(1, 2, 3, 4, 5);
        List<String> stringList = List.of("사과", "바나나", "오렌지");

        printList(intList);
        printList(stringList);
    }
}
```

```
// 실행 결과
1
2
3
4
5
사과
바나나
오렌지
```

### 와일드카드의 상한과 하한

타입 파라미터의 구체적인 타입을 제한할 필요가 있을 때 제한된 타입 파라미터(Bounded Type Parameter)를 사용합니다.

#### 상한 제한된 와일드카드(Upper Bounded Wildcards)

상한 제한된 와일드카드를 사용하면 대입할 수 있는 타입을 특정 타입 또는 특정 하위 타입으로 제한할 수 있습니다.

```java
public <? extends 특정타입> 리턴타입 메서드명(매개변수, ...) {...}
```

예로 어떤 리스트의 요소를 출력하는 메서드를 만드는데, 이 메서드의 매개변수 타입을 `Number` 또는 하위 클래스(Byte, Short, Integer, Long, Double)로 제한한다면 아래와 같이 작성하면 됩니다.

```java
import java.util.List;

public class Main {
    public static void printList(List<? extends Number> list) {
        for (Number n : list) {
            System.out.println(n);
        }
    }

    public static void main(String[] args) {
        List<Integer> intList = List.of(1, 2, 3);
        List<Double> doubleList = List.of(1.0, 2.0, 3.0);
        List<String> stringList = List.of("사과", "바나나", "오렌지");

        printList(intList);
        printList(doubleList);
        printList(stringList); // String은 Number를 상속하지 않기 때문에 에러 발생
    }
}
```

#### 하한 제한된 와일드카드(Lower Bounded Wildcards)

하한 제환된 와일드 카드는 필요한 타입이 특정 타입과 같거나 특정 타입의 상위 타입일 때 사용합니다.

```java
public <? super 특정타입> 리턴타입 메서드명(매개변수, ...) {...}
```

```java
public void processList(List<? super Integer> list) {

    list.add(new Integer(20));
    list.add(new Float(2.0f)); // Float 타입은 Integer 타입 또는 Integer 상위 타입이 아니여서 에러 발생

}
```
