---
layout: post
title: 개인적인 개발환경 설정 방법
date: 2018-05-02 00:46:35 +0900
description: 개인적으로 사용하고 있는 툴, 개발환경 설정 순서
img: personal_env.jpeg
tags: [Tips]
---
-------------------------------------
### 이 글을 남기는 목적
SI 개발 쪽에서 일하다 보면 때때로 사용하는 단말이 바뀌는 경우가 많이 있습니다. 그 때마다 개발자마다 하루나 이틀정도 사용환경을 구성하는 경우가 있게 되는데, 매번 뭐 설치 했었는지, 어떤 설정이었는지 등 잘 기억이 안나는 경우가 많아 개인적인 기록의 목적으로 사용하는 툴이나 환경구성을 적어 놓으려 합니다.

> 생각날 때마다 조금씩 적어 나가려고 합니다.

- [D2 Coding Fonts](https://github.com/naver/d2codingfont) - NAVER 에서 만든 코딩용 폰트
Consolus에서 최근에 갈아탔습니다. Consolus보다 많이 길쭉해서 아직 어색한 감은 있지만 한글 폰트는 좋아 보이네요.
- [Cmder](http://cmder.net/) - Windows OS용 콘솔 에뮬레이터.
기본 `cmd` 콘솔이 워낙 부실하기 때문에 평소에는 **Cmder** 를 사용합니다.<br/>
**VI Editor** 도 기본 내장되어 있고 간단한 유닉스 기반 명령어들도 실행할 수 있어 매우 편리합니다.
- **Chrome Browser**
- [Vimium 크롬 확장 프로그램](https://chrome.google.com/webstore/search/vimium?utm_source=chrome-ntp-icon) - **Vim** 사용이 익숙하신 분들께는 정말 강추 합니다. 생산성 향상에 큰 도움이 되는 Must Have app.
- [SharpKeys](https://github.com/randyrants/sharpkeys) - 키 레지스트리 변경 앱입니다. 저는 일본 키보드를 쓰고 있기 때문에 한영키가 없는 문제를 이걸로 해결하고 있습니다. 그 외에도 **CapsLock** 버튼을 **Control** 로 바꿔서 사용하고 있습니다. 정말 편합니다. 대신 익숙해지면 다른 사람 단말기 쓸 때 진짜 불편해서 짜증난다는 단점이...
- [Visual Studio Code](https://code.visualstudio.com/) - Atom, SublimeText 등 여러가지 텍스트 에디터와 비교해본결과 VSCODE가 가장 좋았습니다. ATOM은 속도면에서 무거운 감이 있었고, SublimeText는 유료라는 점과 한글입력 문제 등이 있었기 때문에 결론 적으로 VSCODE에 정착하게 되었습니다. 물론 개인적인 의견입니다. 설정파일도 같이 올립니다. 몇몇 설정들은 extend 의존의 설정입니다.
```json
{
    "editor.fontSize": 20,
    "editor.renderWhitespace": "all",
    "editor.renderControlCharacters": true,
    "editor.tabSize": 2,
    "files.trimFinalNewlines": true,
    "files.trimTrailingWhitespace": true,
    "files.eol": "\n",
    "debug.inlineValues": true,
    "debug.toolBarLocation": "docked",
    "search.exclude": {
        "**/node_modules": true,
        "**/bower_components": true,
        "**/logs": true
    },
    "editor.wordWrap": "on",
    "editor.fontFamily": "D2Coding",
    "terminal.integrated.fontSize": 18,
    "breadcrumbs.enabled": true,
    "terminal.external.windowsExec": "C:\\cmder\\bin\\cmder.exe",
    "insertDateString.format": "YYYY-MM-DD hh:mm:ss ZZZZ",
}
```
키 바인딩 설정들도 같이 추가합니다.
```json
[
  {
    "key": "ctrl+c",
    "command": "-extension.vim_ctrl+c",
    "when": "editorTextFocus && vim.active && vim.overrideCtrlC && vim.use<C-c> && !inDebugRepl"
  },
  {
    "key": "ctrl+b",
    "command": "-extension.vim_ctrl+b",
    "when": "editorTextFocus && vim.active && vim.use<C-b> && !inDebugRepl && vim.mode != 'Insert'"
  },
  {
    "key": "ctrl+j",
    "command": "-extension.vim_ctrl+j",
    "when": "editorTextFocus && vim.active && vim.use<C-j> && !inDebugRepl"
  },
  {
    "key": "ctrl+w",
    "command": "-extension.vim_ctrl+w",
    "when": "editorTextFocus && vim.active && vim.use<C-w> && !inDebugRepl"
  },
  {
    "key": "ctrl+k",
    "command": "-extension.vim_ctrl+k",
    "when": "editorTextFocus && vim.active && vim.use<C-k> && !inDebugRepl"
  },
  {
    "key": "ctrl+f",
    "command": "-extension.vim_ctrl+f",
    "when": "editorTextFocus && vim.active && vim.use<C-f> && !inDebugRepl"
  },
  {
    "key": "ctrl+v",
    "command": "-extension.vim_ctrl+v",
    "when": "editorTextFocus && vim.active && vim.use<C-v> && !inDebugRepl"
  }
]
```

- [Insomnia](https://insomnia.rest/) - Rest API 테스트 클라이언트 입니다. 깔끔한 UI와 사용하기 매우 쉽기 때문에 API 테스트에서 주로 사용하고 있습니다.