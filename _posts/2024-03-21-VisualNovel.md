---
title: Unity - VisualNovel
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

다양한 게임들을 해보면서, 비주얼 노벨식 연출을 많이 봐왔고,
그로 인해 한번 만들어보고 싶어 구현해보게 되었습니다.

**[Play Video]**
{% include embed/youtube.html id='ANYZy58OLfg' %}

**개발**

<ul>
    <li>UnityWebRequest를 사용해Google Sheet를 받아와 스토리 진행에 필요한 대사, 효과, 움직임, 감정 표현, 등 데이터를 받아와 파싱하여 그대로 실행하도록 구현하였습니다.
    </li>
    <li>char 배열로 문장을 받아, Coroutine을 사용해 글자를 차례대로 출력해
    타이핑 효과를 구현했습니다.
    </li>
</ul>

[GitHub Link](https://github.com/miro0325/VisualNovel) 


