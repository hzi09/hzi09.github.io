---
title: "[TIL][JavaScript] 대문자, 소문자 변환"

categories:
  - TIL
tags:
  - TIL

toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL3.png){: .align-center style="width:35%;"}

# 👀Today I Learn

## 1. 대문자 → 소문자 : toLowerCase()

- JavaScript에서는 `toLowerCase()` 메서드를 사용하여 모든 문자를 소문자로 변환 가능

```jsx
const str = "Hello, World";
const lowerStr = str.toLowerCase();

console.log(lowerStr); // hello, world
```

## 2. 소문자 → 대문자 : toUpperCase()

- JavaScript에서는 `toUpperCase()` 메서드를 사용하여 모든 문자를 대문자로 변환 가능

```jsx
const str = "Hello, World";
const upperStr = str.toUpperCase();

console.log(upper); // HELLO, WORLD
```

## 관련 코딩테스트 문제

- 프로그래머스 : [대소문자 바꿔서 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/181949)

  ```jsx
  const readline = require("readline");
  const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout,
  });

  let input = [];

  rl.on("line", function (line) {
    input = [line];
  }).on("close", function () {
    str = input[0];

    let value = "";

    for (let i = 0; i < str.length; i++) {
      if (str[i] == str[i].toUpperCase()) {
        value += str[i].toLowerCase();
      } else {
        value += str[i].toUpperCase();
      }
    }
    console.log(value);
  });
  ```

  ➡️ 문제 풀이 보러가기 : [[Programmers][JavaScript] 대소문자 바꿔서 출력하기](https://hzi09.github.io/javascript_programmers/pg_js_181949)

<br>

# 🎯 Today’s Goals

- [x] JavaScript 코드카타 1문제
- [x] TIL 작성

<br>

# 💡Today I Thought

- 오랜만에 자바스크립트 코딩테스트 문제 풀이~
  - 자바스크립트는 isUpper 같은게 없는 모양이다.. 조금 어려운..
  - 조건문도, 반복문도 처음 코딩테스트에 써보는 거라 조금 더 감 잡는 시간이 필요할 것 같다.
