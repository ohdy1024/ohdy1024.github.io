---
layout: post
title: "[Java] 배열"
subtitle: "배열, array"
date: 2023-07-06 13:10:00 +0900
categories: java
comments: true
---

# 배열

### 배열이란?

배열은 동일한 데이터 타입의 데이터를 연속된 공간에 저장하기 위한 자료구조입니다.

배열은 길이를 늘리거나 줄일 수 없는 특징을 가지고 있습니다.

배열이 생성되면 인덱스를 사용하여 개별 요소에 접근할 수 있습니다.

### 배열 선언

**배열 선언 방법**

```java
// 방법1
타입[] 변수;

// 방법2
타입 변수[];
```

배열 선언 방법으로 방법1을 많이 씁니다.

### 배열 초기화

배열은 `new` 키워드를 사용해서 값을 초기화 할 수 있습니다.

```java
int[] nums = new int[5]; // int 타입의 값이 들어갈 5개의 빈 공간 생성

nums[0] = 1;
nums[1] = 2;
nums[2] = 3;
nums[3] = 4;
nums[4] = 5;
```

선언과 동시에 특정 값으로 배열을 초기화할 수도 있습니다.

```java
int[] nums = new int[] { 1, 2, 3, 4, 5 };

// 또는

int[] nums = {1, 2, 3, 4, 5};
```

주의할 점은 `new`를 사용하지 않고 특정 값을 대입할 때, 배열 변수를 미리 선언한 후에는 값을 변수에 대입할 수 없습니다.

```java
int[] nums;
nums = {1, 2, 3, 4, 5}; // 에러 발생
```

메서드의 매개변수가 배열 타입일 경우에도 주의해야 합니다.

```java
public int sum(int[] nums) {
  int result = 0;

  for (int i = 0; i < nums.length; i++) {
    result += nums[i];
  }

  return result;
}

int result = sum({1, 2, 3}); // 에러 발생

int result = sum(new int[]{1, 2, 3}); // result = 6;
```

배열의 변수는 참조 변수이기 때문에 null로 초기화할 수 있습니다.

```java
int[] nums = null;
```

배열의 길이는 length를 사용해서 구하면 됩니다.

```java
int[] nums = {1, 2, 3};

System.out.println(nums.length); // 3
```

### 배열 출력(Arrays.toString())

`System.out.print()` 메서드를 사용하여 배열의 값을 출력하면 이상한 값이 나옵니다. 배열의 변수는 참조 변수이기 때문에 메모리 주소값이 출력됩니다.

```java
int[] nums = {1, 2, 3};

System.out.print(nums); // [I@24d46ca6
```

주소값이 아닌 사람이 읽을 수 있는 문자열로 확인하려면 `Arrays.toStirng()`을 사용하면 됩니다.

```java
int[] nums = {1, 2, 3};

System.out.print(Arrays.toString(nums)); // [1, 2, 3]
```

### 오름차순 정렬(Arrays.sort())

`Arrays.sort()`를 사용하면 배열의 요소를 오름차순으로 정렬합니다.

```java
int[] nums = { 1, 3, 2, 5, 4 };

Arrays.sort(nums);

System.out.print(Arrays.toString(nums)); // [1, 2, 3, 4, 5]
```

### 배열 복사(Arrays.copyOf())

`Arrays.copyOf(복사할 배열, 복사할 길이)`은 지정된 길이로 새 배열을 만들고 원래 배열의 요소를 새 배열로 복사합니다.

```java
int[] nums1 = {1, 2, 3};

int[] nums2 = Arrays.copyOf(nums1, 2);

int[] nums3 = Arrays.copyOf(nums1, nums1.length);

System.out.println(Arrays.toString(nums2)); // [1, 2]
System.out.println(Arrays.toString(nums3)); // [1, 2, 3]
```

### 배열 비교(Arrays.equals())

`Arrays.equals()`는 요소별로 두 배열이 같은지 비교합니다.

```java
int[] nums1 = {1, 2, 3};
int[] nums2 = {1, 2, 3};

System.out.println(Arrays.equals(nums1, nums2)); // true
System.out.println(nums1 == nums2) // false
```

배열이 가지고 있는 요소의 값을 비교하기 위해서는 `Arrays.equals()`을 사용하고, `==`은 배열이 참조하는 객체가 같은 객체인지 확인하기 위해 사용됩니다.

### 향상된 for 문

자바는 배열 및 컬렉션을 좀 더 쉽게 처리하기 위해 향상된 for문을 제공합니다.

사용이 간편하고 가독성이 좋으며, 배열의 인덱션 문제를 해결할 수 있는 장점이 있습니다. 단점으로는 배열의 인덱션 문제는 해결이 가능하지만, 인덱스를 사용하지 못합니다.

```java
for(타입 변수: 배열) {
  실행문
}
```

```java
int[] nums = { 1, 2, 3, 4, 5 };
int sum = 0;

for (int num : nums) {
  sum += num;
}

System.out.print(sum); // 15
```

### 다차원 배열

배열은 또 다른 배열을 대입할 수 있습니다. 이러한 배열을 다차원 배열이라고 부릅니다.

```java
변수[1차원][2차원]...[N차원인덱스]
```

**2차원 배열 생성**

```java
int[][] nums1 = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };

// 또는

int[][] nums2 = new int[][]{ { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };

```
