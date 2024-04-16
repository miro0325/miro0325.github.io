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

[GitHub Link](https://github.com/miro0325/VisualNovel) 

## 공부 내용

다양한 게임들을 해보면서, 비주얼 노벨식 연출을 많이 봐왔고,
그로 인해 한번 만들어보고 싶어 구글 스프레드 시트를 연동해 
데이터들을 받아오고 다이얼로그 시스템에 맞게 데이터를 파싱해 
비주얼 노벨 식 스토리 연출을 유니티에서 구현했습니다.

## 영상
{% include embed/youtube.html id='ANYZy58OLfg' %}

## 기능 구현

* **구글 스프레드 시트**
  * UnityWebRequest를 사용해Google Sheet를 받아와 스토리 진행에 필요한 대사, 효과, 움직임, 감정 표현, 등 데이터를 받아와 파싱하여 그대로 실행하도록 구현하였습니다.
* **다이얼로그 시스템**
  * char 배열로 문장을 받아, Coroutine을 사용해 글자를 차례대로 출력해
    타이핑 효과를 구현했습니다.

### 시트 데이터 받아오기
```csharp
  public class SheetImporter : MonoBehaviour
{
    public static SheetImporter Instance { get; private set; }

    public bool IsLoad => isLoad;

    private readonly string SHEET_ADDRESS = "https://docs.google.com/spreadsheets/d/1-NP8GVR_9VYLyoQrqjREOahXRpfndTx5G3DEfUBNDug/export?format=tsv&range=A1:G";

    private bool isLoad = false;

    private List<Dictionary<string, object>> sheetData = new();

    public List<Dictionary<string, object>> GetData()
    {
        if (!isLoad || sheetData.Count == 0)
        {
            Debug.LogError("Data is loading or not loaded");
            return null;
        }
        else
        {
            return sheetData;
        }
    }

    private void Awake()
    {
        if(Instance == null)
        {
            Instance = this;
            DontDestroyOnLoad(gameObject);
        } else
        {
            Destroy(gameObject);
        }
        StartCoroutine(Import());
    }

    private IEnumerator Import()
    {
        using(UnityWebRequest www = UnityWebRequest.Get(SHEET_ADDRESS))
        {
            yield return www.SendWebRequest();
            if(www.isDone)
            {
                ImportData(www.downloadHandler.text);
            }
        }
    }
    
    private void ImportData(string data)
    {
        if (string.IsNullOrEmpty(data)) return;
        string[] lines = data.Trim().Split('\n');

        string[] headers = lines[0].Trim().Split('\t');
        for(int i = 1; i < lines.Length; i++)
        {
            string[] values = lines[i].Trim().Split('\t');
            var datas = new Dictionary<string, object>(values.Length);
            for(int j = 0; j < values.Length; j++)
            {
                string value = values[j].Trim();
                if (string.IsNullOrEmpty(value)) continue;
                value = value.TrimStart().TrimEnd();
                object final = value;
                Debug.Log(final);
                int n;
                float f;

                if (int.TryParse(value, out n))
                {
                    final = n;
                }
                else if (float.TryParse(value, out f))
                {
                    final = f;
                }
                Debug.Log(headers[j]);
                datas[headers[j]] = final;
            }
            sheetData.Add(datas);
        }

        isLoad = true;
    }
    
}
```
UnityWebRequest를 통해 구글 스프레드 시트 데이터를 요청하고, 받아올 때까지 기다립니다.

데이터를 받아온 뒤 **ImportData** 함수를 통해 Header와, 데이터들을 정리하여 sheetData에 저장합니다.

### 다이얼로그 텍스트 실행
```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using TMPro;



public class DialogueText : MonoBehaviour
{
    public static DialogueText Instance { get; private set; }
    
    TextMeshProUGUI tempText;
    [SerializeField] float timeForChar;
    [SerializeField] float timeForChar_Fast;

    float charTime;

    float timer;

    string saves;

    bool isDialogEnd = false;
    bool isTypingEnd = false;

    int dialogNumber = 0;

    Coroutine coroutine = null;

    public bool IsTypingEnd()
    {
        return isTypingEnd; 
    }


    public void Typing(string dialogs, TextMeshProUGUI text)
    {
        isDialogEnd = false;
        saves = dialogs;
        tempText = text;
        coroutine = StartCoroutine(Typer(dialogs.ToCharArray(), text));
        
    }

    IEnumerator Typer(char[] chars, TextMeshProUGUI text)
    {
        int currentChar = 0;
        charTime = timeForChar;
        int charLength = chars.Length;
        isTypingEnd = false;
        text.text = "";
        while(currentChar < charLength)
        {
            if(timer >= 0)
            {
                yield return null;
                timer-=Time.deltaTime;
            } else
            {
                text.text += chars[currentChar].ToString();
                currentChar++;
                timer = charTime;
            }
        }
        if(currentChar >= charLength)
        {
            isTypingEnd = true;
            dialogNumber++;
            coroutine = null;   
            yield break;
        }

    }

    public void EndTyping()
    {
        
        if (!isTypingEnd)
        {
            charTime = timeForChar_Fast;
        }
    }

    void Start()
    {
        if (Instance == null) Instance = this;
        else Destroy(this);
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            EndTyping();
        }
    }
}
```
**Typing** 함수를 실행시켜 전달 받은 문장을 char[] 배열로 받아 딜레이 마다 단어 하나씩 텍스트 UI에 추가해  
타이핑되는 듯한 효과를 구현 하였습니다.  

스페이스 바를 입력 받을 시 딜레이 시간을 **EndTyping** 함수를 실행하여 timeForChar_Fast로 교체하여, 문장이 바로 완성하도록 구현하였습니다.
