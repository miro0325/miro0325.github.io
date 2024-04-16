---
title: Unity - Escape From
date: YYYY-MM-DD HH:MM:SS +09:00
categories: [PORTPOLIO]
tags:
  [
    Unity,
    C#,
    Team Project
  ]
comments: false
math: true
mermaid: true
---
## 게임 정보

*    장르 : 공포 스릴러 퍼즐게임
*    플랫폼 : PC
*    개발 환경 : Unity
*    역할 : 퍼즐, 몬스터 AI, 연출 담당
*    개발 기간 : 1달

## 게임 소개
전공 동아리가 진행했던 게임잼에서 만든 작품입니다.  

폐교에서 퍼즐을 풀어 탈출하는 게임입니다.  

공포 게임 느낌을 주는데 집중하여 개발하였습니다.  


## Play Video
{% include embed/youtube.html id='uoeCP4sKrGo' %}


## 기능 구현

* **몬스터 AI**
  * NavMesh를 이용해 맵을 구워 이동 가능한 구역을 지정하였고,  
  몬스터가 자연스럽게 맵을 순찰하고 플레이어를 추격하도록를 제작했습니다.  
    
* **매니저**
  * Singleton 패턴을 사용하여 매니저들을 쉽게 접근하여, 데이터를 공유 가능하게 구현하였습니다.  

<span style="font-size: 30px;"> [Github Link](https://github.com/Proffeine0327/EscapeFrom) </span>  

