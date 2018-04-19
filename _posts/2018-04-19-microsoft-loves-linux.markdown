---
layout: post
title: 윈도우즈 10에서 드디어 bash shell을...!!
date: 2018-04-19 23:51:14 +0900
description: 윈도우에서의 bash Shell 이용후기 입니다. # Add post description (optional)
img: 2018-04-19/bash.jpg # Add image post (optional)
tags: [windows10, bash shell, linux] # add tag
---
----------------------------------
### 드디어 대통합의 시대가 열리다...!

 이번에 블로그를 이전하면서 [Jekyll](https://jekyllrb.com/)을 설치하려고 했더니 평소 VM에서 돌리던 리눅스가 상태가 좋지 않았습니다. 겸사겸사 그 동안 한번 써봐야지 했었던 **Bash on Windows10**을 직접 사용해봤습니다.

 > 일단 감동적입니다....!

 [2016 Microsoft Build](https://channel9.msdn.com/Events/Build/2016)는 제가 느꼈던 MS의 build중에 가장 뜨거웠던 것 같습니다. 저도 windows10의 발표와 함께 홀로렌즈 등과 함께 굴직굴직한 뉴스들이 많아 매우 흥분했었던 기억이 나네요.

 > *개인적으로 우리 [나델라](https://en.wikipedia.org/wiki/Satya_Nadella)형이 수장이 되면서 MS가 점점 마음에 든다는...*

 ![Alt text](/assets/img/2018-04-19/Satya_Nadella.jpg)

 그런데 이상하게도 2년이나 지났는데 bash 를 윈도우에서 사용하는 개발자나 인터넷 후기들을 찾기가 힘든 것 같습니다. 여전히 대부분의 개발자들이 리눅스나 맥을 이용하고 있다고 생각되네요.

 > *아마도 아직까지는 베타버전이기에 무언가 호환성같은 문제가 있는걸까요?*

 아무튼 일단 설치 ㄱㄱ

## 환경구성순서
---------------
1. 먼저 **설정** - **시스템** 으로 들어가서 윈도우 버전을 확인합니다.
 ![Alt text](/assets/img/2018-04-19/01-check-version.png)
  **1607이하**의 윈도우를 사용하고 계신분들은 윈도우즈 업데이트가 필요합니다.



1. **설정** - **업데이트 및 복구** - **개발자용** 에서 **개발자 모드**를 켭니다.
 ![Alt text](/assets/img/2018-04-19/02-activate-dev.png)

1. 설정에서 **windows 기능** 으로 검색 - **Linux용 Windows 하위 시스템(베타)** 를 **체크**합니다.
 ![Alt text](/assets/img/2018-04-19/03-activate-linux.png)    
  체크 후 **확인** - **재시작**


1. 재시작 후 콘솔에서 `bash`를 입력하면 리눅스가 설치되기 시작합니다.
 ![Alt text](/assets/img/2018-04-19/04-install-linux.png)  
 중간에 로켈설정 확인이 나오는데 저는 그냥 ko-KR로 했습니다. 사용할 유저명과 암호를 입력하면 설치가 완료됩니다. *윈도우에서 bash shell을 보니 뭔가 기분이 이상합니다...ㅋ*

> 리눅스 버전을 확인해 보았습니다. **우분투 16 LTS**가 설치되었네요..!  
 
 ![Alt text](/assets/img/2018-04-19/07-linux-version.png)  
 
> GIT도 미리 설치되어있는 것을 확인했습니다.  
 
 ![Alt text](/assets/img/2018-04-19/08-git-version.png)

## 후기
--------
 일단 저는 아직까지는 나쁜점을 발견하지 못했습니다. 실제로 이 블로그를 돌리고 있는 **Jekyll**로 **윈도우 & bash**로 돌리고 있는거니깐요. **ruby**환경도 충분이 잘 돌아가고 있는 것 같습니다.^^ 양대 OS의 장점만을 살려서 사용할 수 있을 것 같아 매우 기대가됩니다. 앞으로 더 사용해보고 버그나 호환성 문제 등이 있을 경우 내용 업데이트 하도록 하겠습니다.

 ![Alt text](/assets/img/2018-04-19/microsoft-love-linux.jpg)
