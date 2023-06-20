---
layout: post
title: "[Spring Boot] Spring Boot 시작하기"
subtitle: "개요"
date: 2023-06-21 01:45:00 +0900
categories: spring
tag: boot
comments: true
---

# Spring Boot

## Spring Boot를 사용하는 이유

스프링 부트는 스프링 프레임워크에 비해 설정이 간단하며 서버를 내장하고 있어 애플리케이션을 독립적으로 사용할 수 있고 외부 서버에 배포할 필요가 없습니다.

## Spring Boot 시작하기

### 1. 자바 설치 확인하기

터미널을 열고 다음 명령어를 실행해서 Java가 설치되어 있는지 확인합니다.

```
$ java -version
openjdk version "17.0.4.1" 2022-08-12 LTS
OpenJDK Runtime Environment (build 17.0.4.1+1-LTS)
OpenJDK 64-Bit Server VM (build 17.0.4.1+1-LTS, mixed mode, sharing)
```

### 2. 스프링 프로젝트 생성

먼저 spring initializr를 이용하여 스프링 부트 프로젝트를 만듭니다.

<https://start.spring.io/>

링크에 접속해 아래와 같이 설정을 한 후 GENERATE를 누릅니다.

- Project
  - gradle - Groovy
- Language
  - Java
- Spring Boot
  - 3.1.0
- Packaging
  - Jar
- Java
  - 17
- Dependencies
  - Spring Web

GENERATE를 눌러 압축 파일이 생성되었다면 압축을 풀어줍니다.

압축을 풀었다면 vscode, intellij community와 같은 개발 환경에서 프로젝트를 열어줍니다.

### 3. Hello World 출력하기

프로젝트가 정상적으로 열렸다면 src/main/java/.../DemoApplication.java 파일을 열어 다음과 같이 수정합니다.

```java
@RestController
@SpringBootApplication
public class DemoApplication {

    @RequestMapping("/")
    String home() {
        return "Hello World!";
    }

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

}
```

위와 같이 수정하였으면 애플리케이션을 실행합니다. 실행 후 브라우저에 접속하여 url 입력창에 "http://localhost:8080" 을 입력하여 "Hello World!" 문구가 보인다면 성공입니다.

@RestController는 여기로 HTTP 요청을 처리하고 반환 데이터는 Json 형태로 반환한다는 뜻으로 생각하면 됩니다. @RequstMapping은 특정 url이나 url 패턴을 이 메서드에 매핑한다는 뜻입니다.

스프링 부트를 사용하면 이와 같이 따로 서버를 설치 및 설정하지도 않고 간단한 설정만으로 웹 애플리케이션을 만들고 실행할 수 있는 장점이 있습니다.
