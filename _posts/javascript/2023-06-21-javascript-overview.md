---
layout: post
title: "[JavaScript] javascript란?"
subtitle: "개요"
date: 2023-06-21 03:15:00 +0900
categories: javascript
comments: true
---

# JavaScript

### JavaScript란 무엇인가?

자바스크립트는 웹 페이지에 생동감과 복잡한 기능을 구현할 수 있도록 하는 스크립팅 언어 또는 프로그래밍 언어입니다.

처음에는 웹 브라우저에서 클라이언트 측 스크립팅 기능을 제공하기 위해 개발되었지만 시간이 지남에 따라 브라우저뿐만 아니라 서버, 데스크탑 애플리케이션 및 모바일 앱 개발을 할 수 있게 되었습니다.

### 자바스크립트가 브라우저에서 할 수 있는 일

**자바스크립트가 브라우저에서 할 수 있는 일**

- 웹 페이지의 DOM(Document Object Model) API를 통해 HTML과 CSS를 동적으로 수정, 사용자 인터페이스를 업데이트할 수 있습니다. 이를 통해 양식 유효성 검사, 이미지 슬라이더, 드롭 다운 메뉴 등과 같은 기능을 만들 수 있습니다.
  <br>
- 마우스 클릭이나 포인터의 움직임, 키보드 키 눌림 등과 같은 이벤트를 처리할 수 있습니다. 이를 통해 웹 페이지의 특정 요소에 이벤트 핸들러를 연결하여 특정 이벤트가 발생할 때 페이지가 응답하는 방식 등을 구현할 수 있습니다.
  <br>
- 네트워크를 통해 원격 서버에 요청을 보내거나, 파일 다운로드, 업로드 등을 할 수 있습니다.
  <br>
- 로컬 스토리지 및 세션 스토리지 등을 이용하여 클라이언트 측에 데이터 저장할 수 있습니다.

### 웹 페이지에 자바스크립트 넣기

웹 페이지에 자바스크립트를 넣는 방식은 내부, 외부 방식이 있습니다.

내부 방식은 `<script>` 태그를 사용해서 HTML 파일 내 자바스크립트 코드를 직접 삽입하는 방법입니다.
HTML 문서의 `<head>` 또는 `<body>` 태그 내에 `<script>` 태그를 배치하면 됩니다.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello World</title>
    <script>
      console.log("Hello World");
    </script>
  </head>
  <body></body>
</html>
```

외부 방식은 확장자가 .js인 자바스립트 파일을 만들어. `<script>` 태그의 src 속성을 사용하여 파일을 참조하는 방식입니다.

```javascript
// hello.js
console.log("Hello Word");
```

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello World</title>
    <script src="hello.js"></script>
  </head>
  <body></body>
</html>
```

### 이벤트 처리

자바스크립트를 이용하여 이벤트를 처리하는 방법은 두 가지가 있습니다.

예시로 HTML `<button>` 요소에 클릭 이벤트가 발생했을 때 콘솔 창에 "Hello World"를 출력해보겠습니다.

**인라인으로 처리하기 (권장하지 않음)**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello World</title>
  </head>
  <body>
    <button onclick="clickBtn()">눌러</button>

    <script>
      function clickBtn() {
        console.log("Hello World");
      }
    </script>
  </body>
</html>
```

**addEventListener 사용하기**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello World</title>
  </head>
  <body>
    <button>눌러</button>

    <script>
      const buttons = document.querySelectorAll("button");

      for (const button of buttons) {
        button.addEventListener("click", clickBtn);
      }

      function clickBtn() {
        console.log("Hello World");
      }
    </script>
  </body>
</html>
```

HTML 태그 요소 안에 자바스크립트 코드를 사용하는 방법은 권장하지 않습니다. 왜냐하면 같은 기능이 필요한 버튼이 있을 때 모든 버튼마다 일일히 `onclick="clickBtn()"`를 추가해야 하는 것은 비효율적이기 때문입니다.
