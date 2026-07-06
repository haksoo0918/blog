---
tags:
  - vscode
  - shortcut
  - 단축키
---

적어두면 언젠가 찾아 볼 듯

```json title="keybindings.json"
[
  {
    "key": "ctrl+oem_1",
    "command": "cursorEnd",
    "when": "textInputFocus",
  },
  {
    "key": "ctrl+alt+t",
    "command": "editor.action.insertSnippet",
    "when": "editorTextFocus",
    "args": {
      "snippet": "${CURRENT_YEAR}-${CURRENT_MONTH}-${CURRENT_DATE} ${CURRENT_HOUR}:${CURRENT_MINUTE} ",
    },
  },
]
```

- 첫번째 꺼는 'ctrl + ;' 키를 누르면 그 줄의 맨 끝으로 간다.
- 두번째 꺼는 'ctrl + alt + t'를 누르면 날짜와 시간이 입력된다.