---
layout: post
title: "[Java] 컬렉션 프레임워크"
subtitle: "컬렉션 프레임워크, 컬렉션, Collection, List, Set, Map"
description: "컬렉션 프레임워크는 자바에서 제공하는 데이터를 쉽고 효과적으로 처리할 수 있는 인터페이스와 클래스 집합입니다. 주요 인터페이스로는 List, Set, Map이 있습니다. List는 중복된 데이터를 저장할 수 있으며, 데이터의 순서를 유지하고 각 요소마다 인덱스를 부여하는 특징이 있습니다. Set은 List와 다르게 저장 순서가 유지되지 않고 데이터를 중복해서 저장할 수 없는 특징이 있습니다. Map은 키(Key)와 값(Value)을 하나의 쌍으로 저장합니다. 키는 중복 저장될 수 없고 값은 중복 저장할 수 있습니다. 다른 값을 가진 중복된 키를 저장하면 새로운 값으로 대체됩니다."
date: 2023-07-22 10:36:00 +0900
categories: java
comments: true
---

# 컬렉션 프레임워크

### 컬렉션 프레임워크란?

컬렉션 프레임워크는 자바에서 제공하는 데이터를 쉽고 효과적으로 처리할 수 있는 인터페이스와 클래스 집합입니다.

주요 인터페이스로는 List, Set, Map이 있습니다.

### List

List는 중복된 데이터를 저장할 수 있으며, 데이터의 순서를 유지하고 각 요소마다 인덱스를 부여하는 특징이 있습니다. 인덱스는 0부터 시작합니다.

List 인터페이스에서 제공하는 몇 가지 메서드들은 다음과 같습니다.

| 메서드              | 설명                                                        |
| ------------------- | ----------------------------------------------------------- |
| add(E e)            | 요소를 끝에 추가합니다.                                     |
| add(int index, E e) | 리스트의 지정된 위치에 지정된 요소를 삽입합니다.            |
| get(int index)      | 지정된 위치에 있는 요소를 반환합니다.                       |
| size()              | 리스트의 요소 수를 반환합니다.                              |
| indexOf(Object o)   | 리스트에서 지정된 요소가 처음 나타나는 인덱스를 반환합니다. |
| remove(int inedex)  | 리스트에서 지정된 위치에 있는 요소를 제거합니다.            |
| clear()             | 모든 요소를 제거합니다.                                     |

List 인터페이스를 구현하는 클래스는 ArrayList, LinkedList, Vector 등이 있습니다.

#### ArrayList

ArrayList의 특징은 배열과는 달리 동적으로 크기를 늘릴 수 있으며 요소에 자주 접근하는 상황에서 효율적입니다.

```java
List<자료형> 리스트명 = new ArrayList<자료형(생략가능)>();
```

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> fruits = new ArrayList<>();

        fruits.add("사과");
        fruits.add("바나나");
        printFruits(fruits);

        fruits.add(1,"포도" );
        printFruits(fruits);

        fruits.remove(0);
        printFruits(fruits);
    }

    public static void printFruits(List<?> fruits) {
        int size = fruits.size();

        for(int i = 0; i < size; i++) {
            if (i == size - 1) {
                System.out.println(fruits.get(i));
                continue;
            }
            System.out.print(fruits.get(i)+" ");
        }
    }
}
```

```
// 실행결과
사과 바나나
사과 포도 바나나
포도 바나나
```

#### LinkedList

LinkedList의 요소는 배열과 같이 연속된 메모리 위치에 저장되지 않고 참조를 통해 연결됩니다. 요소를 추가하거나 제거할 때 `ArrayList`보다 더 좋은 성능을 보입니다.

```java
List<자료형> 리스트명 = new LinkedList<자료형(생략가능)>();
```

```java
public class Main {
    public static void main(String[] args) {
        List<Integer> numbers1 = new LinkedList<>();
        List<Integer> numbers2 = new ArrayList<>();

        long startTime;
        long endTime;

        startTime = System.nanoTime();
        for(int i = 0; i < 10000; i++) {
            numbers1.add(0, i);
        }
        endTime = System.nanoTime();
        System.out.printf("소요시간: %d \n", endTime - startTime);

        startTime = System.nanoTime();
        for(int i = 0; i < 10000; i++) {
            numbers2.add(0, i);
        }
        endTime = System.nanoTime();
        System.out.printf("소요시간: %d", endTime - startTime);
    }

}
```

```
// 실행 결과
소요시간: 2051500
소요시간: 4349600
```

### Set

Set은 List와 다르게 저장 순서가 유지되지 않고 데이터를 중복해서 저장할 수 없는 특징이 있습니다.

Set 인터페이스에서 제공하는 메서드는 다음과 같습니다.

| 메서드             | 설명                                            |
| ------------------ | ----------------------------------------------- |
| add(E e)           | 지정된 요소가 아직 없으면 Set에 추가합니다.     |
| remove(Object o)   | 지정된 요소가 있으면 Set에서 제거합니다.        |
| contains(Object o) | Set에 지정된 요소가 포함되어 있는지 확인합니다. |
| size()             | Set의 요소 수를 반환합니다.                     |
| isEmpty()          | Set이 비어 있는지 확인합니다.                   |
| clear()            | Set에서 모든 요소를 ​​제거합니다.               |

Set 인터페이스를 구현하는 HashSet, TreeSet, LinkedHashSet 등 여러 클래스가 있습니다.

#### HashSet

HashSet은 서로 다른 객체라도 hashCode() 메서드의 리턴값이 같고, equals() 메서드가 true를 리턴한다면 중복 저장하지 않습니다.

```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void display() {
        System.out.printf("%s는 %d살 \n", name, age);
    }

    @Override
    public int hashCode() {
        return name.hashCode() + age;
    }

    @Override
    public boolean equals(Object obj) {
        if ( ((Person)obj).name.equals(name) && (((Person)obj).age) == age)  {
            return true;
        } else
            return false;
    }
}
```

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Set<Person> peopleSet = new HashSet<>();

        Person person1 = new Person("철수", 5);
        Person person2 = new Person("짱구", 5);
        Person person3 = new Person("철수", 5);

        peopleSet.add(person1);
        peopleSet.add(person2);
        peopleSet.add(person3);

        System.out.println("저장된 수: " + peopleSet.size());

        for(Person p: peopleSet) {
            p.display();
        }
    }
}
```

