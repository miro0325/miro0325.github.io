---
title: Unity - Future Space
date: YYYY-MM-DD HH:MM:SS +09:00
categories: [PORTPOLIO]
tags:
  [
    Unity,
    C#,
    기능 대회 연습작
  ]
comments: false
math: true
mermaid: true
---
## 게임 정보
*    장르 : 종 스크롤 슈팅게임
*    플랫폼 : PC
*    개발 환경 : Unity
*    역할 : 전체 개발
*    개발 기간 : 1주

## 게임 소개

기능 대회 연습작으로, 짧은 시간 내 대회 조건에 맞게 개발하는데 집중했습니다.  

우주에서 라운드마다 몰려오는 우주선들을 처리하며 보스에게 도달하고,  
보스를 처치해 클리어하는 게임입니다.

## Play Video
{% include embed/youtube.html id='lCvenjHqRFs' %}


## 기능 구현

* **랭킹 시스템**
  *  JsonUtility 기능을 사용해 플레이어 이름과 점수를 Json 파일에 저장하고 불러와 플레이어 랭킹을 구현했습니다.
* **오브젝트 관리**
  * Object Pool 패턴을 사용해 적들이나 탄환들을 재사용해, GC 사용량을 줄이고 오브젝트들을 효율적으로 사용했습니다.
* **몬스터 패턴**
  * 삼각 함수를 사용하여 다양한 탄막 패턴을 제작했습니다.  

<span style="font-size: 30px;">[GitHub Link](https://github.com/miro0325/FutureSpace)</span>

