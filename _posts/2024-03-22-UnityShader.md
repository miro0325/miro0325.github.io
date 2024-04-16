---
title: Unity - Shader
date: YYYY-MM-DD HH:MM:SS +09:00
categories: [PORTPOLIO]
tags:
  [
    Unity,
    CG,
    Study
  ]
comments: false
math: true
mermaid: true
---


개발 환경 : Unity  

[GitHub Link](https://github.com/miro0325/) 

## 공부 내용

Unity에서 여러 그래픽 스타일이나, 효과등을 만들어 보고 싶어
쉐이더에 입문하게 되었습니다. 

Shader 코드의 기본적인 구조를 이해하고
CG문법에 대해 공부하여, 다양한 쉐이더 효과들을 제작하였습니다.

## 영상
{% include embed/youtube.html id='_emUx8IzS-s' %}
<!-- /![Image Alt 텍스트]({{site.url}}/assets/img/CartoonShader.png ) -->

<!-- <p style="font-size:25px">개발</p> -->
## 기능 구현

* 왜곡 효과
  * GrabPass를 사용하여 화면에 잡힌 내용을 가져오고, Normal Map을 더해줘 굴절 효과를 구현했습니다.
* 홀로그램 효과
  * Rim Lighting으로 가장자리에 그라데이션을 칠하고 가운데일수록 Alpha값을 낮게 주어 홀로그램 효과를 구현하였습니다.
* 파도
  * 삼각 함수를 사용해, Vertex 위치를 조절하여 파도 물결을 구현하고, Texture Scrolling 으로 물 텍스쳐를 계속 움직여, 물이 흐르는 듯한 효과를 구현했습니다.


  ### 왜곡 효과

  ```c
  Shader "Custom/GlassShader"
{
    Properties
    {
        _MainTex ("Albedo (RGB)", 2D) = "white" {}
        _Color ("Color", Color) = (1,1,1,1)
        _BumpMap ("Normal Map",2D) = "bump" {}
        _ScaleUV ("Scale",Range(1,10)) = 1
    }
    SubShader
    {
        Tags { "Queue" = "Transparent" }
        //화면에 잡힌 내용을 가져온다.
        //정확히는 화면에 잡힌 프레임 버퍼 내용을 가져옵니다 
        GrabPass {}
        Pass 
        {
            CGPROGRAM
            #pragma vertex vert
            #pragma fragment frag

            #include "UnityCG.cginc"

            struct appdata 
            {
                float4 vertex : POSITION;
                float2 uv : TEXCOORD0;
            };

            struct v2f
            {
                float2 uv_MainTex : TEXCOORD0;
                float4 uv_GrabTex : TEXCOORD1;
                float2 uv_BumpMap : TEXCOORD2;
                float4 vertex : SV_POSITION;
            };

            sampler2D _GrabTexture;
            sampler2D _MainTex;
            sampler2D _BumpMap;

            float4 _GrabTexture_TexelSize;
            float4 _MainTex_ST;
            float4 _BumpMap_ST;
            float _ScaleUV;
            float _Speed;

            float4 _Color;
            
            v2f vert(appdata v) 
            {
                v2f o;
                //왜곡된 화면이 뒤집히는 것을 방지
                # if UNITY_UV_STARTS_AT_TOP
                float scale = -1.0;
                # else
                float scale = 1.0f;
                # endif
                //3D vertex좌표를 2D 화면 위치로 변환
                o.vertex = UnityObjectToClipPos(v.vertex);
                //uv값을 조절해 오브젝트 너머 화면이 비추도록 조절
                o.uv_GrabTex.xy = (float2(o.vertex.x,o.vertex.y * scale) + o.vertex.w) * 0.5;
                o.uv_GrabTex.zw = o.vertex.zw;
                o.uv_MainTex = TRANSFORM_TEX(v.uv, _MainTex);
                o.uv_BumpMap = TRANSFORM_TEX(v.uv, _BumpMap);
                return o;
            }

            fixed4 frag(v2f i) : SV_Target 
            {
                //Normal Map 값을 GrabTexture의 Texel 크기에 곱해 왜곡 효과를 준다
                fixed2 bump = UnpackNormal(tex2D(_BumpMap,i.uv_BumpMap)).rg;
                fixed2 offset = bump * ((_ScaleUV-1) * 10000) * _GrabTexture_TexelSize.xy;
                //GrabTexture의 uv값에 왜곡을 곱해준다
                i.uv_GrabTex.xy = offset * i.uv_GrabTex.z + i.uv_GrabTex.xy; 
                //GrabTexture를 오브젝트에 적용 시켜준 후 MainTex와 합쳐준다.
                fixed4 col = tex2Dproj(_GrabTexture, UNITY_PROJ_COORD(i.uv_GrabTex));
                fixed4 tint = tex2D(_MainTex, i.uv_MainTex);
                col *= (tint * _Color);
                return col;
            }
            ENDCG

        }
       
    }
    FallBack "Diffuse"
}
  ``` 
    
  `GrabPass`를 이용해 화면에 잡힌 프레임 버퍼 내용을 가져오고, **Vertex & Fragment Shader**에서  
  `vert` 함수에서 `GrabTexture`의 uv값을 조절해 물체뒤에 있는 물체가 정상적으로 화면에 보이도록 조절해줍니다.    
    
  `frag` 함수에서 `Normal Map` 값과 `GrabTexture`의 텍셀 사이즈를 곱해 왜곡 효과를 만든 뒤
  `GrabTexture`의 uv값에 곱해줍니다. 화면에 잡힌 `GrabTexture`와 `MainTexture`를 곱해준 후 오브젝트에 적용하여 오브젝트 너머 물체가 왜곡되어 보이게 만들었습니다.

  ### 홀로그램 효과
  
  ```c
  Shader "Custom/Hologram"
{
    Properties
    {
        _Color ("Color", Color) = (1,1,1,1)
        _MainTex ("Albedo (RGB)", 2D) = "white" {}
        _RimColor ("Rim Color", Color) = (1,1,1,1)
        _RimPower ("Rim Power", Range(0.5, 8)) = 1
    }
    SubShader
    {
        Tags { "Queue"="Transparent" }
        //오브젝트 뒤가 보이게 하기 위한 Pass
        Pass 
        {
            ZWrite On
            ColorMask 0
        }

        LOD 200

        CGPROGRAM
        #pragma surface surf Lambert alpha:fade

        #pragma target 3.0

        sampler2D _MainTex;

        struct Input
        {
            float2 uv_MainTex;
            float3 viewDir;
        };

        float4 _RimColor;
        float _RimPower;
        fixed4 _Color;

        UNITY_INSTANCING_BUFFER_START(Props)
        UNITY_INSTANCING_BUFFER_END(Props)

        void surf (Input IN, inout SurfaceOutput o)
        {
            fixed4 c = tex2D (_MainTex, IN.uv_MainTex) * _Color;
            o.Albedo = c.rgb;
            //내적을 이용해 음영을 구한 뒤 1을 빼 역광을 구합니다.
             half rim = 1 - saturate(dot(normalize(IN.viewDir),o.Normal));
            //Emission 값에 역광과 _RimPower를 제곱한 뒤 곱해 RimLight를 구현합니다.
            o.Emission = _RimColor.rgb * pow(rim,_RimPower) * 10;
            //
            o.Alpha =  pow(rim,_RimPower);
        }
        ENDCG
    }
    FallBack "Diffuse"
}

  ```
`vertex`의 `Normal` 값과 카메라의 `viewDir`를 내적해 음영 값을 구한 뒤 1을 빼 역광을 구합니다.
역광과 `RimPower`를 제곱한 뒤 Emission 값에 넣어 물체 가장자리 부분을 그라데이션처럼 칠해 준 후
Alpha 값에 역광 값을 넣어 가운데로 갈 수록 투명해지게 하여 홀로그램 효과를 구현했습니다.

  ### 파도

  ```c
  Shader "Custom/WaterShader"
{
    Properties
    {
        _Color ("Color", Color) = (1,1,1,1)
        _MainTex ("Albedo (RGB)", 2D) = "white" {}
        _FormTex ("Form", 2D) = "white" {}
        _ScrollUVX("Scrool UV X",Range(-10,10)) = 1
        _ScrollUVY("Scrool UV Y",Range(-10,10)) = 1
        _ScrollSpeed("Scroll Speed",Range(0,10)) = 1
        _Tint("Colour Tint", Color) = (1,1,1,1)
        _Freq("Frequency", Range(0,10)) = 3
        _WaveSpeed("Wave Speed", Range(0,100)) = 10
        _Amp("Amplitude", Range(0,10)) = 0.5
    }
    SubShader
    {
         CGPROGRAM
        #pragma surface surf Lambert vertex:vert 
        struct Input 
        {
            float2 uv_MainTex;
            float2 uv_FormTex;
            float3 vertexColor;
        };

        struct appdata 
        {
            float4 vertex : POSITION;
            float3 normal : NORMAL;
            float4 texcoord : TEXCOORD0;
            float4 texcoord1 : TEXCOORD1;
            float4 texcoord2 : TEXCOORD2;
        };

        float _ScrollSpeed;
        float _ScrollUVX;
        float _ScrollUVY;
        float4 _Color;
        
        float _WaveSpeed;
        float _Freq;
        float _Amp;
        float4 _Tint;

        sampler2D _MainTex;
        sampler2D _FormTex;
       
       void vert(inout appdata v, out Input o) 
        {
            UNITY_INITIALIZE_OUTPUT(Input,o);
            float t = _Time * _WaveSpeed;
            //삼각 함수를 이용해 버텍스 위치를 조절해 파도 모양을 만든다 
            float waveHeightX = cos(t + v.vertex.x * _Freq) * _Amp;
            float waveHeightZ = sin(t + v.vertex.z * _Freq) * _Amp;
            float waveHeight = (waveHeightX + waveHeightZ)/2;
            //버텍스 y값에 파도 높이를 더해 준다.
            v.vertex.y = v.vertex.y + waveHeight;
            v.normal = normalize(float3(v.normal.x + waveHeight,v.normal.y,v.normal.z + waveHeight));
            //높이에 따라 색상 변화를 살짝 준다.
            o.vertexColor = waveHeight + 2;
        }

        void surf(Input IN, inout SurfaceOutput o) 
        {
            //uv값을 계속 조절하여 텍스쳐가 움직이는 듯한 효과를 준다
            _ScrollUVX *= _Time * _ScrollSpeed;
            _ScrollUVY *= _Time * _ScrollSpeed;
            float2 mainUV = IN.uv_MainTex + float2(_ScrollUVX,_ScrollUVY);
            float4 col = tex2D(_MainTex, mainUV);
            float2 formUV = IN.uv_FormTex + float2(_ScrollUVX / 2,_ScrollUVY / 2); 
            float4 form = tex2D(_FormTex, formUV);
            float3 final = (col.rgb + form.rgb)/2 * _Color;
            final * IN.vertexColor.rgb;
            o.Albedo = final;
        }
        ENDCG
    }
    FallBack "Diffuse"
}

  ```
  텍스쳐 uv값을 움직여 텍스쳐가 움직이는 듯한 효과로 물이 흐르는 듯한 효과를 주고, 
  Vertex값에 삼각함수를 이용해 vertex값 높이를 조절하여 파도가 치는 듯한 효과를 구현하였습니다.