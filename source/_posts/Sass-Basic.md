---
title: Sass Basic
date: 2022-09-13 23:05:15
tags:
- 개발
- Sass
---
# Sass?

CSS를 사용해 웹 애플리케이션 스타일을 관리하는 것은 애플리케이션 규모가 커지고 복잡해질수록 매우 어렵다.

반면 Sass와 같은 프리프로세서(Pre-Processor, 전처리기)를 사용하면 매우 효과적으로 복잡한 애플리케이션 스타일을 관리할 수 있다.

Sass란 Syntactically Awesome Style Sheets의 준말로 CSS가 아직은 할 수 없는 다양한 기능(중첩, 함수, 믹스인, 상속 등)을 제공한다.

Sass말고도 Stylus, Less와 같은 전처리기가 존재하지만 현재 Sass가 통계상 가장 사용자가 많으면서 만족도가 높아 배웠을 때 가장 유용하다고 할 수 있다. ([설문결과](https://2021.stateofcss.com/ko-KR/technologies/#scatterplot_overview))

<hr>

## 설치

Sass를 이용하기 위해선 먼저 설치를 해야한다. [공식사이트](https://sass-lang.com/install)를 참고해 다양한 방식으로 설치가 가능하다. 나는 Node.js를 이용하고 있기에 npm을 통해 설치해 주었다.
```bash
npm install -g sass
```

## 컴파일
Sass를 설치해 이용하고자 할 때, 웹 브라우저는 Sass파일을 해석할 수 없기에 Sass파일을 CSS파일로 변경해야 한다. 이를 컴파일이라 하는데 다음과 같이 사용 가능하다.
```bash
sass input.scss output.css
```
단일 파일이 아니라 폴더 단위의 변경을 처리한다면 `:`을 이용할 수 있다.
```bash
sass src/scss:public/css
```
더 많은 옵션은 [Dart Sass CLI](https://sass-lang.com/documentation/cli/dart-sass)를 참고할 수 있다.

<hr>

## 문법
Sass파일은 사용하는 문법에 따라 `.scss`의 확장자를 가진 SCSS 구문과 `.sass`를 가진 Sass구문 2가지로 나뉜다.

### Sass 구문

Sass 구문은 중괄호, 세미콜론을 생략하고 들여쓰기 문법을 사용한다. 좀 더 간결하고 작성하기 편리하며 `{}`나 `;`를 사용하지 않아도 되어 코드가 깔끔하다.

```sass
.button
	cursor: pointer
	&:disabled
		cursor: not-allowed
```

### SCSS 구문

SCSS 구문은 CSS와 유사한 문법을 사용한다. 인라인 코드를 작성할 수 있고, CSS와 유사한 문법을 가지기 때문에 코드 통합이 훨씬 쉽다.

```scss
.button {
	cursor: pointer;
	&:disabled {
	  cursor: not-allowed;
	}
}
```

서로 장단점이 있기 때문에 회사나 팀에서 원하는 방식 혹은 개인의 취향에 따라서 선택할 수 있다. 일반적으로 CSS 구문과 문제없이 호환되는 SCSS구문이 많이 사용된다.

<hr>

## Sass Basics
수업을 들으면서 Sass의 두 가지 구문중 SCSS를 사용했기에 Sass Basics에 대해 SCSS를 이용한 방법으로 정리하겠다.

### 변수(Variables)
CSS도 변수 사용이 가능하지만 Sass에서는 `$`를 이용해 더 쉽게 변수를 사용할 수 있다.

**CSS 변수**

```css
:root {
  --spacing-1: 4px;
  --spacing-2: 8px;
  --primary-400: hsl(250, 75%, 60%);
  --primary-500: hsl(250, 75%, 50%);
}

.container {
  margin-top: var(--spacing-2);
  color: var(--primary-500);
}
```

**SCSS 변수**

```scss
$spacing-1: 4px;
$spacing-2: 8px;
$primary-400: hsl(250, 75%, 60%);
$primary-500: hsl(250, 75%, 50%);

.container {
  margin-top: $spacing-2;
  color: $primary-500;
}
```

### 중첩(Nesting)
CSS는 HTML과 달리 시각적인 계층 구조와 명확히 중첩된 구문을 작성할 수 없다. 하지만 Sass는 HTML과 동일하게 시각적 계층 구조를 따르는 방식으로 스타일을 작성하는 방법을 지원한다.

**CSS 구문**

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

**SCSS 구문**

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

Sass 중첩 구문은 시각적으로 계층 구조를 파악할 수 있어 CSS 보다 직관성이 높다. 하지만 많은 중첩은 오히려 복잡성을 증가시켜 가독성이 떨어지므로 피해야한다.

### 모듈(modules)

모듈은 독립적으로 묶인 작은 코드 조각으로, Sass는 관심사에 따라 여러 조각의 코드로 묶인 파일을 관리할 수 있는 기능인 모듈화를 제공한다. 모듈은 애플리케이션 스타일을 유지 관리하기 쉽게 만들어 주는 매우 효과적인 방법이다.

Sass(정확히는 Dart Sass)에서는 `@import rule`대신 `@use`를 이용해 다른 스타일 모듈을 불러올 수 있다. Sass 파일 확장자와 언더스코어(_)는 생략 가능하다.

**_base.scss**
```scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```
불러온 모듈은 기본적으로 파일 이름을 네임스페이스(namespace)로 가지며 점(.) 문법을 사용해 모듈의 변수 등에 접근할 수 있다.

**styles.scss**

```scss
@use 'base';

.inverse {
  background-color: base.$primary-color;
  color: white;
}
```
네임스페이스 이름을 다른 이름으로 변경해 사용하고자 할 경우 as를 사용한다. 특히 as에 별(*) 기호를 사용할 경우 네임스페이스 없이 바로 모듈에서 내보낸 변수를 사용할 수 있다.

```scss
@use 'base' as *;

.inverse {
  background-color: $primary-color;
  color: white;
}
```


**CSS**

```css
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}

.inverse {
  background-color: #333;
  color: white;
}
```

### 믹스인(mixins)

CSS는 코드를 재사용 할 수 있는 기능이 제공되지 않기 때문에 코드 중복이 잦은 언어이다. 하지만 Sass는 코드를 효율적으로 재사용할 수 있도록 믹스인 기능을 제공한다. 믹스인을 이용해 재사용할 코드 그룹을  선언할 수 있다.

**SCSS**
```scss
@mixin theme($theme: DarkGray) {
  background: $theme;
  box-shadow: 0 0 1px rgba($theme, .25);
  color: #fff;
}

.info {
  @include theme;
}
.alert {
  @include theme($theme: DarkRed);
}
.success {
  @include theme($theme: DarkGreen);
}
```

**CSS**

```css
.info {
  background: DarkGray;
  box-shadow: 0 0 1px rgba(169, 169, 169, 0.25);
  color: #fff;
}

.alert {
  background: DarkRed;
  box-shadow: 0 0 1px rgba(139, 0, 0, 0.25);
  color: #fff;
}

.success {
  background: DarkGreen;
  box-shadow: 0 0 1px rgba(0, 100, 0, 0.25);
  color: #fff;
}
```
`@mixin`과 이름을 통해 믹스인을 만들 수 있다. 믹스인을 만든 후에는 `@include`와 이름을 선언해 믹스인을 이용 할 수 있다. 또한 믹스인은 JavaScript 함수처럼 매개변수를 설정할 수 있는데, 매개변수를 사용하면 믹스인 외부에서 사용자가 전달한 값을 믹스인 내부에서 사용해 재사용성을 더 높여줄 수 있다.

### 확장/상속 (extend/inheritance)

선택자 이름 앞에 `%`를 사용해 선언한 플레이스홀더 클래스는 스타일을 확장할 때만 사용되는 특수한 유형의 클래스로 여러 선택자에서 공유할 수 있다. 스타일 집합을 공유할 때는 `@extend`를 사용한다.

이 방법은 스타일 코드를 반복 생성하는 믹스인과 달리, 스타일 코드 집합 하나를 재사용하는데 목적을 두고 있어 보다 코드를 깨끗하게 유지하는데 도움이 될 수 있다.

**SCSS**
```scss
%message-shared {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.message {
  @extend %message-shared;
}

.success {
  @extend %message-shared;
  border-color: green;
}

.error {
  @extend %message-shared;
  border-color: red;
}

.warning {
  @extend %message-shared;
  border-color: yellow;
}
```

**CSS**

```css
.message, .success, .error, .warning {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  border-color: green;
}

.error {
  border-color: red;
}

.warning {
  border-color: yellow;
}
```

### 연산자 (operators)

CSS에서 수학은 매우 유용하다. Sass는 산술연산자(`+`, `-`, `*`, `%`) 및 수학 함수(예: `math.div()`)를 제공한다.

**SCSS**
```scss
@use "sass:math";

.container {
  display: flex;
}

article[role="main"] {
  width: math.div(600px, 960px) * 100%;
}

aside[role="complementary"] {
  width: math.div(300px, 960px) * 100%;
  margin-left: auto;
}
```

**CSS**

```css
.container {
  display: flex;
}

article[role="main"] {
  width: 62.5%;
}

aside[role="complementary"] {
  width: 31.25%;
  margin-left: auto;
}
```
특히 `math.div()`를 이용하기 위해서는 `@use "sass:math"`를 이용해 Sass에서 기본으로 제공하는 math 모듈을 불러와야 한다. 이때 as *를 이용해 사용한다면 div 태그와 구분이 가지 않으므로 `math.div()`의 기본 형태로 사용하는 것이 추천된다.

<hr>

# 참고
- https://sass-lang.com/guide
- https://euid.notion.site/euid/Sass-04a97ad611cc4436a9f09e9ff052b183
- https://heropy.blog/2018/01/31/sass/
