---
title: IR기법 (Image Replacement)
date: 2022-09-07 22:21:22
tags:
- 개발
- CSS
- IR
---
# 👀
WCAG 2.1에 웹 콘텐츠의 접근성을 향상시키기 위해 텍스트 아닌 콘텐츠에 대해 대체 텍스트를 제공해주어야 한다는 지침이 있다. 이미지 역시 텍스트가 아닌 콘텐츠이기 때문에 대체 텍스트를 제공해주어야 하는데, 이는 접근성의 향상 뿐만 아니라 SEO(검색 엔진 최적화)와도 관련이 있어 중요하다.

이렇게 사용자에게 대체 텍스트를 제공하는 것을 IR(Image Replacement)이라고 하는데, HTML의 요소를 사용할 경우 alt 속성을 통해 대체 텍스트를 제공하는것이 일반적이다.

하지만 CSS를 이용해 background-image를 넣는 경우도 많기에 어떻게 대체 텍스트를 제공하는지 정리해보자.

<hr>

# 😒 visibility: hidden, display: none

먼저 IR기법으로 잘못 사용되고 있는 대표적인 예가 있는데 visibility: hidden과 display: none이다.

이 두 방법은 모두 적용된 요소가 화면에서 보이지 않게 하기 때문에 스크린리더 사용자를 위한 텍스트를 제공하기 위해 사용되는 경우를 발견할 수 있다. 하지만 이 두 방법은 스크린리더에서도 읽지 않는것을 원칙으로 한다.

IR기법의 목표는 대체 텍스트를 시각적으는 숨기지만 스크린 리더 사용자는 읽을 수 있어야 하기 때문에 이 두가지 방법은 옳지 않다.

<hr>

# 😊 올바른 IR 기법

## Phark Method
- 가장 널리 사용되는 방법으로 이미지로 대체할 엘리먼트에 배경이미지를 설정하고 글자는 text-indent를 이용하여 화면 바깥으로 빼내어 보이지 않게 하는 방법이다.

- 의미있는 이미지의 대체 텍스트를 제공하는 경우에 사용한다.

- Text-indent 속성은 사용하기 간편하지만 단점 또한 존재한다. 만약 이미지가 제대로 로드되지 않으면 텍스트가 보이지 않기 때문에 스크린리더 사용자가 아닌 경우 이미지를 설명하는 텍스트를 보고 콘텐츠의 내용을 확인 할 수 없다. 또한, 웹페이지에 text-indent 스타일 속성이 적용된 요소가 많으면 성능 저하를 불러올 수 있다.

``` css
.ir_pm{
width: 995px;
height: 1441px;
text-indent: -9999px;
background : url("rocketgril_poster.jpg") no-repeat;
}
```

## Dwyer Method
- 이미지로 대체할 엘리먼트에 배경이미지를 설정하고 글자는 span태그로 감싼 후 width와 height를 각각 0으로 하여 넘치는 글자를 숨기는 방법이다.

- 추가적인 tag를 사용하고, Phark Method와 마찬가지로 이미지가 제대로 로드되지 않으면 텍스트가 보이지 않아 콘텐츠 내용 확인이 어렵다는 단점이 존재한다.

``` css
.ir_dm{
width: 995px;
height: 1441px;
background : url("rocketgril_poster.jpg") no-repeat;
}

.ir_dm span{
display :block;
overflow: hidden;
width: 0px;
height: 0px;
}
```

## WA IR
- 접근성 및 UX(User Experience) 향상을 위한 화면읽기프로그램 활용 기법으로 권장되는 방법이다.

- 의미있는 이미지의 대체 텍스트로 이미지가 없어도 대체 텍스트를 보여주고자 할 때 사용한다.

- 이미지로 대체할 엘리먼트에 배경이미지를 설정하고 글자는 span 태그로 감싼 후 z-index:-1을 이용하여 배치순서를 뒤로 보내어 화면에 안보이게 처리한다.

- 만약 브라우저에서 CSS를 끄거나, 웹 페이지에 적용된 CSS가 정상적으로 로드되지 않을 때 숨겨진 텍스트가 화면에 출력된다. 또한, position 속성을 사용하기 때문에 성능에 영향을 줄 수 있다.
``` css
.ir_wa{
width: 995px;
height: 1441px;
background : url("rockegril_poster.jpg") no-repeat;
}

.ir_wa span{
display:block;
position:relative;
z-index:-1;
}
```

이 외에도 CSS의 위치 속성과 overflow: hidden을 사용하는 방법, 자바스크립트를 이용하여 이미지로 대체할 엘리먼트의 텍스트를 img태그로 교체하는 방법등 다양한 방법이 존재한다.

<hr>

# 참고
- https://m.blog.naver.com/eirene100999/221686480420
- https://nuli.navercorp.com/community/article/1132804?email=true
- https://alonehistory.tistory.com/14
