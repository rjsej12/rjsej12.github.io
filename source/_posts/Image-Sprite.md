---
title: 이미지 스프라이트(Image Sprite)
date: 2022-09-08 23:25:20
tags:
- 개발
- CSS
---
이미지 스프라이트란 여러 개의 이미지를 하나로 합쳐서 관리하는 이미지를 의미한다.

웹 페이지에 이미지를 사용한다면 웹 브라우저는 해당 이미지의 다운로드를 위해 서버에 요청을 보낸다. 만약 사용된 이미지가 많을 경우 요청 하는 횟수가 많아지므로 웹 페이지의 로딩 시간이 오래 걸리게 된다. 하지만 만약 이미지 스프라이트를 사용한다면 스프라이트 이미지 파일 하나가 여러 이미지를 가지고 있기에 서버 요청 횟수를 줄일 수 있다.

개인적인 블로그와 같은 일반적인 사이트에서는 굳이 이미지 스프라이트를 사용 할 필요가 없지만, 트래픽이 매우 많거나 많은 사람이 이용하는 검색포털과 같은 사이트에서는 이미지 스프라이트를 사용하여 서버 요청을 줄이고 웹 페이지의 로딩 시간을 단축시켜 사이트의 품질을 높일 수 있다.

다음은 네이버 메인페이지의 스프라이트 이미지이다.
![](https://velog.velcdn.com/images/rjsej12/post/34bfd37f-ea3a-4073-8a76-7c5cfbf8b1fc/image.png)

이처럼 여러개의 이미지를 하나로 합쳐두고 CSS의 `background-position`을 이용해 사용하려는 이미지만을 보여 줄 수 있다. 이 때 `background-position`의 값은 하나씩 position값을 변경해보며 찾을 수 도 있지만 [Sprite Cow](http://www.spritecow.com/)와 같은 사이트를 이용 할 수 있다.

추가적으로 스프라이트 이미지를 만들기 위해 포토샵, 피그마 등으로 에디팅 할 수 도 있지만 [CSS Sprites Generator](https://www.toptal.com/developers/css/sprite-generator/)라는 사이트를 이용 가능하다.

<hr>

# 참고
- https://creativestudio.kr/1653
- http://www.tcpschool.com/css/css_basic_imageSprites
