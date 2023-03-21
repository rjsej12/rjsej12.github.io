---
title: MDN을 확신하지는 말자.
date: 2022-09-01 09:37:03
tags:
- 개발
- MDN
---
어제에 이어 position에 대해 공부하면서 position이 absolute인 경우 containing block은 가장 가까운 position이 static이 아닌 부모요소 외에도 다른 조건들이 있다고 해 MDN을 통해 공부를 하던 중 이상하다고 생각되는 점이 생겼다.
<hr>

# 👀


[컨테이닝 블록의 모든것](https://developer.mozilla.org/ko/docs/Web/CSS/Containing_block)이라는 MDN 문서에서 컨테이닝 블록 식별 항목을 읽어보면 다음과 같이 설명하고 있다. 
> position 속성이 **absolute**나 **fixed**인 경우, 다음 조건 중 하나를 만족하는 가장 가까운 조상의 내부 여백 영역이 컨테이닝 블록이 될 수도 있습니다.
 - transform이나 perspective (en-US) 속성이 none이 아님.
- will-change 속성이 transform이나 perspective임.
- filter 속성이 none임. (Firefox에선 will-change가 filter일 때도 적용)
- contain 속성이 paint임.

각 속성들이 어떤 역할을 하는지 찾아보던 중 filter 속성을 검색해 보았는데 default value가 none임을 알았다. 그러자 다음과 같은 의문이 생겼다.

# 🤔
음 이상한데? filter 속성이 none이면 containing block이 될 수 있고 filter 속성의 default value가 none이면 거의 모든것이 containing block이 될 수 있다는 소리인가? 그건 아닌것 같은데...
아 된다가 아니라 될 수도 있다네? 그러면 될 수 있는 조건과 안되는 조건은 무엇이지? 

그러다 [position] (https://developer.mozilla.org/ko/docs/Web/CSS/position) MDN을 들어가 보니 fixed 항목이 이렇게 나와 있었다.
> 요소를 일반적인 문서 흐름에서 제거하고, 페이지 레이아웃에 공간도 배정하지 않습니다. 대신 뷰포트의 초기 컨테이닝 블록을 기준으로 삼아 배치합니다. 단, 요소의 조상 중 하나가 transform, perspective, filter 속성 중 어느 하나라도 none이 아니라면 (CSS Transforms 명세 참조) 뷰포트 대신 그 조상을 컨테이닝 블록으로 삼습니다. (perspective와 filter의 경우 브라우저별로 결과가 다름에 유의) 최종 위치는 top, right, bottom, left 값이 지정합니다.

앗 여기에는 filter 속성이 none이 아니라고 되어있네 뭐가 맞는거지? transform이나 perspective가 none이 아니여야 했으니 filter도 none이 아닌게 맞는것 같은데.. 라며 계속 고민하다 같이 공부하시는 분들의 도움을 받아 궁금증을 해결했다.

# ✔

바로 [영문 MDN 사이트](https://developer.mozilla.org/en-US/docs/Web/CSS/Containing_block)에는 filter 속성이 none이 아니라고 나와있던것! 사이트 번역과정에서 오류가 있었던것이다. 
> - A filter value other than none or a will-change value of filter (only works on Firefox).

<hr>

MDN이 거의 공식문서 혹은 표준처럼 여겨지기는 하지만 번역문서 그리고 원문 역시도 contributor분들에 의해 쓰여지는 것이기 때문에 확신을 하지는 말고 여러 레퍼런스들을 통해 교차검증해야되겠다고 깨달았다.


