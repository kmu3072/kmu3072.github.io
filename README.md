# 프로젝트 빌드 과정

## Git 저장소 생성 및 GitHub 연동
1. Git을 컴퓨터에 설치
2. 로컬 저장소로 사용할 폴더 결정 후 ```git init``` 명령어를 통해 로컬 저장소 지정
3. kmu3072.github.io라는 이름의 원격 저장소 생성
4. ```git clone <respository> <path>```를 통해 GitHub의 원격 저장소와 연결

### Git 테스트
1. 파일 작성
2. ```git status``` 통해 내부 파일 상태 확인
3. ```git add <filename>```으로 commit란에 파일 추가
4. ```git commit -m "message"``` 통해 메시지를 덧붙이고 commit
5. ```git branch -M main```으로 branch의 이름을 main으로 변경 후 GitHub에서 PAT(Personal Access Token)을 가져온 뒤에 
   ```git push origin main```으로 push

##Jekyll 사용하기
1. ```gem install bundler jekyll```로 Jekyll 설치
2. ```jekyll -v```로 설치 확인 후 ```jekyll new . --force```로 현재 디렉터리에 jekyll 설치
3. ```bundle exec jekyll serve```로 서버 개방 후 ```localhost:4000```으로 jekyll 페이지 접속
4. ```_config.yml```을 원하는 대로 수정한 후 Git을 통해 commit하고 push 후 반영되었는지 확인

##블로그 포스트 업로드하기
1. _posts 폴더에 YYYY-MM-DD-제목.md 형태로 markdown 파일 생성
2. 문서의 맨 위에 다음과 같은 형태로 초기 설정
   ```
   ---
   layout : post
   title : 제목
   date : YYYY-MM-DD HH:MM:SS +0900
   categories : jekyll update
   ---
   ```
3. Markdown 형식을 통해 원하는 내용 작성 후 commit 및 push, 이후 결과물 확인

## 테마 적용하기
1. ```http://jekyllthemes.org/``` 접속 후 원하는 테마 탐색
2. ```git clone```을 통해 로컬 저장소로 받아온 후 _posts 제외한 폴더 및 파일 덮어쓰기
3. commit 후 push한 후 결과물 확인

## 댓글 기능 추가
1. ```https://disqus.com``` 접속 후 회원가입 
2. "I want to install Disqus on my site" 선택 후 사이트 이름 입력
3. Jekyll 선택 후 Install Instruction을 숙지한 뒤에 Configure를 눌러 진행
4. 사이트 주소 입력 후 댓글 정책 설정
5. 다음과 같은 key value 추가
```
---
comment:
 provider:        "disqus"
 disqus:
   shortname:     "kmu3072"
---
```
6. disqus 홈페이지에서 Universal Code 복사 후 _layouts 폴더의 post.html에 삽입
  - 이때, 코드 맨 끝자리에 ```{% endif %}```를 삽입해주어야 함

7. 복사해 온 Universal Code를 다음과 같이 수정
```html
{% if page.comments %}
<h2>Comments</h2>
<div id="disqus_thread"></div>
<script>
    /**
    *  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
    *  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables    */
    let PAGE_URL = "{{site.url}}{{page.url}}"
    let PAGE_IDENTIFIER = "{{page.url}}"
    var disqus_config = function () {
    this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
    this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
    };

    (function() { // DON'T EDIT BELOW THIS LINE
    var d = document, s = d.createElement('script');
    s.src = 'https://kmu3072.disqus.com/embed.js';
    s.setAttribute('data-timestamp', +new Date());
    (d.head || d.body).appendChild(s);
    })();

</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
```

8. _posts 폴더 내의 블로그 포스트 중 원하는 곳에 다음과 같이 입력
   ```
   ---
   layout : post
   title : 제목
   date : YYYY-MM-DD HH:MM:SS +0900
   categories : jekyll update
   comments : true
   ---
   ```