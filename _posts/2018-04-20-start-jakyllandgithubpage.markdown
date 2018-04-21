---
layout: post
title: Jekyll + Github으로 블로그 시작하기-1
date: 2018-04-20 10:48:01 +0900
description: Jekyll과 Github의 조합으로 블로그 시작하기 # Add post description (optional)
img: 2018-04-20/jekyll_logo.jpg # Add image post (optional)
tags: [Jekyll, Github page, blog] # add tag
---
-----------------------------------------
# Jekyll 로컬환경에 설치하기

- 이 포스트는 bash shell에서 설치를 기준으로 하고 있습니다.
- **Windows 10 bash**에서도 동일하게 돌아가는 것을 확인했습니다. windows 10 의 bash 설치법은 이전 글을 참고해 주세요 [**Windows 10 Bash 설치하기**](/microsoft-loves-linux/)

<br/>
### Requirements
- **Ruby version 2.2.5 이상** `ruby -v`로 확인
- **RubyGems** `gem -v`로 확인
- **GCC, MAKE** `GCC -v`, `make -v`로 확인(이건 보통설치되어 있을거라 생각됩니다.)
 > 위의 요구사항이 없을 경우 `sudo apt-get install ruby-full ruby-dev` 로 설치해주세요.

<br/>
### 설치법
1. 위의 요구사항을 준비 후 `sudo gem install bundler jekyll` 로 설치합니다.  
<br/>
 만약 jekyll 설치 중 에러가 발생한다면 `nokogiri -v`로 [**nokogiri**](http://www.nokogiri.org/) 가 설치되어 있는지 확인 바랍니다. 만약 설치되어 있지 않다면 아래와 같이 설치해 주세요.
```bash
sudo apt-get install build-essential patch ruby-dev zlib1g-dev liblzma-dev
sudo gem install nokogiri
```
<br/>
1. 설치 후 `jekyll -v`로 **Jekyll**이 설치된 것을 확인합니다.
```bash
jekyll -v
```

<br/>
### [Jekyll + Github으로 블로그 시작하기-2 Jekyll에 테마 적용하기](/start-jakyllandgithubpage-2/) 바로가기