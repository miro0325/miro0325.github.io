---
title: Unity - CyberSeeds
date: YYYY-MM-DD HH:MM:SS +09:00
categories: [PORTPOLIO]
tags:
  [
    Unity,
    C#,
    Team Project,
    GameJam
  ]
comments: false
math: true
mermaid: true
---


장르 : 멀티, 카드, 배틀, 보드게임

플랫폼 : PC

역할 : 프로그래밍

개발 환경 : Unity

2023 교내 게임잼에서 제작한 게임으로, 기간 내 나뭇잎을 수집해 팔아 돈을 벌고, 
장비를 업그레이드하여 나무를 특정 수준까지 성장시키는 캐주얼 게임입니다.

게임잼 기간 내 제작하기 위해 팀 내 역할을 분할하고, 코드를 간결하게 쓰기 위해 노력했습니다.

**[Play Video]**
{% include embed/youtube.html id='gKwReIauHaU' %}

**개발**

<ul>
    <li>
    State 패턴을 사용하여, 날짜가 계절이 바뀔 때마다 ISeasonBase Interface를 상속받은 계절(Spring,Summer 등) 클래스를 할당하여, 계절에 맞는 이벤트나 효과를 쉽게 구현 가능하게 하였습니다.
    </li>
    <li>
    Shader Graph를 사용하여, 눈 텍스쳐에 Dissolve 효과를 주고 스크립트로 Dissolve값을 조정하여 부드럽게 눈이 쌓이는 효과를 구현하였습니다. 
    </li>
</ul>


[GitHub Link](https://github.com/miro0325/TreeGrowth) 




