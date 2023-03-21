---
title: 백준 Node.js 입출력법
date: 2022-08-06 17:08:05
tags:
- 개발
- JavaScript
- 코딩테스트

---

지금까지 leetcode와 프로그래머스를 통해 코딩테스트 공부를 하고 있었는데 leetcode는 영어 해석의, 프로그래머스는 적은 문제수의 단점을 가지고 있어 백준을 통해 코딩테스트 연습을 시작해보았다.

백준에서는 javascript로 코딩테스트를 준비하기 위해 node.js를 선택해야 했는데 프로그래머스에서는 함수만 작성하면 되었던 반면에 백준에서는 입출력을 직접 해주어야 했다.

백준에서 node.js로 입력을 받는 방법은 크게 두가지로 readline 모듈을 사용하는 것과 fs 모듈을 사용하는 것이다. fs 모듈의 경우 readline 모듈보다 코드가 간단하고 더 빠르다고 해 fs 모듈의 대해 찾아보았다.

<hr>

# **fs**

FileSystem의 약자인 fs 모듈은 파일 처리와 관련된 모듈이다. [BOJ 도움말](https://help.acmicpc.net/)에서는 다음과 같은 코드로 fs 모듈을 통한 입력을 소개하고 있다.

```javascript
let fs = require('fs');
let input = fs.readFileSync('/dev/stdin').toString().split(' ');
let a = parseInt(input[0]);
let b = parseInt(input[1]);
console.log(a+b);
```

하지만 위 코드를 이용할때에도 입력되는 값에 따라 에러가 발생하는 경우가 있어 다양한 방식의 입력법에 대해 정리해 보았다.

```javascript
1. 하나의 값을 입력받을 때
const fs = require('fs');
const input = fs.readFileSync("/dev/stdin").toString().trim();

2. 공백으로 구분된 한 줄의 값들을 입력받을 때
const fs = require('fs');
const input = fs.readFileSync("/dev/stdin").toString().trim().split(" ");

3. 여러 줄의 값들을 입력받을 때
const fs = require('fs');
const input = fs.readFileSync("/dev/stdin").toString().trim().split("\n");

4. 첫 번째 줄에 자연수 n을 입력받고, 그 다음줄에 공백으로 구분된 n개의 값들을 입력받을 때
const fs = require('fs');
const [n, ...arr] = fs.readFileSync("/dev/stdin").toString().trim().split(/\s/);

5. 첫 번째 줄에 자연수 n을 입력받고, 그 다음줄부터 n개의 줄에 걸쳐 한 줄에 하나의 값을 입력받을 때
const fs = require('fs');
const [n, ...arr] = fs.readFileSync("/dev/stdin").toString().trim().split("\n");

6. 하나의 값 또는 공백으로 구분된 여러 값들을 여러 줄에 걸쳐 뒤죽박죽 섞여서 입력받을 때
  ex) n 입력 - 공백으로 구분된 n개의 값 입력 - m 입력 - 여러 줄에 걸쳐 m개의 값 입력
const fs = require('fs');
const input = fs.readFileSync("/dev/stdin").toString().trim().split(/\s/);
const n = input[0];
const n_arr = input.slice(1, n+1);
const [m, ...m_arr] = input.slice(n+1);
```
최종 결과 확인을 위해선 **console.log()** 를 통해 값을 출력해주면 된다.
<hr>

## 참고

[[알고리즘] 백준 0.nodejs 입력하기](https://overcome-the-limits.tistory.com/25)
[Node.js로 백준(BOJ) 문제 풀 때 유의할 점들](https://tesseractjh.tistory.com/39)

