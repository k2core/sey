---
layout: page
title: GitHub Pages에 호스팅 하기
description: "예뻐야 쓰고 싶다. Jekyll에 Clean Blog 테마를 적용하자."
date: 2021-08-13 13:10:37 +0900
background: "/assets/img/posts/strawberries2.jpeg"
---

Clean Blog 테마를 Jekyll에 적용하고, GitHub Pages로 호스팅 하는 환경을 만들어 본다.

- [Clean Blog 테마](https://github.com/StartBootstrap/startbootstrap-clean-blog-jekyll)
- [Jekyll](https://jekyllrb.com/)
- [Jekyll 한글 문서](https://jekyllrb-ko.github.io/docs/)
- [GitHub Pages](https://pages.github.com/)

<br>

---

## 🍫 Clean Blog 테마의 Jekyll 프로젝트 다운 받기

[Clean Blog 테마](https://github.com/StartBootstrap/startbootstrap-clean-blog-jekyll) 사이트 요약 정리이다.

위 사이트에는 2가지 _Using RubyGems, Using Core Files_ 테마 설치 방법이 나온다.
**_Using Core Files_** 방법으로 진행해보자.
(이유는 Jekyll 테마 중 [GitHub Pages가 지원하는 테마](https://pages.github.com/themes/)는 제한적이다.
미지원 테마를 사용하기 위해서는 테마의 파일들을 풀어서 올리는 방법이라 생각해 봤다. _이 가설이 맞는지는 아직 모른다._)

1. 이미 구성된 압축 파일을 다운 받는다.<br>
   위 사이트 _Using Core Files_ 영역의 **_"Download"_** 또는 여기서([**`.zip`**](https://github.com/StartBootstrap/startbootstrap-clean-blog-jekyll/archive/master.zip))
   다운 하자.
2. 블로그를 생생할 위치에 압축을 푼다.
3. 디렉토리명을 사용할 프로젝트명으로 바꾼다.
4. 계속해서 `_config.yml` 파일의 항목을 수정한다.
   - `baseurl`: 슬래시(/)로 시작한다.
     프로젝트명, GitHub Pages URL(\*https://GitHub-ID.github.io/**프로젝트명***)에서 사용된다.
   - `url`: 아직 필요 여부를 모르겠다. 혹시 페이지에서 변수로 읽어 올 수도 있을 듯하다.
     필요하다면, _"https:GitHub-ID.github.io/"_ 또는 _"https:GitHub-ID.github.io/프로젝트명"_ (보강 필요)
   - `title`: 홈페이지의 이름이 된다.
   - `email`: 이메일
   - `description`: 해당 내용을 사이트에 표시할 수 있다.
   - `author`: 작성자
   - (Optional) `twitter_username`, `facebook_username`, `github-username`, `linkedin_username`, `instagram_username`

<br>

## 🌭 Git 초기화

### #. git 초기화 전에 `.gitignore` 파일 먼저 설정하자.

git이 관리할 필요없는 파일을 먼저 설정하는 것이 편하다.
다운로드 받은 파일과 Jekyll에서 생성한 파일을 참조하여 "최종" 버전으로 만들자.

- (변경 전) Clean Blog .zip 파일의 `.gitignore` 파일

  ```
  _site
  .sass-cache
  node_modules
  Gemfile.lock
  *.gem
  ```

- (변경 후) $ jekyll new 생성 후 `.gitignore` 파일

  ```
  _site
  .sass-cache
  .jekyll-cache
  .jekyll-metadata
  vendor
  ```

- **(최종) 위의 (변경 후)를 리모트에 push하면 에러가 난다. 다음과 같이 하자.**

  ```
  _site/
  .sass-cache/
  .jekyll-cache/
  .jekyll-metadata
  ```

> (변경 후)의 `.gitignore`를 리모트에 push하면 GitHub에서 빌드 시 실패한다.
> <br>GitHub에서 "[GitHub-ID/리파지토리명] Page build failure" 제목으로 메일이 왔다.
> <br>내용은,
> <br>Your SCSS file 'assets/main.scss' has an error on line 2: File to import not found or unreadable: ../assets/vendor/startbootstrap-clean-blog/scss/styles.scss. Load paths: \_sass /hoosegow/.bundle/ruby/2.7.0/gems/jekyll-theme-primer-0.6.0/\_sass /hoosegow/.bundle/ruby/2.7.0/gems/jekyll-theme-primer-0.6.0/\_sass.
> <br>🍭 **관련 파일이 없어서다.** 그 이유는 아래를 보자.

<br>

> <strong style="background-color: crimson; color: white; padding: 0 5px">⚠️ .gitignore 설정 시 주의 사항</strong>
>
> > (변경 후)에서와 같이 'vender'라고 쓰면 모든 위치에서 'vender'를 찾는다.
> > <br>Clean Blog 테마에는 /assets 하위에 vender 디렉토리가 있는데, 그것이 commit 되지 않아 파일이 없게 되었다(빌드 실패).
> > <br>명확하게 '/vender'이라고 하면 현 디렉토리 바로 하위 디렉토리만 무시한다.
> > <br>또한, 끝에 슬래시(/)를 붙이면 그 디렉토리에 있는 모든 파일을 무시한다.
> > <br>결국 '\_site' 보다는 해당 디렉토리에 있는 모든 파일을 의미하는 '\_site/'가 낫고,
> > <br>엄격하게 바로 하위 디렉토리만 무시하게 하려면 '/\_site/'가 낫다.

> `.gitignore` 작성 시 참조 사이트 <https://github.com/github/gitignore>

<br>
### #. 그리고, **git 초기화**를 하자.

```
$ git init
```

또는,

해당 프로젝트가 GitHub Pages 호스팅용이므로 **GitHub Pages에서 특정하는 브랜치명인 `gh-pages`**를 바로 사용할 수 있다.

```
$ git init --initial-branch=gh-pages
```

> **_git_**에서 기본 사용하는 브랜치명 `master`는 관례적인 사용일뿐 별다른 의미나 권한이 있는 것은 아니다. 즉, 일반적인 브랜치명 중 하나일 뿐이다.

<br>

## 🍞 서버 테스트 기동

`webrick`을 먼저 설치하고, 검증을 위해 서버를 기동해보자.

```
$ bundle add webrick
$ bundle exec jekyll serve
```

<br>

## 🍔 GitHub에 올리자

GitHub에서 프로젝트를 설정한다. 참조: [GitHub Pages 사용 가이드](./github-pages-guide.html)

### #. 이미 존재하는 프로젝트를 git에 어떻게 설정하는지 보자.

GitHub Pages에 올리기 위해서는 `gh-pages`라는 특정 브랜치명을 사용해야 한다.

- (방법#1) 그냥 **git init**을 했다면 브랜치명을 변경해야 한다.

  ```
  $ git init
  $ git branch -m gh-pages
  -m은 --move이며 rename이다.
  ```

- (방법#2) 초기화부터 브랜치명으로 `gh-pages`를 사용한다.

  ```
  $ git init --initial-branch=gh-pages
  ```

- (방법#3) **git init**해서 열심히 썼다면,
  ```
  $ git checkout -b gh-pages
  -b 옵션은 다음 두 줄의 명령어와 같다!
    $ git branch gh-pages
    $ git checkout gh-pages
  ```

<br>
### #. 원격 저장소인 GitHub에 push 한다.

위와 같이 `gh-pages` 브랜치명을 가진 프로젝트가 준비되었다면, 그 다음은 리모트를 설정하고 `push` 하자

```
$ git remote add origin https://github.com/GitHub-ID/프로젝트명.git
$ git push -u origin gh-pages
```

> `origin`은 리모트 즉 원격 저장소에 사용하는 관례적인 이름이다. 원하는 이름을 써도 된다.

<br>
## 🥯 여러 로컬에서 블로그 관리하기

### #. 또 다른 로컬에서의 사용법(로컬 2대 이상 사용 시)

프로젝트를 `clone` 하고 jekyll을 실행하면 된다.

```
$ git clone https://github.com/GitHub-ID/프로젝트명.git
$ cd 프로젝트명
$ bundle exec jekyll serve
```

`bundle`에서 아래와 같은 오류가 발생한다.

```
Could not find jekyll-paginate-1.1.0, jekyll-sitemap-1.4.0 in any of the sources
Run `bundle install` to install missing gems.
```

위 메시지대로 gem을 설치하기 위해 최초 한 번 `bundle install`을 실행해야 한다.

```
$ bundle install
```

<br>
### #. 여러 로컬에서 블로그 기록하기

다른 로컬에서의 변경 사항이 리모트에 반영되어 있을 수 있으니 먼저 받아온다.

```
$ git pull
```

그리고, 현재 로컬에서 기록한(변경된) 블로그를 `commit`하고 `push`하면 된다.

```
$ git push
```
