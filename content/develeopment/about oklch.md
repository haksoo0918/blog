---
title: 새로운 색상 모델인 OKLCH 알아보기
date: "2025-06-10"
tags: ["oklch", "color", "css", "rgb"]
description: 새로운 색상 모델인 OKLCH 설명 및 활용 방법
---

개인적으로 제일 많이 사용하는 컬러값은 해시값인거 같다. rgb시스템이나 hsl을 굳이 사용할 이유가 없었다.

CSS가 계속 발전하면서 hsl이나 rbg도 활용도가 예전에 비하면 높아졌으나, 새롭게 추가된 oklch는 대세가 될 정도로 활용도가 높은거 같아 정리해 보고 사용하려 한다.

## oklch란?

oklch는 새로운 색상 모델로, 색상을 표현하는 데 있어 더 직관적이고 사용하기 쉬운 방법을 제공한다. oklch는 밝기(Lightness), 채도(Chroma), 색상(Hue)을 기반으로 하며, 인간의 시각적 인지에 더 잘 맞춰져 있다. 특히 밝기값이 인간의 시각과 일치하도록 설계되어 있어서, 같은 밝기값을 가진 다른 색상들은 실제로도 같은 밝기로 보인다.

## oklch의 사용 방법

기본적인 사용 방법은 다음과 같다.

```css
.element {
  /* oklch(lightness-밝기 chroma-채도 hue-색상) */
  color: oklch(0.5 0.2 120deg);
  /* alpha값 사용 : oklch(l c h / alpha) */
  background-color: oklch(0.5 0.2 120deg / 0.8);
}
```

lightness는 0에서 1 사이의 값으로, 색상의 밝기를 나타낸다. 0은 검은색, 1은 흰색에 가깝다.
chroma는 0에서 약 0.37 사이의 값으로, 색상의 채도를 나타낸다. 0은 무채색(회색)이며, 값이 클수록 더 선명한 색상이 된다.
hue는 색상을 나타내며, 0에서 360도 사이의 값을 가진다.

이렇게만 보면 사용하기 더 어려워 보이기도 한다.
익숙하지 않아서 그런것도 있겠지만, 사용해 보면 코드값만으로도 직관적으로 이해할 수 있고 활용도가 높다.

간단히 설명하면, hue값만 변경해서 채도와 밝기를 유지하면서 색상을 변경할 수 있고, lightness값만 변경해서 색상을 유지하면서 밝기만 조절할 수 있다.

```css
.btn {
  --bg: oklch(0.5 0.2 120deg);
  background-color: var(--bg);

  &:hover {
    --bg: oklch(0.6 0.2 120deg); /* 밝기만 높이기 */
    background-color: var(--bg);
  }
}
```

이런식으로 활용하면 색상 팔레트나 테마를 쉽게 관리할 수 있다.

## 추가적으로

P3 색 영역은 기존 sRGB보다 약 50% 더 넓은 색 영역을 지원한다. OKLCH를 사용하면 P3 색 영역의 색상도 자연스럽게 활용할 수 있으며, 브라우저가 지원하지 않는 경우 자동으로 가장 가까운 색상으로 대체된다.

```css
/* P3 색상 활용 예시 */
.vivid-color {
  background-color: oklch(0.5 0.32 120deg); /* P3 색영역의 선명한 색상 */
}
```

## 간단 예제

가벼운 예제로 oklch를 활용해서 간단하게 버튼하나 만들었다. 기본 버튼 모습과 클릭했을때를 구현했다.

<iframe
  width="100%"
  height="300"
  title="use oklch color"
  src="https://codepen.io/haksoo/embed/OPVxgWe?default-tab=result"
  loading="lazy"
  allowtransparency="true"
  allowFullScreen
></iframe>
See the Pen <a href="https://codepen.io/haksoo/pen/OPVxgWe">use oklch color</a> by haksoo yi (
<a href="https://codepen.io/haksoo">@haksoo</a>) on <a href="https://codepen.io">CodePen</a>.

실무에서 가능하면 사용하고 싶긴 한데... 디자이너가 과연...

## 참조

- [왜 우리는 RGB와 HSL에서 OKLCH로 전환했을까요?](https://siosio3103.medium.com/%EC%99%9C-%EC%9A%B0%EB%A6%AC%EB%8A%94-rgb%EC%99%80-hsl%EC%97%90%EC%84%9C-oklch%EB%A1%9C-%EC%A0%84%ED%99%98%ED%96%88%EC%9D%84%EA%B9%8C%EC%9A%94-329816984db5)
