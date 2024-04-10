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

장르 : 횡 스크롤 로그라이크 슈팅게임
플랫폼 : PC

역할 : 프로그래밍

개발 환경 : Unity

**게임 개요**

몰려오는 적들을 물리치며, 캐릭터를 레벨업 시키고, 능력을 선택하여
플레이어를 키워 나가며 강해지는 게임입니다.

**맡은 요소**

레벨 업, 플레이어 스킬, 적 패턴, 일일 퀘스트, 게임 오버  

**[Play Video]**
{% include embed/youtube.html id='edrxeZIffk4' %}

**개발**

<ul>
    <li>Shader(CG)를 사용하여 Outline Shader를 제작하고,
     디버프가 걸린 몬스터 Outline Color에 차이를 줘 디버프 유무를 확인할 수 있게 구현하였습니다.
    </li>
    <li>Observer Pattern을 사용하여, 이벤트들을 받아 
    퀘스트를 구현했으며 날짜를 PlayerPrefs와 JsonUtility를 이용해 저장하고, 현재시간을 받아와 날짜가 바뀌면, 초기화 되도록 구현하였습니다. 
	  </li>
    <li>베지어 곡선을 사용하여 부드러운 곡선 탄환을 구현하였습니다.
    </li>
</ul>

[GitHub Link](https://github.com/miro0325/Temple_Of_Sita) 


