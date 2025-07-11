---
layout: post
title: "[Jungle] WIL : Week-0"
author : Dev/ Paul
categories: Krafton-Jungle
tags:
  - Develop
  - Developer
  - CS
  - Computer-Science
  - Study
  - Project
  - Krafton-Jungle
  - Jungle
---

> 크래프톤 정글에서의 0주차를 마치는 Week-I-Learn

## 2025.07.09

**이모지의 글자수 처리**

- 알아보게 된 배경
    - 웹상에서 `input` 혹은 `textarea`에서 입력값에 대한 글자수를 처리해야함
    - 여기서 문제는, **이모지의 경우 이모지 하나당 적게는 2자에서 많게는 6자 이상으로 인식**이 되는 Issue가 발생
    - 이모지를 한글자로 처리할 수 없을까에 대한 방안을 모색하던 중 알게 된 내용

<br/>

- 컴퓨터에서 글자수를 처리하는 단위
    - `Bytes` : Memory 혹은 Storage상에서 Unicode String이 몇 Byte를 차지하는지 Encoding에 따라 달라짐
    - `Code Units` : Text Encoding에 있어 처리를 위한 **한 단위**를 표현할 수 있는 비트 조합
        - 1 code unit = [`UTF-8`: `1byte`], [`UTF-16` : `2bytes`], [`UTF-32` : `4bytes`]
    - `Code Points` : Unicode Character. Unicode Space 상의 한 integer 값으로 현재는 U+0000 ~ U+10FFFF 사이의 값 중 하나
    - `Grapheme Clusters` : 사용자(사람)이 인식하는 하나의 글자. `1 Grapheme Cluster` = `여러개의 Code Point`로 이루어질 수 있음

> 출처 : [Line Engineering Tech Blog](https://engineering.linecorp.com/ko/blog/the-7-ways-of-counting-characters)

<br/>

- `HTML`에서 이러한 이모지들의 글자수 처리 방법
    - **Basic Multilingual Plane(`BMP`)로 처리하기**
        - `BMP`란 : 기본 다국어 평면, `Unicode`에서 대부분의 문자 체계를 모두 집어넣은 문자 집합
        - 기본적인 그림문자(우리가 흔히 부르는 Emoji)도 일부 포함하고 있음
        - _👍 Props_
            - 간단하고, HTML의 경우 별도 라이브러리를 필요로 하지 않음
            - IE를 제외한 브라우저 호환성도 좋음
        - _👎 Cons_
            - 조합 Emoji는 제외함(👩‍👩‍👧‍👦와 같은 여러 코드포인트 + `ZWJ`)
                - `ZWJ` : Zero Width Joiner, 두 개 이상의 다른 문자를 순서대로 결합하여 새로운 Emoji를 만든 것
    - **사용자 인식 문자 즉, Grapheme Cluster로 처리하기**
        - `Intl.Segmenter`를 사용하여 하나의 문자로 처리하는 방법
        - _👍 Props_
            - 복합 이모지(`ZWJ`), 깃발 이모지 등 모든 클러스터를 1개로 처리 가능
        - _👎 Cons_
            - 최신의 브라우저를 제외하고는 지원하지 않음(IE 포함)

<br/>

HTML & JS 에서의 구현
```JS
// segmenter.js
// ──────────────────────────────────────────────────────────────────
// Intl.Segmenter 기반으로 input 제한 모듈화
// Usage: import { setupGraphemeLimiter } from './segmenter.js';

export function setupGraphemeLimiter({
  inputSelector,
  maxChars,       // === maxlength of input or textarea tag
  locale = 'ko'
}) {
  // segmenter 선언
  const segmenter = new Intl.Segmenter(locale, { granularity: 'grapheme' });
  // inputSelector로부터 쿼리 내 내용을 받아옴
  const inputs = document.querySelectorAll(inputSelector);

  // eventListener 등록 후 input의 변화에 따라 로직 수행
  inputs.forEach(input => {
    input.addEventListener('input', () => {
      // 입력값을 grapheme 단위로 쪼개 배열로 생성 => 형태는 { segment: "문자" }
      const segments = Array.from(segmenter.segment(input.value));
      // 실제 문자만 뽑아 배열로 만듦 => segment 단위로 쪼갠다는 뜻 (아래에서 자세하게 설명)
      const chars = segments.map(seg => seg.segment);
      // 만약, maxChars 보다 현재 받아온 세그먼트 전체의 개수가 많아진다면,
      if (chars.length > maxChars) {
        // 0번째부터 마지막 50번째 객체 까지만 slice, 나머지는 버림
    	input.value = chars.slice(0, maxChars).join('');
      }
    })
  })
}

// 부연 설명
// consts chars = segments.map(seg => seg.segment) 에 대한 자세한 설명
// 아래와 같이 segments의 반환 값은 {세그먼트 / 인덱스 / 워드의 형태인지} 로 반환
// 여기에서 워드가 아닐 경우는, 세그먼트의 개수에 따라가도록 설계한 것

// const segmenter = new Intl.Segmenter('ko', { granularity: 'grapheme' });
// const segments = Array.from(segmenter.segment('안녕😊하세요'));

// output
// segments = [
//   {segment: '안', index: 0, isWordLike: true},
//   {segment: '녕', index: 1, isWordLike: true},
//   {segment: '😊', index: 2, isWordLike: false},
//   {segment: '하', index: 3, isWordLike: true},
//   {segment: '세', index: 4, isWordLike: true},
//   {segment: '요', index: 5, isWordLike: true}
// ]

```

```HTML
<!-- index.html -->
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>Grapheme Limiter 데모</title>
  <style>
    body { font-family: sans-serif; padding: 20px; }
    input { padding: 8px; font-size: 1rem; width: 300px; }
    #char-counter { margin-top: 8px; color: #555; }
  </style>
</head>
<body>
  <h1>이모지 입력 제한 (grapheme 단위)</h1>
  <input type="text" class="emoji-input" placeholder="여기에 입력하세요" />
  <div id="char-counter">0/10</div>

  <!-- 모듈 스크립트 로드 -->
  <script type="module">
    import { setupGraphemeLimiter } from './segmenter.js';

    // 옵션에 따라 파라미터만 바꿔서 여러 input에 적용 가능
    setupGraphemeLimiter({
      inputSelector: '.emoji-input',
      maxChars: 10,
      locale: 'ko'
    });
  </script>
</body>
</html>

```

> [Intl에 대한 Javascript Official Document](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl)
