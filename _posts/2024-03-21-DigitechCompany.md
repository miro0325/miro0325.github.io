---
title: Unity - Digitech Company
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
* 장르 : 4인 협동 멀티
* 플랫폼 : PC
* 역할 : 연출, 몬스터 AI, 아이템
* 개발 환경 : Unity
* 개발 기간 : 2024-03~2024-07

## 게임 소개

리썰 컴퍼니의 모작입니다.  
기존 리썰 컴퍼니처럼 플레이어들끼리 아이템을 파밍하고 판매하거나 구매하는 등 리썰 컴퍼니의 메인이라 할수 있는 시스템을 구현하였습니다.   

## 인게임 요소

 
**Pixel Rendering + Cartoon Rendering**  

![Image Alt 텍스트]({{site.url}}/assets/img/digitech.png )  

**명령어를 칠수 있는 Terminal 기능**  

![Image Alt 텍스트]({{site.url}}/assets/img/terminal.png )  

**스타일라이즈 쉐이더**  

![Image Alt 텍스트]({{site.url}}/assets/img/pbrshader.png )  

**인게임**

![Image Alt 텍스트]({{site.url}}/assets/img/scan.png )
![Image Alt 텍스트]({{site.url}}/assets/img/scan2.png )
![Image Alt 텍스트]({{site.url}}/assets/img/sell.png )
![Image Alt 텍스트]({{site.url}}/assets/img/terminal2.png )
![Image Alt 텍스트]({{site.url}}/assets/img/delivary.png )

## 기능 구현

* **스타일라이즈 쉐이더**
  *  Shader(hlsl)을 사용하여, PBR 기반의 Stylized Lit Shader를 제작하여
  스타일라이즈 그래픽을 구현하였습니다.
* **픽셀화**
  *  Shader(hlsl)을 사용하여, Pixelate Shader를 제작하고, Postprocessing의 Volume Component에 추가해 Global Volume에서 쉽게 Shader를 조절할 수 있게 구현하였습니다.
* **명령어** 
  * Scriptable Object를 사용해 Command 클래스를 제작하고, 명령어 클래스들에게 상속시켜 명령어을 만들고, 터미널에서 Input Field로 명령어와 필요시 Argument를 입력받아 실행되게 구현하였습니다.  
* **몬스터 AI** 
  *  Behavior Tree로 몬스터 행동 패턴을 제작하여 몬스터 AI를 구현하였습니다.  

<span style="font-size: 30px;">[GitHub Link](https://github.com/miro0325/Digitech_Company) </span>




