---
title: Unity - Digitech Company[개발중]
date: YYYY-MM-DD HH:MM:SS +09:00
categories: [PORTPOLIO]
tags:
  [
    Unity,
    C#,
    Team Project,
    졸업작품,
    개발중
  ]
comments: false
math: true
mermaid: true
---
## 게임 정보
* 장르 : 4인 협동 멀티 공포
* 플랫폼 : PC
* 역할 : Shader, 연출, 메인 시스템 담당
* 개발 환경 : Unity
* 개발 기간 : 2024-03~

## 게임 소개

졸업 작품으로, 리썰 컴퍼니의 모작입니다.  
기존 리썰 컴퍼니처럼 플레이어들끼리 아이템을 기간 내 파밍하고 판매해 할당량을 채우는 부분까지는 동일하나,   
집을 꾸며 효과를 얻을 수 있는 하우징 시스템, 플레이어 능력치를 분배해 강화할 수 있는 스탯 시스템 등 여러 시스템을 추가 제작할 예정입니다.  


## 인게임 요소


**Pixel Rendering + Cartoon Rendering**  

![Image Alt 텍스트]({{site.url}}/assets/img/digitech.png )  

**명령어를 칠수 있는 Terminal 기능**  

![Image Alt 텍스트]({{site.url}}/assets/img/terminal.png )  



## 기능 구현

* **픽셀화**
  *  Shader(hlsl)을 사용하여, Pixelate Shader를 제작하고, Postprocessing의 Volume Component에 추가해 Global Volume에서 쉽게 Shader를 조절할 수 있게 구현하였습니다.
* **명령어** 
  * Scriptable Object를 사용해 Command 클래스를 제작하고, 명령어 클래스들에게 상속시켜 명령어을 만들고, 터미널에서 Input Field로 명령어와 필요시 Argument를 입력받아 실행되게 구현하였습니다.  

<span style="font-size: 30px;">[GitHub Link](https://github.com/miro0325/Digitech_Company) </span>




