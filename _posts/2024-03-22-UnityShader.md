---
title: Unity - Shader
date: YYYY-MM-DD HH:MM:SS +09:00
categories: [PORTPOLIO]
tags:
  [
    Unity,
    C#,
    Study
  ]
comments: false
math: true
mermaid: true
---


개발 환경 : Unity

Unity에서 여러 그래픽 스타일이나, 효과등을 만들어 보고 싶어
쉐이더에 입문하게 되었습니다. 

Shader 코드의 기본적인 구조를 이해하고
CG문법에 대해 공부하였습니다.

![Image Alt 텍스트]({{site.url}}/assets/img/CartoonShader.png )

<!-- <p style="font-size:25px">개발</p> -->
**개발**

<ul>
    <li>GrabPass를 사용하여 화면에 잡힌 내용을 가져오고, Normal Map을 더해줘 굴절 효과를 구현했습니다.</li>
    <li>Rim Lighting으로 가장자리에 그라데이션을 칠하고 가운데일수록 Alpha값을 낮게 주어 홀로그램 효과를 구현하였습니다.</li>
    <li>삼각 함수를 사용해, Vertex 위치를 조절하여 파도 물결을 구현하고, Texture Scrolling 으로 물 텍스쳐를 계속 움직여, 물이 흐르는 듯한 효과를 구현했습니다. </li>
</ul>








[GitHub Link](https://github.com/miro0325/) 




