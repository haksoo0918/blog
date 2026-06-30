---
tags:
  - obsidian
  - frontmatter
  - yaml
---
읽어보고 사용하거나 기억해두고 싶은거 위주로 적어둠.

# Configuration 구성

- gray-matter 플러그인을 사용하여 구성한다.
- `quartz.config.yaml` 파일에서 기본 구성이 설정되어 있다.

## 기본 설정

`quartz.config.yaml`

```yaml
- source: github:quartz-community/note-properties
  enabled: true
  options:
    includeAll: false
    includedProperties:
      - description
      - tags
      - aliases
    excludedProperties: []
    hidePropertiesView: false
    delimiters: "---"
    language: yaml
```

# 중요 프론트매터

- `title` - 제목
- `description` - 설명
- `tags`, `tag` - 태그
- `cssclasses`, `cssclass` - CSS 클래스가 페이지 본문에 적용됨
- `socialImage`, `image` - 소셜 미디어 미리보기용으로 사용될 이미지
- `socialDescription` - 소셜 미디어 미리보기용 설명 문구
- `created`, `date` - 작성일
- `modified`, `lastmod`, `updated`, `last-modified` - 수정일
- `published`, `publishDate`, `date` - 공개일
- `publish` - 공개 여부
- `draft` - 초안 여부
- `comments` - 댓글 기능 활성화 여부
- `enableToc` - 목차(Table of Contents) 출력 여부

# 참조

- https://quartz.jzhao.xyz/plugins/frontmatter