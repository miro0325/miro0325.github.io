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

장르 : 3D 횡 스크롤 슈팅게임
플랫폼 : PC

역할 : 프로그래밍

개발 환경 : Unity

**게임 개요**

몰려오는 적들을 물리치며, 캐릭터를 레벨업 시키고, 능력을 선택하여
플레이어를 키워 나가며 강해지는 게임입니다.

**맡은 요소**

레벨 업, 플레이어 스킬, 적 패턴, 일일 퀘스트, 게임 오버  

**[Play Video]**
{% include embed/youtube.html id='2ym6mHKbVWA' %}

**개발**

<ul>
    <li>버프를 표시 하기 위해 Outline Shader를 제작하여, 버프에 걸린 엔티티에게 Outline Color를 변경하여, 표시했습니다.</li>
    <li>Observer Pattern을 사용하여, 이벤트를 받아오고 
		날짜를 감지하여 하루가 지나면 초기화 되는 일일 퀘스트를 구현하였습니다.
	</li>
    <li>베지어 곡선을 사용하여 곡선 탄환을 구현하였습니다.</li>
</ul>

[GitHub Link](https://github.com/miro0325/Temple_Of_Sita) 