```
// 실행 결과
저장된 수: 2
철수는 5살
짱구는 5살
```

#### TreeSet

TreeSet의 특징은 요소를 오름차순으로 저장합니다.

```java
import java.util.Set;
import java.util.TreeSet;

public class Main {
    public static void main(String[] args) {
        Set<Integer> numsSet = new TreeSet<>();

        numsSet.add(1);
        numsSet.add(7);
        numsSet.add(4);
        numsSet.add(2);
        numsSet.add(8);

        System.out.println(numsSet);
    }

}
```

```
// 실행 결과
[1, 2, 4, 7, 8]
```

#### LinkedHashSet

LinkedHashSet은 삽입 순서를 유지하며 중복된 요소를 허용하지 않습니다.

```java
import java.util.LinkedHashSet;
import java.util.Set;

public class Main {
    public static void main(String[] args) {
        Set<String> colorsSet = new LinkedHashSet<>();

        colorsSet.add("빨강");
        colorsSet.add("초록");
        colorsSet.add("파랑");
        colorsSet.add("빨강");

        System.out.println(colorsSet);
    }

}
```

```
// 실행 결과
[빨강, 초록, 파랑]
```

### Map

Map은 키(Key)와 값(Value)을 하나의 쌍으로 저장합니다. 키는 중복 저장될 수 없고 값은 중복 저장할 수 있습니다. 다른 값을 가진 중복된 키를 저장하면 새로운 값으로 대체됩니다.

Map 인터페이스에서 제공하는 일부 메서드는 다음과 같습니다.

| 메서드                      | 설명                                                                                                      |
| --------------------------- | --------------------------------------------------------------------------------------------------------- |
| put(K key, V Value)         | 키와 값을 추가합니다. 저장되면 값을 반환합니다.                                                           |
| get(Object key)             | 지정된 키의 값을 반환합니다.                                                                              |
| containsKey(Object key)     | 지정된 키가 포함되어 있는지 확인합니다. 키가 있으면 "true"를 반환하고 그렇지 않으면 "false"를 반환합니다. |
| containsValue(Object value) | 지정된 값이 포함되어 있는지 확인합니다. 값이 있으면 "true"를 반환하고 그렇지 않으면 "false"를 반환합니다. |
| keySet()                    | 모든 키를 포함하는 Set을 반환합니다.                                                                      |
| values()                    | 모든 값을 포함하는 Collection을 반환합니다.                                                               |
| entrySet()                  | 모든 키-값 쌍을 Map.Entry 객체로 포함하는 Set을 반환합니다.                                               |
| size()                      | 키-값 쌍의 수를 반환합니다.                                                                               |
| isEmpty()                   | Map이 비어 있는지 확인합니다.                                                                             |
| clear()                     | Map의 모든 키-값 쌍을 제거합니다.                                                                         |
| remove(Object Key)          | Map에서 주어진 키와 일치하는 쌍을 제거합니다.                                                             |

Map 인터페이스를 구현하는 클래스는 HashMap, TreeMap, LinkedHashMap 등이 있습니다.

#### HashMap

HashMap은 키로 사용할 객체가 hashCode() 메서드의 리턴값이 같고 equals() 메서드가 true를 리턴하면 중복 저장을 하지 않는 특징이 있습니다.

```java
Map<K, V> map = new HashMap<K, V>();
```

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Map<String, Integer> people = new HashMap<>();

        people.put("짱구", 5);
        people.put("철수", 5);
        people.put("맹구", 5);
        people.put("짱구", 5);

        System.out.println(people.keySet());
    }
}
```

```
// 실행 결과
[철수, 짱구, 맹구]
```

#### TreeMap

TreeMap의 특징은 키가 오름차순으로 정렬됩니다.

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Map<Integer, String> people = new TreeMap<>();

        people.put(1, "짱구");
        people.put(3, "철수");
        people.put(2, "유리");

        System.out.println(people);

    }
}
```

