---
layout: post
title: "[Java] 스레드"
subtitle: "스레드, 쓰레드, thread"
date: 2023-08-09 20:43:00 +0900
categories: java
comments: true
---

# 스레드

### 스레드

스레드는 자바 프로그램 내에서 가장 작은 실행 단위입니다. 스레드는 프로그램이 여러 작업을 동시에 수행할 수 있도록 하여 동시 및 병렬 처리를 효과적으로 가능하게 합니다. 각 스레드는 일련의 명령을 실행하는 독립적인 제어 흐름을 나타냅니다.

### 메인 스레드

'메인 스레드'는 자바 프로그램이 실행되기 시작할 때 생성되는 첫 번째 스레드를 나타냅니다. 자바 프로그램이 실행되기 시작하면 JVM(Java Virtual Machine)은 메인 스레드를 생성하고 `main()` 메서드를 호출합니다.

### 스레드 생성

스레드는 `Thread` 클래스를 상속하거나 `Runnable` 인터페이스를 구현해서 생성할 수 있습니다.

#### Thread 클래스

`Thread` 클래스를 사용하여 스레드를 생성하려면 클래스를 확장하고 `run()` 메서드를 재정의합니다.

```java
public class WorkThread extends Thread {
    @Override
    public void run() {
        System.out.println("스레드 실행 중");
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Thread thread = new WorkThread();
    }
}
```

#### Runnable 인터페이스

`Runnable` 인터페이스를 사용하여 스레드를 생성하려면 먼저 인터페이스를 구현하고 `run()` 메서드를 재정의합니다. 그리고 구현한 클래스의 객체를 생성 후 객체를 `Thread`의 생성자 인수로 전달합니다.

```java
public class Task implements Runnable{
    @Override
    public void run() {
        System.out.println("스레드 실행 중");
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Runnable task = new Task();
        Thread thread = new Thread(task);
    }
}
```

`Runnable` 인터페이스는 추상 메서드가 하나인 함수형 인터페이스이기 때문에 익명 클래스와 람다식을 활용할 수 있습니다.

```java
public class Main {
    public static void main(String[] args) {
        Thread thread = new Thread(new Task() {
            @Override
            public void run() {
                System.out.println("스레드 실행 중");
            }
        });
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Runnable task = () -> System.out.println("스레드 실행 중");
        Thread thread = new Thread(task);
    }
}
```

### 스레드 실행

스레드를 실행하려면 스레드 객체의 `start()` 메서드를 호출해야 합니다. `start()` 메서드를 호출하면 새 스레드에 필요한 리소스를 할당한 후 재정의한 `run()` 메서드를 호출합니다. 주의할 점은 `start()` 메서드가 `run()` 메서드를 호출한다고 해서 `start()` 메서드 대신 `run()`를 호출하면 안됩니다. `run()` 메서드는 새 스레드를 생성하지 않고 현재 스레드에서 재정의한 함수를 실행합니다.

```java
public class Main {
    public static void main(String[] args) {
        Thread thread = new Thread(() ->
                System.out.println(Thread.currentThread().getName() + "에서 쓰레드 실행 중"));

        thread.run();
    }
}
```

```
// 실행 결과
main에서 쓰레드 실행 중
```

```java
public class Main {
    public static void main(String[] args) {
        Thread thread = new Thread(() ->
                System.out.println(Thread.currentThread().getName() + "에서 쓰레드 실행 중"));

        thread.start();
    }
}
```

```
// 실행 결과
Thread-0에서 쓰레드 실행 중
```

### 스레드 동기화

스레드 동기화는 멀티스레드 환경에서 공유 자원에 대한 안전한 접근을 보장하기 위한 메커니즘입니다. 여러 스레드가 동일한 자원을 동시에 접근하려고 할 때 발생하는 문제를 해결하기 위해 사용됩니다. 스레드 동기화는 데이터의 일관성과 무결성을 보장하며, 경쟁 조건과 데드락 같은 문제를 방지하는 데 중요한 역할을 합니다.

자바에서는 스레드 동기화를 위해 동기화 메서드와 블록을 제공합니다. 동기화 메서드는 실행하는 즉시 잠금이 일어나며, 메서드 실행이 끝나면 잠금이 풀립니다. 메서드 전체가 아닌 일부 영역을 실행할 때만 잠금이 필요하다면 동기화 블록을 사용하면 됩니다.

