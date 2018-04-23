---
layout: post
title: Jekyll + Github으로 블로그 시작하기-3
date: 2018-04-23 23:32:38 +0900
description: Jekyll과 Github의 조합으로 블로그 시작하기- 글 포스팅하기
img: 2018-04-20/jekyll_logo.jpg # Add image post (optional)
tags: [Jekyll, Github page, blog] # add tag
---
-------------------------------------
**이전글 바로가기**
- ### [Jekyll + Github으로 블로그 시작하기-1](/start-jakyllandgithubpage/)로 바로가기
- ### [Jekyll + Github으로 블로그 시작하기-2](/start-jakyllandgithubpage-2/)로 바로가기

글을 포스팅 하는 방법은 사실 매우 단순합니다. 간단하게 얘기하면 _posts 폴더에 파일만 올리면 됩니다.

다만 jekyll엔진이 기본적으로 요구하는 몇가지 사항이 있습니다.
1. 파일명 Format은 `YEAR-MONTH-DAY-title.MARKUP`의 형식을 따를 것. (여기서 확장자 **.MARKUP**은 .md등과 같은 markup 언어를 말합니다.)
2. 파일 머리에 아래와 같이 메타 정보를 추가할 것.
```yaml
---
layout: post
title:  "Welcome to Jekyll!"
date:   2015-11-17 16:16:01 -0600
categories: jekyll update
---
```
여기서 **- - -**과 **- - -**사이는 [YAML](https://ko.wikipedia.org/wiki/YAML)로 정의됩니다.

포스트에 META정보를 정의했다면, 이제 진짜 글을 쓸 차례 입니다.
글은 기본적으로 **MARKDOWN**형식으로 작성하는 것이 가장 일반적입니다.  
[GITHUB-STYLE MARKDOWN 작성방법](https://guides.github.com/features/mastering-markdown/)

익숙하지 않으신 분들은 처음엔 약간 불편하실 수도 있겠지만 익숙해지면 **Markdown** 만큼 글쓰기 편한 문법도 없는 것 같습니다. 개발자 분들이라면 **IDE**나 기존에 사용하던 **text editor**를 사용할 수 있는 점도 큰 장점이라고 생각됩니다.

<br/>
자 그럼 이제 글을 작성했다면 올려야 겠죠.
아래와 같이 원격마스터에 `push`해 **Github Page** 에 반영해줍니다.
```bash
git add .
git commit -m "add new post"
git push origin master
```