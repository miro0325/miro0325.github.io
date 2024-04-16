---
title: Unity - Temple Of Sita
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
* 장르 : 횡 스크롤 슈팅게임
* 플랫폼 : PC
* 역할 : 메인 시스템, 몬스터 패턴, 아웃게임, 연출
* 개발 환경 : Unity
* 개발 기간 : 5개월

## 게임 소개

웨이브 별로 몰려오는 몬스터들을 물리치며, 경험치를 얻어 캐릭터를 레벨업 시키고, 스킬을 선택하여  
플레이어를 키워 나가 보스를 잡아서 클러어하는 슈팅 게임입니다.  

학교 프로젝트에 참여하여, Gstar에 출품한 게임입니다.  

## Play Video
{% include embed/youtube.html id='edrxeZIffk4' %}

## 기능 구현


* **Outline Shader**
  * Shader(CG)를 사용하여 Outline Shader를 제작하고,  
    디버프가 걸린 몬스터 Outline Color에 차이를 줘 디버프 유무를 확인할 수 있게 구현하였습니다.
* **일일 퀘스트**
  * Observer Pattern을 사용하여, 이벤트들을 받아 퀘스트를 구현했으며 날짜를 PlayerPrefs와 JsonUtility를 이용해 저장하고, 현재 시간을 받아와 날짜가 바뀌면, 초기화 되도록 구현하였습니다. 
* **곡선 탄환**
  * 베지어 곡선을 사용하여 부드러운 곡선 탄환을 구현하였습니다.

<span style="font-size: 30px;"> [Github Link](https://github.com/miro0325/Temple_Of_Sita) </span>  



