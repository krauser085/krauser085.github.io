---
layout: post
title: 개인정보 암호화에 대해
date: 2018-05-11 18:27:55 +0900
description: 개인정보 암호화와 법률에 관한 이야기
img: encryption.jpg
tags: [etc]
---
몇달전 기회가 생겨 몇몇 한국 구매대행 쇼핑몰들의 소스들을 볼 기회가 있었습니다. 사용하고 있는 프레임워크나 서버환경 등이 오래된 것도 있겠지만 보면서 충격받은게 있습니다. 내부 DB의 고객정보가 전혀 암호화가 되어있지 않더군요. 3개 이상의 업체들의 내부로직을 봤었는데 이렇다는 건 저에게는 약간 충격이었습니다. 그 때 이후로 작은 싸이트들은 왠만하면 가입도 하지 않습니다.
실제로 시스템을 만들고 있는 입장에서 암호화에 대해 스스로도 지식을 정리할 필요가 있을 것 같아 포스트하게 됐습니다.

먼저 현재 기준에서의 법령을 살펴보면 아래와 같습니다.
> **개인정보의 안전성 확보조치 기준** - 제7조(개인정보의 암호화)<br/>
>
>① 개인정보처리자는 고유식별정보, 비밀번호, 바이오정보를 정보통신망을 통하여 송신하거나 보조저장매체 등을 통하여 전달하는 경우에는 이를 암호화하여야 한다.<br/>
>
>② 개인정보처리자는 비밀번호 및 바이오정보는 암호화하여 저장하여야 한다. 다만, 비밀번호를 저장하는 경우에는 복호화되지 아니하도록 **일방향 암호화**하여 저장하여야 한다.<br/>
>
>③ 개인정보처리자는 인터넷 구간 및 인터넷 구간과 내부망의 중간 지점(DMZ : Demilitarized Zone)에 고유식별정보를 저장하는 경우에는 이를 암호화하여야 한다.<br/>
>
>④ 개인정보처리자가 내부망에 고유식별정보를 저장하는 경우에는 다음 각 호의 기준에 따라 암호화의 적용여부 및 적용범위를 정하여 시행할 수 있다.
>
>1. 법 제33조에 따른 개인정보 영향평가의 대상이 되는 공공기관의 경우에는 해당 개인정보 영향평가의 결과<br/>
>2. 암호화 미적용시 위험도 분석에 따른 결과<br/>
>
>⑤ 개인정보처리자는 제1항, 제2항, 제3항, 또는 제4항에 따라 개인정보를 암호화하는 경우 안전한 암호알고리즘으로 암호화하여 저장하여야 한다.<br/>
>
>⑥ 개인정보처리자는 암호화된 개인정보를 안전하게 보관하기 위하여 안전한 암호 키 생성, 이용, 보관, 배포 및 파기 등에 관한 절차를 수립·시행하여야 한다.<br/>
>
>⑦ 개인정보처리자는 업무용 컴퓨터 또는 모바일 기기에 고유식별정보를 저장하여 관리하는 경우 상용 암호화 소프트웨어 또는 안전한 암호화 알고리즘을 사용하여 암호화한 후 저장하여야 한다.<br/>
>
>⑧ [별표]의 유형1 및 유형2에 해당하는 개인정보처리자는 제6항을 아니할 수 있다.<br/>
>
>출처[국가법령정보센터](http://www.law.go.kr/%ED%96%89%EC%A0%95%EA%B7%9C%EC%B9%99/%EA%B0%9C%EC%9D%B8%EC%A0%95%EB%B3%B4%EC%9D%98%EC%95%88%EC%A0%84%EC%84%B1%ED%99%95%EB%B3%B4%EC%A1%B0%EC%B9%98%EA%B8%B0%EC%A4%80)

위에서 확인하신 것 과 같이 개인정보 보호의 암호화는 법적으로 의무화 되어있습니다. 잘못하면 정말로 *무식한게 죄* 라는 말이 사실이 될 수도 있겠네요. 암호화의 관해서 만큼은 모든 개발자들이 기본 지식들을 습득하고 있어야 하겠다는 생각이 듭니다.
모든 내용이 중요하지만 개발자 입장에서 2번의 내용을 가지고 암호화 방법과 최신 트랜드에 대해 이야기해 보도록 하겠습니다.

<br/>
### 일방향 암호화(one way encryption)란

**일방향 암호화**란 일단 정보가 암호화 되면 다시 되돌리기(**복호화**)가 어려운 암호화를 말합니다. 그래서 일방향 암호화가 되어있는 웹사이트들의 경우 비밀번호 찾기를 하면 이전 비밀번호를 그대로 알려주는 경우가 없습니다. 임시 비번을 주고 다시 설정하라는 경우가 대부분이지요. 암호화가 잘 되어있는 경우는 관리자도 원래 비밀번호가 뭐였는지 알 수가 없습니다.

<br/>
### 일방향 암호화의 사용예
암호화에는 여러가지 방법이 있겠지만 여기서는 단방향 암호화만 다루도록 하겠습니다. 단방향 암호화를 이야기 할 때 해쉬(Hash) 알고리즘을 빼놓고는 이야기 하기가 어렵습니다. **해쉬 알고리즘**이란 추상적으로 말하자면 사용자가 입력한 값을 알아볼 수 없도록 복잡하게 꼬아놓은? 알고리즘을 말합니다. 때문에 한번 해쉬 알고리즘을 통과하고 나면 다시 원래 입력치로 돌리는게 매우 어렵습니다. 여기서 중요한 특징은 몇번을 해쉬알고리즘을 통과해도 항상 같은 값으로 암호화 된다는 특징입니다. 때문에 비밀번호 같은 정보를 서버에 저장할 때 해쉬 알고리즘을 이용해 암호화된 값을 일반적으로 저장하게 됩니다. 관리자 입장에서는 복호화 하기 어렵기 때문에 원래값이 뭐였는지 알 수는 없지만 사용자가 로그인 할 때마다 입력하는 비밀번호는 항상 같은 값으로 암호화 되기 때문에 암호화된 데이터를 비교해서 비밀번호가 맞다는 것을 인증하게 됩니다. 
>이 걔념에 대해서 알기 쉽게 설명한 블로그를 하나 링크 걸어둡니다.  
>https://steemit.com/kr/@twinbraid/4yjj7b

해쉬 알고리즘의 기본 원리는 나중에 기회가 되면 포스트 하도록 하겠습니다. 

<br/>
### 해쉬 알고리즘의 종류  

|알고리즘|해시값 크기|내부 상태 크기|블록 크기|길이 한계|워드 크기|과정 수|사용되는 연산|충돌|
|--------|-----------|--------------|---------|---------|---------|-------|-------------|----|
|SHA-0   |160        |160           |512      |64       |32       |80     |+,and,or,xor,rotl|발견됨|
|SHA-1   |160        |160           |512      |64       |32       |80     |+,and,or,xor,rotl|발견됨[1]|
|(SHA-2)SHA-256/224|256/224 |256(32바이트) |512      |64       |32       |64     |+,and,or,xor,shr,rotr|-|
|(SHA-2)SHA-512/384|512/384 |512(64바이트) |1024     |128      |64       |80     |+,and,or,xor,shr,rotr|-|

출처 [위키페디아](https://ko.wikipedia.org/wiki/SHA)

**SHA-0** 부터 숫자가 올라갈 수록 보안성도 올라갑니다. **SHA-1** 까지는 취약점이 공식적으로 발표되었기 때문에 **SHA-256** 이상의 사용이 의무화 되고 있습니다. (이렇게 얘기했지만 앞에서 언급했듯이 소규모 서비스들은 아직 암호화 하지 않은 업체들도 많이 있다는게 현실이죠....ㅠㅠ 여러분 조심하세요.) 2011년 1월 NIST 발표를 통해 **SHA-2**가 공식 권장 해쉬 표준으로 발표된 상태입니다. **SHA-3** 가 언제 공식적으로 사용될지는 아직까는 발표된 바는 없습니다. 제 경험상으로는 아직까지 사용하는 서비스는 본 적이 없었던 것 같습니다.

*참조*  
http://www.itworld.co.kr/insight/108321