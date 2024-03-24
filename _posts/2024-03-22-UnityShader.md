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

간단한 Cartoon Shader를 제작하였습니다.

**개발**

- ![Image Alt 텍스트]({{site.url}}/assets/img/CartoonShader.png )

Outline
```cg
 ST_VertexOutput _VertexFuc(ST_VertexInput stInput) 
 {
    ST_VertexOutput stOutput;
    stInput.color = _OutlineColor;

    float3 fNormalized_Normal = normalize(stInput.normal); //Vertex Normal값 받아오기
    float3 fOutline_Position = stInput.vertex + fNormalized_Normal * (_Outline_Bold * 0.1f); //Normal값 방향으로 Vertex 확장

    stOutput.vertex = UnityObjectToClipPos(fOutline_Position);
    stOutput.color = stInput.color;
    return stOutput;
                    
}
```
Pass를 2개를 그려 하나에서
Vertex의 Normal을 받아와 Object의 크기보다 크게 확장시켜 아웃라인을 표현


Toon
```cg
float Toon(float3 normal, float3 lightDir) 
{
    float NdotL =  max(0.0,dot(normalize(normal),normalize(lightDir))); //빛의 방향을 내적을 통해 그림자를 구현

    return floor(NdotL/0.3); //floor로 값을 층으로 나눠 단계별 그림자 형성
}
```
빛의 방향을 받아오고 빛의 방향과 Normal값을 내적해 그림자를 구현하고,
floor로 그림자에 층을 형성시켜 카툰풍을 표현함

[GitHub Link](https://github.com/miro0325/) 




