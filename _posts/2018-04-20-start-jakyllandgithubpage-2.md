---
layout: post
title: Jekyll + Github으로 블로그 시작하기-2
date: 2018-04-20 23:54:08 +0900
description: Jekyll과 Github의 조합으로 블로그 시작하기- Jekyll에 테마 적용하기
img: 2018-04-20/jekyll_logo.jpg # Add image post (optional)
tags: [Jekyll, Github page, blog] # add tag
---
-------------------------------------
- 이전글
### [Jekyll + Github으로 블로그 시작하기-1](/start-jakyllandgithubpage/)로 바로가기
- 다음글
### [Jekyll + Github으로 블로그 시작하기-3 새 글 포스팅하기](/start-jakyllandgithubpage/)로 바로가기

<br/>
# local환경과 github page에 테마 적용하기 

1. **Github에 블로그 deploy용 repository생성하기**<br/>
<br/>
Repository Name 작성시 [사용자아이디].github.io형식으로 작성해주어야합니다.
<br/>
![Alt text](/assets/img/2018-04-20/01-git-repo.png)

1. **repository를 만든 후 로컬환경에 블로그를 관리 할 폴더를 만든 후 그곳에 아래와 같이 클론합니다.**  
<br/>
```bash
git clone -u origin [1.에서 만든 repository url ]
```  
<br/>
2. **테마를 다운받아 설치하기**   
<br/>
이제 설치할 테마를 찾아보겠습니다. http://jekyllthemes.org/ 여기서 마음에 드는 테마를 찾아서 다운로드 후 (1)에서 클론한 폴더에 압축을 풀어 줍니다.<br/>
<br/>
![Alt text](/assets/img/2018-04-20/02-git-forder.png)  
<br/>
위와 같은 폴더구성을 확인 하였다면 이제 로컬에서 블로그를 돌려보겠습니다.
터미널에서 해당 폴더로 이동 후 `bundle`을 실행해서 *.gem*파일에 명시되어 있는 gem들을 설치해줍니다. 그 후 `jekyll -s`으로 jekyll 서버를 실행합니다.  
<br/>
```bash
bundle
jekyll -s
```
<br/>
서버가 실행되었습니다. **localhost:4000**에서 돌아가고 있네요.
<br/>
![Alt text](/assets/img/2018-04-20/03-run-server.png)    
<br/>
> *저는 이미 글을 좀 올린 상태입니다. 여러분들은 초기화면이 표시될 꺼에요.*
<br/>
<br/>
1. **Github에 내 블로그 올리기**  
<br/>
로컬에서 돌아가는 걸 확인했다면 이번에는 **Github**에 올려서 확인해 보겠습니다. 터미널에서 아래와 같이 `push`해 주세요.  
<br/>
```bash
git add .
git commit -m "initial commit"
git push origin master
```
<br/>
`push`후에 브라우저를 통해 github에 내 블로그로 접속합니다. 접속주소는 `자기 아이디.github.io`입니다.  
> 서버상태에 따라 deploy되는데 시간이 걸릴 수 있습니다. 저는 길어도 5분정도 이상은 안걸리더라구요.

<br/>
다음에는 글 포스팅 하는 법을 중점으로 올려보도록 하겠습니다.