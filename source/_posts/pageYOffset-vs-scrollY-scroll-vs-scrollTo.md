---
title: pageYOffset vs scrollY, scroll() vs scrollTo()
date: 2022-11-28 12:31:26
tags:
- JS
---
# 🤔What is Problem?

페어 프로그래밍을 진행하면서 수직으로 스크롤한 거리에 따라 숨겨진 버튼을 활성화 하고, 스크롤 버튼을 클릭했을 때 맨 위로 스크롤하는 예제를 해결해야했다.

이를 위해 수직으로 스크롤한 거리를 측정하는 방법과 스크롤을 시키는 방법이 필요해 이에 대해 알아보았는데, 같은 기능을 하는 프로퍼티와 메서드가 중복으로 존재해 어떤것을 사용해야하는지 고민이 되었다.

## Window.pageYOffset vs Window.scrollY

먼저 수직으로 스크롤한 거리를 측정하는 방법에는 Window.pageYOffset와 Window.scrollY가 존재했다. MDN에서는 pageYOffset이 scrollY의 다른이름이라고 했지만, 두 프로퍼티에는 브라우저 호환성의 차이가 존재했다.

일부 오래된 브라우저는 scrollY 대신 pageYOffset만 지원했고 노후 환경을 신경쓰지 않아도 된다면 둘 중 아무거나 사용해도 괜찮지만, 별다른 요구조건이 없다면 하위호환성을 위해 pageYOffset을 사용하는 것이 더 좋은 코드라고 판단했다.

## Window.scroll() vs Window.scrollTo()

다음으로 맨 위로 스크롤하기 위해서는 Window.scroll() 이나 Window.scrollTo() 메서드를 사용할 수 있었다. 이 두 메서드는 차이 없이 동일해 둘 중 아무거나 사용해도 괜찮았다. 다만 scroll 메서드가 더 먼저 나왔기 때문에 실제로 사용된 코드도 많고 혹여나 버그등이 발생해 검색을 해야한다면 검색 결과도 많아 scroll을 사용하는것이 더 좋을 것이라고 판단했다.

또 단순히 메서드의 인자로 x-좌표와 y-좌표를 주는것 이외에도 options를 통해 top, left, behavior를 줄 수 있다는 것을 알았다. 특히 behavior: smooth를 사용해 애니메이션을 따로 만들지 않더라도 부드럽게 이동할 수 있는점이 유용해 꼭 기억하자 생각했다.

## 참고

- https://developer.mozilla.org/ko/docs/Web/API/Window/pageYOffset
- https://developer.mozilla.org/ko/docs/Web/API/Window/scrollY
- https://developer.mozilla.org/en-US/docs/Web/API/Window/scroll
- https://developer.mozilla.org/en-US/docs/Web/API/Window/scrollTo
- https://stackoverflow.com/questions/1925671/javascript-window-scroll-vs-window-scrollto

