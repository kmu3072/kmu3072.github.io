---
layout: post
title:  "Google Analytics 적용"
date:   2021-12-13 23:28:30 +0900
categories: jekyll update
comments: true
---

## Google Analytics 가입
1. 먼저 [Google Analytics]에 접속
2. 계정 이름 및 속성 설정
   - 이때, **유니버설 애널리틱스 속성 만들기**에 **반드시** 체크

[Google Analytics]: "https://analytics.google.com/analytics/web/"

## Google Analytics를 블로그에 적용하기
### 추적 ID 및 추적 코드 받아오기
1. 왼쪽 하단에서 **관리** 클릭
2. **추적 정보** 클릭한 후 **추적 코드** 클릭
3. **추적 ID**와 다음의 ```gtag.js``` 코드를 복사하기

```html
   <!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=UA-215132491-1"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', '추적 ID가 들어갈 위치');
</script>
```

### 추적 코드를 파일에 적용시키기

1. 로컬 저장소의 _includes 폴더에 ```analytics.html``` 파일 생성 후 위 코드 붙여넣기
2. _layouts 폴더의 ```default.html``` 파일에 다음 코드 입력하기
```{``` ```%``` ```include analytics.html``` ```%``` ```}```   
3. ```_config.yml``` 파일에 다음 코드 입력하기

```html
  analytics:
     provider:      "google"
     google:
       tracking_ID: "추적 ID 입력"
```

이후 commit하고 push한 이후, [Google Analytics]에서 경과 지켜보기 