---
layout: post
title: "[Java] 스트림"
subtitle: "스트림, stream"
date: 2023-08-03 11:25:00 +0900
categories: java
comments: true
---

# 스트림

### 스트림(Stream)

컬렉션 및 배열의 요소를 하나씩 참조하면서 코드를 실행하기 위해 스트림을 사용합니다. 스트림은 생성, 중간 연산, 최종 연산 단계를 거칩니다.

### 스트림 생성

스트림 생성은 Stream 객체를 얻는 초기 단계입니다. 스트림은 컬렉션, 배열과 같은 다양한 데이터 소스에서 생성하거나 Stream 클래스에서 제공하는 정적 메서드를 사용하여 생성할 수 있습니다.

컬렉션에서 `stream()` 메서드를 호출하여 직접 스트림을 생성할 수 있습니다. 이 메서드는 `Collection` 인터페이스를 구현하는 모든 클래스에서 사용할 수 있습니다.

```java
import java.util.List;
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = List.of(1, 2, 3, 4, 5);
        Stream<Integer> stream = numbers.stream();
    }
}
```

배열에서 스트림을 만들려면 `Arrays.stream()` 메서드를 사용하면 됩니다.

```java
import java.util.Arrays;
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        String[] names = {"짱구", "철수", "맹구"};
        Stream<String> stream = Arrays.stream(names);
    }
}
```

`Stream.of()` 메서드를 사용하면 개별 요소를 전달해 스트림을 생성할 수 있습니다.

```java
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        Stream<String> stream = Stream.of("짱구", "철수", "맹구");
    }
}
```

### 중간 연산

중간 연산 단계는 각 요소를 수정, 필터링 등을 수행하기 위한 단계입니다. 중간 연산은 0개 이상의 연산을 할 수 있으며, 최종 연산 단계가 호출 될 때까지 연산이 수행되지 않습니다.

#### filter

`filter()` 메서드는 주어진 조건을 만족하는 요소를 필터링하여 새 스트림을 반환합니다.

```java
filter(Predicate<? super T> predicate)
```

```java
import java.util.List;
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = List.of(1, 2, 3, 4, 5);
        Stream<Integer> filteredStream = numbers.stream().filter(num -> num % 2 == 0); // 2 4
    }
}
```

#### map

`map()` 메서드는 주어진 함수를 스트림의 각 요소에 적용 후 변환된 요소를 새 스트림으로 반환합니다.

```java
map(Function<? super T,? extends R> mapper)
```

```java
import java.util.List;
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        List<String> names = List.of("짱구", "흰둥이", "맹구");
        Stream<Integer> nameLengths = names.stream().map(name -> name.length()); // 2 3 2
    }
}
```

#### sorted

`sorted()` 메서드는 오름차순 또는 내림차순으로 정렬 후 새 스트림을 반환합니다.

```java
sorted()
```

```java
import java.util.List;
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = List.of(5, 3, 1, 4, 2);
        Stream<Integer> sortedStream = numbers.stream().sorted(); // 1 2 3 4 5
    }
}
```

#### distinct

`distinct()` 메서드는 Stream에서 중복 요소를 제거하고 고유한 요소가 있는 새 스트림을 반환합니다.

```java
distinct()
```

```java
import java.util.List;
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = List.of(1, 2, 3, 2, 4, 3, 5);
        Stream<Integer> uniqueNumbers = numbers.stream().distinct(); // 1 2 3 4 5
    }
}
```

#### limit, skip

`limit()` 메서드는 스트림의 요소 수를 지정된 크기로 제한 후 새 스트림을 반환합니다.

```java
limit(long maxSize);
```

```java
import java.util.List;
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = List.of(1, 2, 3, 4, 5);
        Stream<Integer> limitedStream = numbers.stream().limit(3); // 1 2 3
    }
}
```

`skip()` 메서드는 인자로 전달된 'n'만큼 요소를 건너띄고 그 이후의 요소를 새 스트림으로 반환합니다.

```java
skip(long n)
```

```java
import java.util.List;
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = List.of(1, 2, 3, 4, 5);
        Stream<Integer> skippedStream = numbers.stream().skip(2); // 3 4 5
    }
}
```

#### flatMap

`flatMap()` 메서드는 중첩된 컬렉션이나 배열을 단일 스트림으로 변환할 때 사용하며 새 스트림을 반환합니다.

```java
flatMap(Function<? super T,? extends Stream<? extends R>> mapper)
```

```java
import java.util.List;
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        List<List<Integer>> nestedNumbers = List.of(List.of(1, 2), List.of(3, 4, 5), List.of(6, 7, 8));
        Stream<Integer> flattenedStream = nestedNumbers.stream().flatMap(List::stream);
    }
}
```

### 최종 연산

최종 연산 단계에서는 결과값을 반환하고 스트림을 닫아 스트림을 재사용할 수 없도록 합니다.

#### forEach

`forEach()` 메서드는 Stream의 각 요소에 결과를 반환하지 않는 특정 작업을 수행하는 데 사용됩니다.

```java
forEach(Consumer<? super T> action)
```

