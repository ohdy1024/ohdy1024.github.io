---
layout: post
title: "[Java] 자바 시작하기"
subtitle: "자바 시작하기"
description: "OpenJDK 17 다운로드 및 설치하기"
date: 2023-06-22 13:50:00 +0900
categories: java
comments: true
---

# 자바 시작하기

## 개발 환경 설정하기 (윈도우10)

### OpenJDK 17 다운로드 및 설치하기

1.  <https://jdk.java.net/java-se-ri/17> 에서 JDK를 다운로드합니다.

2.  원하는 장소에 압출 파일을 풉니다.

3.  시작 버튼 옆 검색 창에 "시스템 환경 변수 편집"을 검색 후 클릭합니다.

4.  시스템 속성 창이 열렸다면 [환경 변수]을 클릭합니다.

5.  시스템 변수의 [새로 만들기]를 클릭하고, 나타나는 화면에서 다음과 같이 입력 후 확인 버튼을 누릅니다.

         변수 이름: JAVA_HOME
         변수 값: 다운받은 파일의 압축을 푼 OpenJDK의 경로

6.  그 다음 변수 목록에서 "Path" 변수를 찾아 [편집]을 누릅니다.

7.  편집 창이 나타나면 [새로 만들기]를 클릭한 후 "%JAVA_HOME%\bin" 입력하고 확인 버튼을 눌러 열려있던 창을 모두 닫아줍니다.

8.  명령 프롬프트를 열어 다음 명령어를 입력해 설정이 완료되었는지 확인합니다.

        $ java -version
        openjdk version "17.0.4.1" 2022-08-12 LTS
        OpenJDK Runtime Environment (build 17.0.4.1+1-LTS)
        OpenJDK 64-Bit Server VM (build 17.0.4.1+1-LTS, mixed mode, sharing)

### 자바 실행하기

1.  메모장을 열어 다음과 같이 입력 후 파일 이름을 "Hello.java"로 저장을 합니다.

        class Hello {
          public static void main(String args[]) {
            System.out.println("Hello World!");
          }
        }

2.  명령 프롬프트를 열어 작성한 파일의 경로로 이동 후 "javac Hello.java"을 입력합니다.

        파일 경로>javac Hello.java

3.  오류 없이 실행이 되었다면 파일이 있던 위치에 "Hello.class" 파일이 생성되었는지 확인합니다.

4.  파일이 생성되었다면 명령 프롬프트에 다음과 같이 입력 후 "Hello World!"가 출력되었다면 성공입니다.

        파일 경로>java Hello