```java
public class Example {

    private int count;

    public synchronized void synchronizedMethod() {
        // ...
    }

    public void nonSynchronizedMethod() {
        // ...
    }

    public void synchronizedBlock() {
        synchronized (this) {
            // ...
        }
    }
}
```

### 스레드 상태

스레드 상태로는 **생성(NEW)**, **실행 대기(RUNNABLE)**, **실행(RUNNING)**, **일시 정지(BLOCKED, WAITING, TIMED WAITING)**, **종료(TERMINATED)** 가 있습니다. 현재 스레드의 상태를 알고 싶을 때는 `getState()` 메서드를 사용합니다.

**생성(NEW)** 상태는 새로 생성된 스레드가 내부 데이터 구조는 초기화되지만 `run()` 메서드가 호출되지 않은 상태입니다.

```java
public class Main {
    public static void main(String[] args) {
        Thread thread = new Thread(() -> {});

        Thread.State state = thread.getState();

        if (state == Thread.State.NEW) {
            System.out.print("NEW 상태입니다.");
        } else {
            System.out.print("NEW 상태가 아닙니다");
        }
    }
}
```

```
// 실행 결과
NEW 상태입니다.
```

**실행 대기(RUNNABLE)** 상태는 작업을 실행할 준비가 되어있는 상태입니다. 스케줄러가 실행 대기 상태인 스레드에게 CPU 시간을 할당하면 **실행(RUNNING)** 상태로 전환됩니다.

```java
public class Main {
    public static void main(String[] args) {
        Thread thread = new Thread(() -> {});

        thread.start();

        Thread.State state = thread.getState();

        if (state == Thread.State.RUNNABLE) {
            System.out.print("RUNNABLE 상태입니다.");
        } else {
            System.out.print("RUNNABLE 상태가 아닙니다");
        }
    }
}
```

```
// 실행 결과
RUNNABLE 상태입니다.
```

```java
public class Main {
    public static void main(String[] args) {
        Thread thread = new Thread(() -> {});

        thread.start();

        if (thread.isAlive()) {
            System.out.print("RUNNING 상태입니다.");
        } else {
            System.out.print("RUNNING 상태가 아닙니다");
        }
    }
}
```

```
// 실행 결과
RUNNING 상태입니다.
```

일시 정지 상태는 **BLOCKED**, **WAITING**, **TIMED WAITING** 세 가지 상태가 있습니다.

**BLOCKED** 상태는 이미 실행되고 있는 동기화 메서드 또는 동기화 블럭에 다른 스레드가 진입을 시도할 때 발생하는 상태입니다.