```java
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> names = List.of("짱구", "철수", "맹구");
        names.stream().forEach(System.out::println);
    }
}
```

```
// 실행결과
짱구
철수
맹구
```

#### max, min, count

`max()` 메서드는 스트림에서 가장 큰 값을 가진 요소를 포함하는 `Optional` 객체를 반환합니다. 스트림이 비어 있다면 빈 `Optional`을 반환합니다.

```java
max(Comparator<? super T> comparator)
```

```java
import java.util.Optional;
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        Stream<Integer> stream = Stream.of(5, 8, 2, 10, 3);

        Optional<Integer> max = stream.max(Integer::compare);

        if (max.isPresent()) {
            System.out.print("최댓값: " + max.get());
        } else {
            System.out.print("비어있음");
        }
    }
}
```

```
// 실행 결과
최댓값: 10
```

```java
import java.util.Optional;
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        Stream<Integer> stream = Stream.of();

        Optional<Integer> max = stream.max(Integer::compare);

        if (max.isPresent()) {
            System.out.print("최댓값: " + max.get());
        } else {
            System.out.print("비어있음");
        }
    }
}
```

```
// 실행 결과
비어있음
```

`min()` 메서드는 스트림에서 가장 작은 값을 가진 요소를 포함하는 `Optional` 객체를 반환합니다. 스트림이 비어 있다면 빈 `Optional`을 반환합니다.

```java
min(Comparator<? super T> comparator)
```

```java
import java.util.Arrays;
import java.util.List;
import java.util.Optional;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(5, 2, 8, 1, 10);

        Optional<Integer> min = numbers.stream().min(Integer::compareTo);

        if (min.isPresent()) {
            System.out.print("최솟값: " + min.get());
        } else {
            System.out.print("비어있음");
        }
    }
}
```

```
// 실행 결과
최솟값: 1
```

```java
import java.util.Arrays;
import java.util.List;
import java.util.Optional;

public class Main {
    public static void main(String[] args) {
        List<Integer> emptyList = Arrays.asList();

        Optional<Integer> min = emptyList.stream().min(Integer::compareTo);

        if (min.isPresent()) {
            System.out.print("최솟값: " + min.get());
        } else {
            System.out.print("비어있음");
        }
    }
}
```

```
// 실행 결과
비어있음
```

`count()` 메서드는 스트림에 있는 요소의 수를 `long` 타입의 값으로 반환합니다.

```java
long count()
```

```java
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5);

        long count = stream.count();

        System.out.print("요소의 수: " + count);
    }
}
```

```
// 실행 결과
요소의 수: 5
```

#### anyMatch, allMatch, noneMatch

`anyMatch()` 메서드는 스트림 요소 중 주어진 조건과 일치하는 요소가 하나라도 있으면 'true'를 반환하고, 일치하는 요소가 없으면 'false'를 반환합니다. (일치하는 요소가 있으면 조건 비교를 그만합니다.)

```java
anyMatch(Predicate<? super T> predicate)
```

```java
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        Stream<Integer> stream = Stream.of(-1, -2, 3, -4, -5);

        boolean anyPositive = stream.anyMatch(num -> {
            System.out.println(num);
            return num > 0;
        });

        System.out.print("요소 중 양수가 있는가? " + anyPositive);
    }
}
```

```
// 실행 결과
-1
-2
3
요소 중 양수가 있는가? true
```

`allMatch()` 메서드는 스트림의 모든 요소가 주어진 조건과 일치하면 'true'를 반환하고, 요소 중 하나라도 일치하지 않으면 'false'를 반환합니다.

```java
allMatch(Predicate<? super T> predicate)
```

```java
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5);

        boolean allPositive = stream.allMatch(num -> {
            System.out.println(num);
            return num > 0;
        });

        System.out.print("모든 요소가 양수인가? " + allPositive);
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
모든 요소가 양수인가? true
```

`noneMatch()` 메서드는 스트림의 요소 중 주어진 조건과 일치하는 요소가 없다면 "true" 반환하고, 일치하는 요소가 있으면 "false"를 반환하는 메서드입니다. (일치하는 요소가 있으면 조건 비교를 그만합니다.)

```java
noneMatch(Predicate<? super T> predicate)
```

```java
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        Stream<Integer> stream = Stream.of(1, 2, -3, 4, 5);

        boolean noneNegative = stream.noneMatch(num -> {
            System.out.println(num);
            return num < 0;
        });

        System.out.print("음수가 존재하지 않는가? " + noneNegative);
    }
}
```

```
// 실행 결과
1
2
-3
음수가 존재하지 않는가? false
```

#### collect

`collect()` 메서드는 지정된 Collector를 각 요소에 적용합니다. 일반적으로 Stream의 요소를 컬렉션(List, Set, Map)으로 변환할 때 많이 사용합니다.

```java
collect(Collector<? super T, A, R> collector)
```

```java
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        Stream<String> stream = Stream.of("짱구", "철수", "맹구");

        List<String> collectedList = stream.collect(Collectors.toList());

        System.out.print("방범대 리스트: " + collectedList);
    }
}
```

```
// 실행 결과
방범대 리스트: [짱구, 철수, 맹구]
```