```
// 실행 결과
{1=짱구, 2=유리, 3=철수}
```

### Comparable, Comparator

TreeSet, TreeMap은 오름차순으로 값을 정렬하는 데, 저장하는 객체가 Comparable 인터페이스를 구현하고 있어야 가능합니다.

Comparable 인터페이스는 compareTo() 메서드가 정의되어 있기 때문에 이 메서드를 재정의해야 합니다. 값을 오름차순으로 정렬하고 싶다면 비교할 객체(Person o)보다 적으면 음수를 반환하고 많으면 양수를 반환하면 됩니다. 같다면 0을 반환하면 됩니다.

```java
public class Person implements Comparable<Person> {
    public String name;
    public int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int compareTo(Person o) {
        if (age < o.age)
            return -1;
        else if(age == o.age)
            return 0;
        else
            return 1;
    }
}

import java.util.*;

public class Main {
    public static void main(String[] args) {
        Set<Person> people = new TreeSet<>();

        Person person1 = new Person("짱구", 5);
        Person person2 = new Person("마르코", 9);
        Person person3 = new Person("짱아", 1);

        people.add(person1);
        people.add(person2);
        people.add(person3);

        for (Person p: people) {
            System.out.println(p.name);
        }

    }
}
```

```
// 실행 결과
짱아
짱구
마르코
```

반대로 비교할 객체보다 적을 때 양수를 반환하고 클 때 음수를 반환하면 내림차순으로 정렬이 됩니다.

```java
public class Person implements Comparable<Person> {
    public String name;
    public int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int compareTo(Person o) {
        if (age < o.age)
            return 1;
        else if(age == o.age)
            return 0;
        else
            return -1;
    }
}

import java.util.*;

public class Main {
    public static void main(String[] args) {
        Set<Person> people = new TreeSet<>();

        Person person1 = new Person("짱구", 5);
        Person person2 = new Person("마르코", 9);
        Person person3 = new Person("짱아", 1);

        people.add(person1);
        people.add(person2);
        people.add(person3);

        for (Person p: people) {
            System.out.println(p.name);
        }

    }
}
```

```
// 실행 결과
마르코
짱구
짱아
```

객체에 Comparable을 구현하는 방법 외에 Comparator를 사용하여 외부에서 정렬 방식을 제공할 수도 있습니다.

Comparator 인터페이스는 compare() 메서드가 정의되어 있는데, 이 메서드를 재정의해서 비교 결과를 정수로 반환하면 됩니다.

```java
int compare(T o1, T o2)
```

o1이 o2보다 앞에 오려면 음수를 반환하고, 뒤에 오려면 양수를 반환하면 됩니다. o1 과 o2가 동등하다면 0을 반환하면 됩니다.

```java
public class Person {
    public String name;
    public int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

```java
import java.util.Comparator;

public class AgeComparator implements Comparator<Person> {
    @Override
    public int compare(Person o1, Person o2) {
        if(o1.age < o2.age)
            return -1;
        else if (o1.age == o2.age)
            return 0;
        else
            return 1;
    }
}
```

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Set<Person> people = new TreeSet<>(new AgeComparator());

        Person person1 = new Person("짱구", 5);
        Person person2 = new Person("마르코", 9);
        Person person3 = new Person("짱아", 1);

        people.add(person1);
        people.add(person2);
        people.add(person3);

        for (Person p: people) {
            System.out.println(p.name);
        }

    }
}
```

```
// 실행 결과
짱아
짱구
마르코
```

### List.of(), List.copyOf(), Arrays.asList()

List.of() 메서드는 자바 9에서 도입된 정적 팩터리 메서드입니다. List.of()에 의해 생성된 리스트는 크기와 요소를 수정할 수 없습니다. 또 다른 특징으로는 null을 허용하지 않습니다.

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<Integer> nums1 = List.of(1, 2, 3, 4);
        Set<Integer> nums2 = Set.of(1, 2, 3, 4);

        System.out.println(nums1);
        System.out.println(nums2);
    }
}
```

```
// 실행 결과
[1, 2, 3, 4]
[4, 1, 2, 3]
```

copyOf() 메서드는 기존 컬렉션을 복사하여 수정할 수 없는 컬렉션으로 만들 때 사용합니다. 자바 10부터 사용할 수 있습니다.

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<Integer> nums1 = new ArrayList<>();
        nums1.add(1);
        nums1.add(2);
        nums1.add(3);
        nums1.add(4);

        List<Integer> nums2 = List.copyOf(nums1);

        System.out.println(nums2);
    }
}
```

```
// 실행 결과
[1, 2, 3, 4]
```

Arrays.asList()는 배열을 List으로 변환하는 데 유용한 방법입니다. 변환된 List는 고정된 크기를 갖습니다.

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        String[] str = {"짱구", "철수", "맹구"};
        List<String> strList = Arrays.asList(str);

        System.out.println(strList);

    }
}
```

```
// 실행 결과
[짱구, 철수, 맹구]
```
