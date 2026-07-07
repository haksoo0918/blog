---
title: simple background pattern
date: "2025-04-25"
tags: ["background", "pattern", "css", "gradient"]
description: css repeating gradient를 활용하여 배경 패턴 만들기
---

별다른 이유는 없다. 그냥 갑자기 만들고 싶어졌다. 그래서 만들었다.

예전에 격자무늬 만들어 놨던것을 bg1로 바꾸고 나머지를 추가했다.

<iframe
  width="100%"
  height="500"
  title="line background"
  src="https://codepen.io/haksoo/embed/AzqmXJ?default-tab=result"
  frameborder="no"
  loading="lazy"
  allowtransparency="true"
  allowFullScreen
></iframe>

```css
/* new version */
.bg2 {
  background:
    repeating-linear-gradient(#eee 0 1px, transparent 1px 20px),
    repeating-linear-gradient(90deg, #eee 0 1px, transparent 1px 20px);
}
/* stripe */
.bg3 {
  background: repeating-linear-gradient(#eee 0 10px, transparent 10px 20px);
}
/* check line */
.bg4 {
  background:
    repeating-linear-gradient(90deg, #eee 0 10px, #fff 10px 20px),
    repeating-linear-gradient(90deg, #fff 0 10px, #eee 10px 20px);
  background-size: auto 10px;
  background-position:
    0 0,
    0 10px;
  background-repeat: repeat no-repeat;
}
/* ? */
.bg5 {
  background-image: repeating-conic-gradient(#eee 1deg 2deg, transparent 2deg 10deg);
}
/* wave */
.bg6 {
  background-image: repeating-radial-gradient(#eee 0 10px, #fff 10px 20px);
  background-size: 120px 120px;
}
```

bg5의 경우는 0부터 시작하면 세로줄이 생겨서 1부터 시작했다. 마땅한 이름이 생각이 안나서 그냥 물음표로 했다.