```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        final Object lock = new Object();

        Thread thread1 = new Thread(() -> {
            synchronized (lock) {
                try {
                    Thread.sleep(2000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        Thread thread2 = new Thread(() -> {
            synchronized (lock) {
            }
        });

        thread1.start();
        thread2.start();

        Thread.sleep(10);

        Thread.State thread2State = thread2.getState();
        System.out.print("Thread2 State: " + thread2State);

        try {
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

```
// 실행 결과
Thread2 State: BLOCKED
```

**WAITING** 상태는 일반적으로 스레드 간 특정 작업을 수행하기 위해 다른 스레드를 기다릴 때의 상태입니다. 스레드는 `Object.wait()` 또는 `Thread.join()` 메서드를 호출하여 명시적으로 **WAITING** 상태에 들어갈 수 있습니다.

**WAITING** 상태인 스레드를 **RUNNABLE** 상태로 만들려면 `notify()` 또는 `notifyAll()` 메서드를 사용하면 됩니다. `notify()` 메서드는 하나의 스레드를 **RUNNABLE** 상태로 만들고 `notifyAll()` 모든 **WAITING** 상태인 스레드를 **RUNNABLE** 상태로 만듭니다. 주의할 점은 두 메서드 모두 동기화 메서드 또는 동기화 블록 내에서만 사용할 수 있습니다.

```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        final Object lock = new Object();

        Thread thread1 = new Thread(() -> {
            synchronized (lock) {
                try {
                    lock.wait();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        Thread thread2 = new Thread(() -> {
            synchronized (lock) {
                try {
                    Thread.sleep(100);
                    lock.notify();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        thread1.start();
        thread2.start();

        Thread.sleep(50);

        Thread.State thread1State = thread1.getState();
        System.out.print("Thread1 State: " + thread1State);

        try {
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

```
// 실행 결과
Thread1 State: WAITING
```

**TIMED WAITING** 상태란 스레드가 지정된 시간 동안 대기하는 상태입니다. `Thread.sleep(long millis)` 또는 `Object.wait(long timeout)` 메서드와 같이 시간 제한 메서드를 사용할 때 자주 발생합니다.

```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        Thread thread = new Thread(() -> {
            try {
                Thread.sleep(2000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        thread.start();

        Thread.sleep(10);

        Thread.State threadState = thread.getState();
        System.out.print("Thread State: " + threadState);

        try {
            thread.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

```
// 실행 결과
Thread State: TIMED_WAITING
```

**TERMINATED** 상태는 스레드가 `run()` 메서드의 실행을 완료하고 종료되었음을 나타냅니다.

```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        Thread thread = new Thread(() -> {
            System.out.println("스레드 실행 중");
        });

        thread.start();

        try {
            thread.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        if (thread.getState() == Thread.State.TERMINATED) {
            System.out.print("스레드가 종료되었습니다.");
        } else {
            System.out.print("스레드가 아직 실행 중입니다.");
        }
    }
}
```

```
// 실행 결과
스레드 실행 중
스레드가 종료되었습니다.
```

### 스레드 안전하게 종료하는 방법

스레드를 예기치 않게 종료된다면 사용 중이던 리소스들이 불안전한 상태로 남겨져 있기 때문에 스레드를 안전하게 종료해야 합니다.

#### 플래그를 이용한 종료

스레드 내부에서 종료 여부를 판단하는 플래그를 사용해서 스레드를 안전하게 종료할 수 있습니다. 스레드의 `run()` 메서드 내에서 주기적으로 플래그를 체크하여, 스레드를 종료하도록 구현하면 됩니다.

```java
public class WorkThread extends Thread {
    private boolean isRunning = true;

    public void stopThread() {
        isRunning = false;
    }

    @Override
    public void run() {
        while (isRunning) {
            // 스레드 로직 실행
            System.out.println("스레드 실행 중");
        }
        // 리소스 정리
        System.out.println("리소스 정리");
        System.out.print("실행 종료");
    }
}
```

```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        WorkThread thread = new WorkThread();

        thread.start();

        Thread.sleep(10);

        thread.stopThread();
    }
}
```

```
// 실행 결과
...
스레드 실행 중
리소스 정리
실행 종료
```

#### interrupt() 메서드를 이용해 종료하기

`interrupt()` 메서드는 스레드가 일시 정지 상태에 있을 때 `InterruptedException` 예외를 발생시킵니다. 이것을 이용해 스레드를 정상 종료시킬 수 있습니다.

```java
public class WorkThread extends Thread {
    @Override
    public void run() {
        try {
            while (true) {
                // 스레드 로직 실행
                System.out.println("스레드 실행 중");
                Thread.sleep(100);
            }
        } catch (InterruptedException e) {
            // 리소스 정리
            System.out.println("리소스 정리");
            System.out.print("실행 종료");
        }
    }
}
```

```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        WorkThread thread = new WorkThread();

        thread.start();

        Thread.sleep(10);

        thread.interrupt();
    }
}
```

### 데몬 스레드

데몬 스레드는 주 스레드의 보조 작업을 하는 스레드입니다. 데몬 스레드의 특징으로는 주 스레드(사용자 스레드)가 종료되면 데몬 스레드도 같이 종료됩니다.

데몬 스레드를 만드는 방법은 데몬 스레드가 될 스레드에 `setDaemon(true)` 메서드를 호출하면 됩니다.

```java
import java.util.stream.Stream;

public class DemonThread extends Thread {
    @Override
    public void run() {
        Stream.of("짱구", "철수", "맹구").forEach((name) -> {
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
            System.out.println(name);
        });
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        DemonThread thread = new DemonThread();
        thread.setDaemon(true);
        thread.start();

        try {
            Thread.sleep(300);
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }
        System.out.println("메인 스레드 종료");
    }
}
```

```
// 실행 결과
짱구
철수
메인 스레드 종료
```
