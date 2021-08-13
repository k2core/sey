---
layout: page
title: "GitHub Pages 사용 가이드"
description: "하나의 계정으로 여러 프로젝트를 호스팅할 수 있다."
date: 2021-08-13 13:15:32 +0900
background: "/assets/img/posts/strawberries.jpeg"
---

[A guide to using GitHub Pages](https://www.thinkful.com/learn/a-guide-to-using-github-pages/) 사이트를 정래해보자.

**_github pages_**는 크게 두 가지 방식이다:

- User Pages
- Project Pages

각각 알아보자.

<br>

---

## 🍏 User Pages

개인 웹사이트 또는 프로젝트 포트폴리오를 호스팅하는 경우 이 페이지를 사용하자.
**_GitHub_ 계정에는 하나의 user page만 연결할 수 있다.**
이 페이지의 URL은 `http://GitHub-ID.github.io/` 이다.

(추후 보강)

혹시, 리포지토리 이름에 `GitHub-ID.github.io`를 입력하고, 나머지는 아래와 동일?

<br>

---

## 🫐 Project Pages

여러 프로젝트를 호스팅해야 하는 경우 project page를 사용하자.
계정당 여러 프로젝트 페이지를 만들 수 있다.
이 페이지의 URL은 `http://GitHub-ID.github.io/projectname/` 이다.

### #. 새 저장소 생성, github.com/new로 이동

1. Repository name에 **_projectName_**을 입력
2. 저장소를 **_Public_**으로 설정<br>
   *Private*은 제한이 있다. [(GitHub 정책)](https://github.com/pricing)
3. *"Initialize this repository with:"*의 선택 항목은 3가지(_"Add a README file", "Add .gitignore", "Choose a license"_)가 있다.<br>
   기존 저장소를 가져오는 경우 3개 모두 선택하지 않는다.
4. 클릭 **_"Create repository"_**

<br>

---

## 🍹 준비된 프로젝트를 리모트에 push 하기

로컬 브랜치명이 `gh-pages`가 아니라면 브랜치명을 변경하고:

```
$ git checkout -b gh-pages
```

리모트를 설정하고 push 하자:

```
$ git remote add origin https://github.com/GitHub-ID/프로젝트명.git
$ git push -u origin gh-pages
```
