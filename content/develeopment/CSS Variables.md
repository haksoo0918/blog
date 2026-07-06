---
tags:
  - css
  - variable
draft: "true"
---
- css 변수를 생각나는 대로 적어봄
- 기본과 컴포넌트 단위로 구분해서 정의

```css title="base"
:root {
	/* color */
	--white: #fff;
	--black: #000;
	
	--base-color: ;
	--point-color: ;
	--alret-color: ;
	--danger-color: ;
	--success-color: ;
	--info-color: ;
	
	--text-color: ;
	--bg-color: ;
	--link-color: ;
	
	/* amount */
	
	/* font */
	--header-font: ;
	--body-font: ;
	--code-font: ;
	--base-font-size: 1rem;
	
	/* space */
	--space-x: .4em;
	--space-y: .6em;
	
	/* break point */
	--mobile: ;
	--tablet: ;
	--desktop: ;
	
	/* border */
	--border-color: ;
	--border-width: 1px;
	--border-style: solid;
	--border-radius: .5em;
}

/* dark mode */
{
	/* ... */
}
```

## 참조

- https://picocss.com/