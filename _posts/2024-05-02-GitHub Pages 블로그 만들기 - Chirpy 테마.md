---
title: GitHub Pages 블로그 만들기 - Chirpy 테마
date: 2024-05-02 15:18:00 +0800
categories: [블로그 만들기]
tags: [ruby, jekyll, GitHub Page]     # TAG names should always be lowercase
toc: true
---

### 들어가기전

어떤 블로그를 할 지 고민하다가 Notion API가 1초당 3회의 요청까지만 가능하다고 해서 이를 CMS로 사용하는 것은 여러 문제가 발생할 것 같았다. 좀 찾아보니 그런 문제에 직면했던 분들도 있어서 너무 어려운 길을 가지 말자라는 생각이 들었다… 

GitHub Page는 포트폴리오 사이트를 만들면서 사용해봐서 알고는 있었지만 ruby와 jekyll은 낯설어서 살짝 걱정이 됐지만.. 다른 분들의 포스팅과 Chirpy 테마 제작자의 repo를 보고 우선 따라해봤다.

> [Chirpy Template - Getting Started](https://chirpy.cotes.page/posts/getting-started/)
{: .prompt-tip }

### 1. Ruby와 Jekyll 설치하기

- Ruby 설치하기
    
    > [Ruby Downloads](https://rubyinstaller.org/downloads/)
    {: .prompt-tip }
    > [Jekyll Installation Guide](https://jekyllrb.com/docs/installation/)
    {: .prompt-tip }
    
    Jekyll Docs를 보면 권장되는 Ruby 버전이 있기 때문에 그 이상만 설치해주면 되는 것 같다. 32비트(x86)로 설치해야된다는 말도 있는데, 나는 64비트(x64)로 설치했지만 잘 적용되었다. **그리고 Devkit이 있는 버전을 설치해주자!**
    
    ![루비 다운로드 페이지](/assets/img/ruby_cap.png){: width="400" }
    _루비 다운로드 페이지_
    
    인스톨이 완료되면 cmd 창이 자동으로 열리는데, 1, 2, 3 모두 실행해주면 된다. 정상적으로 루비가 설치되었다면 루비 버전을 확인할 수 있다.
    
    ```bash
    ruby -v
    ```
    
    ![루비 버전 확인](/assets/img/ruby_version.png){: width="700" }
    _루비 버전 확인_
    
- Jekyll 설치하기
    
    윈도우 검색창에 ruby를 검색하여 Start Command Prompt with Ruby를 실행한다.
    
    ```bash
    gem install jekyll
    ```
    
    설치과정이 끝나면 설치된 jekyll 버전을 확인할 수 있다.
    
    ```bash
    jekyll -v
    ```
    

### 2. 테마로 GitHub Repo 생성 및 지역 저장소 생성하기

나는 골라둔 테마에서 제공하는 문서를 참고해서 진행했다. 테마는 구글 혹은 GitHub에서 Jekyll themes로 검색하면 굉장히 많이 나오기 때문에 맘에 드는 걸 고르기만 하면 된다.

chirpy 테마가 깔끔하고 맘에 들어서 이걸로 진행했다. 

설치방법은 ①chirpy Starter 사용하기 ②GitHub Fork 하기 두가지 중에 선택해야한다. 나는 Jekyll에 대해 무지하기 때문에 보다 글쓰기 용도에 적합한 첫번째 방식을 택했다.

> [https://github.com/cotes2020/jekyll-theme-chirpy](https://github.com/cotes2020/jekyll-theme-chirpy)
{: .prompt-tip }

- chirpy-starter로 GitHub Repo 생성하기
    
    우선 chirpy-starter Repo로 이동해서 use this template을 클릭한다. 그러면 새로운 Repo를 만들수 있고, `[USERNAME.github.io](http://USERNAME.github.io)` 의 username을 본인의 GitHub 이름으로 지정하고 생성한다. 
    
    ![GitHub Repo 생성하기](/assets/img/git_repo.png){: width="700" }
    _깃헙 저장소 생성_
    
    생성된 저장소를 내 컴퓨터의 로컬 저장소로 clone해주면 된다. 나는 Git bash가 아닌 GUI 기반의 소스트리를 사용하고 있어서 소스트리를 이용해서 clone을 받았다.
    
- 지역저장소에 테마 bundle 다운받기
    
    이렇게 클론받은 프로젝트를 VSCode로 열어서 필요한 번들을 다운로드 받는다.
    
    ```bash
    bundle
    ```
    
    번들 다운로드가 완료되면 로컬에서 테마가 잘 적용되었는지 확인할 수 있다.
    
    ```bash
    bundle exec jekyll s
    ```
    
    정상적으로 서버가 켜졌으면 *[http://127.0.0.1:4000](http://127.0.0.1:4000/)* 에서 테마가 잘 적용되었는지 확인해보자
    
    ![vscode 터미널 명령어 입력](/assets/img/vscode_terminal.png){: width="700" }
    _vscode를 통해 로컬서버 실행_
    
    여기까지하면 기본적인 테마 레이아웃은 적용될 것이다.
    

### 3. GitHub Page 설정 후, 첫번째 push하기

GitHub에서 제공하는 무료 배포를 사용하기 위해서는 GitHub Page 설정을 해야한다. 내 저장소로 돌아가서 우선 설정으로 하고 제대로 설정이 되었는지 push를 해보자

- Settings 탭에서 pages를 선택한다. 이때 빌드 설정을 Action 또는 브랜치 기반으로 할 수 있는데, Jekyll 테마를 사용하는 경우에는 Action설정이 yml 파일로 설정이 되어있을 것이다. 그래서 그냥 소스를 GitHub Action으로 설정하면 된다.

![GitHub Repo 액션 설정하기](/assets/img/git_page.png){: width="700" }
_깃헙 저장소 액션 설정_

- Actions 탭 확인하기
    
    나는 다음과 같은 오류가 발생해서 로그대로 platform을 추가해주었다.
    
    - **Add the current platform to the lockfile with `bundle lock --add-platform x86_64-linux` and try again**
        
        ![빌드 확인하기](/assets/img/git_action_error.png){: width="700" }
        _Action 오류_
        
        해당 프로젝트 파일의 cmd를 다시 열어서 아래 명령어를 실행한다. 
        
        ```bash
        bundle lock --add-platform x86_64-linux
        ```
        
        그러고나면 Gemfile.lock 파일의 platform 영역에 방금 추가한 x86_64-linux가 추가된 것을 볼 수 있다.
        
        ![Gemfile.lock 확인하기](/assets/img/gemlock.png){: width="400" }
        _Gemfile 변경사항 확인하기_

        변경사항을 원격에 push 하면 된다.
        
- 배포된 주소로 접속해서 로컬저장소와 동일한 화면이 뜬다면 이제 원격저장소에서도 테마가 적용되어 배포되는 것을 볼 수 있다.


이제 기초적인 설정은 끝났지만 _config.yml을 내 정보에 맞게 수정하고 조금씩 커스텀하려고 한다.. ㅎㅎ
우선은 SEO 설정을 하고나서 댓글 기능추가 등을 해봐야겠다~ 