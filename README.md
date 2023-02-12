
<dev align="center">

<img src="https://user-images.githubusercontent.com/100463560/218309569-00acc947-3ae0-45e7-abd1-865995aa9962.png"  width="90%"/>

### [Presentation(video)](https://www.youtube.com/watch?v=GT0m3ldshis)| [Demo(video)](https://youtu.be/CHE8jlSvEdQ)  | [Github](https://github.com/boostcampaitech4lv23nlp2/final-project-level3-nlp-12) | [Notion](https://www.notion.so/boostcampait/NLP-12-ET-BGM-54aac8e22a8b40dc9f03e904486702e1) 

---
### Team.ET
🚂🚋🚋🚋🚋🚋  
boostcamp 4th NLP Final Project :  
**영상 콘텐츠 맞춤형 BGM 생성**
  
  [![](https://camo.githubusercontent.com/44916b8f3c58815f4f7b5ad65f3487c593b0519b2deba925d242107d10df9e9c/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f707974686f6e2d3337373641423f7374796c653d666c6174266c6f676f3d707974686f6e266c6f676f436f6c6f723d7768697465)](https://camo.githubusercontent.com/44916b8f3c58815f4f7b5ad65f3487c593b0519b2deba925d242107d10df9e9c/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f707974686f6e2d3337373641423f7374796c653d666c6174266c6f676f3d707974686f6e266c6f676f436f6c6f723d7768697465)  [![](https://camo.githubusercontent.com/4837ae7c2bc54e02b707b9bdc6a1a02c00d5e8d019001c4fd81ca7746539fd5a/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5079546f7263682d4545344332433f7374796c653d666c6174266c6f676f3d5079546f726368266c6f676f436f6c6f723d7768697465)](https://camo.githubusercontent.com/4837ae7c2bc54e02b707b9bdc6a1a02c00d5e8d019001c4fd81ca7746539fd5a/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5079546f7263682d4545344332433f7374796c653d666c6174266c6f676f3d5079546f726368266c6f676f436f6c6f723d7768697465)
[![](https://camo.githubusercontent.com/d53bd5ccff8850c397f9140d39bd626861150abb38408cd4c6b28e1359eacd66/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f466173744150492d3030393638383f7374796c653d666c6174266c6f676f3d46617374415049266c6f676f436f6c6f723d7768697465)](https://camo.githubusercontent.com/d53bd5ccff8850c397f9140d39bd626861150abb38408cd4c6b28e1359eacd66/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f466173744150492d3030393638383f7374796c653d666c6174266c6f676f3d46617374415049266c6f676f436f6c6f723d7768697465)

</dev>

# 1. Team


# 2. About
### **기획의도**
 1인 미디어 시장 규모가 성장하고 있으며, 동영상 콘텐츠 제작의 비중이 대부분이고 이에 따라 BGM 수요 또한 증가하고 있다. 그러나, 늘어나는 동영상 수요와는 달리, 영상제작에 활용 가능한 BGM 의 경우 제한사항(저작권 분쟁과 로열티 비용 등)이 많이 존재하며 이 부분을 해결하고자 **AI 기반 음악 생성 모델을 활용하여 저작권 없는 BGM을 제공**하고자 한다.

### **개발목표**
 동영상을 입력하면, 해당 동영상으로부터 내용을 추출하여 감성 분석 후, 콘텐츠 내용에 맞는 감성을 분류하여 이를 바탕으로 riffusion 모델을 적용하여 BGM을 생성하고자 한다.

# 3. Model
> ### **FlowChart**
<p align="center">
<img src="https://user-images.githubusercontent.com/100463560/218309576-e7fe555d-9f2c-4c67-b1d2-205d8957cfdf.png"  width="80%"/>
</p>

> ### Step1 : 동영상 내용 파악

**Speech-to-Text**
- Openai의 Whisper model을 사용하여 전체 발화 내용을 텍스트로 추출.

**WHISPER 모델 사용 이유 :**
- SPEECH RECOGNITION에서 SOTA로 사용되는 wav2vec 2.0 대비 평균적으로 55.2% 낮은 오류율이라는 우수한 성능을 가졌음.
- Any-to-English speech translation multitask 기능을 제공하기에, STT와 번역기능을 함께 사용할 수 있어 추후 영문 데이터셋 활용 가능한 장점을 가져 선택하게 됨.

> ### Step2 : 동영상 감성 분류

**Sentiment Classifier**
- 전체 텍스트 내용을 알 수 있으면서 내용의 특징을 살릴 수 있도록, 텍스트 구문별로 감성 분류를 시도함.
- 전체 텍스트에 대해 구문별로 감성 분석하여 행복,슬픔,역겨움,분노,놀람,두려움, 중립 7가지 감정으로 분류함.
- 구문별 감성분류 후, 감정 유지기간이 임계값 보다 낮은 경우 해당 감정을 무시했으며, 무시된 감정의 앞뒤로 같은 감정일 경우 그 감정들과 이어진다고 판단하여 대체하는 후처리 과정을 진행.
- 그 결과 타임라인에 따라 안정된 감정을 파악할 수 있었고, 따라서 Sentiment Classifier 방식을 채택함.

> ### Step3 : 감성에 맞는 BGM 생성

**Riffusion Model 활용 및 학습**
- 리퓨전은 디퓨전 모델에 소리나 파동을 시각화하여 파악하기 위한 도구인 스펙트로그램을 학습한 모델.
- Step2에서 얻어진 감성 분류 결과를 prompt로 활용하여 그 감성과 같은 감성의 스펙트로그램을 seed image로 사용함.
- 사용자 편의를 위해 기존 영상에서 말소리를 제외한 음악이나 노이즈를 삭제하고 생성된 BGM을 합쳐서 최종 결과물을 생성함.

# 4. Dataset
> ### **Riffusion 추가 학습을 위한 Train Dataset 구축과정**
<p align="center">
<img src="https://user-images.githubusercontent.com/100463560/218309579-57e0d7fc-165c-4d4e-bdb9-4e2427b12665.png"  width="50%"/>
</p>

> ### Dataset : 
- hugging-face : Chr0my/Epidemic_music

# 5. Architecture
> ### **FlowChart**
<p align="center">
<img src="https://user-images.githubusercontent.com/100463560/218310472-c38abc7b-98f8-4908-8b7b-78c77e29d5c2.png"  width="80%"/>
</p>

# 6. How to Use
### **File Directory**
```

```

### **Environment**
```
Python Version 3.9.7 (Window)
```

### **Prerequisite**
```
import whisper
import 
```
