---
layout: page
title: "git checkout 대신 switch 사용"
date: 2021-08-26 09:54:14 +0900
background: "/assets/img/posts/cheers.jpg"
---

`master` 브랜치의 이전 커밋에서 새 브랜치를 만들어 개선을 하고자 할 때,
`checkout`을 **"commit hash 값"**으로 하면되나? 라고 궁금했다.

즉, *"c1 -> c2 -> c3(HEAD -> master)"*에서
`c2` 커밋을 `hotfix` 브랜치로 만들기가 가능하겠지? 그래서:

```
  $ git checkout -b hotfix "c2의 commit hash 값"
```

추가로 **브랜치명을 사용하지 않고** `checkout`하면 `HEAD`의 위치만 변경된다:

```
  $ git checkout "c2의 commit hash 값"

  $ git log --oneline --graph --all
  * 9a4aeff (master) c3: ...
  * af18342 (HEAD) c2: ...
  * 7bdf3a9 c1: ...
  # 'HEAD'가 변경된 것을 확인할 수 있다.
```

`"detached HEAD"`라고 한다. "분리된 HEAD". 정확한 명령어는 `-d`나 `--detach` 옵션을 붙인다. 또한 `switch`도 가능하다:

```
  $ git checkout -d "commit hash 값"

  # 'checkout'에서는 '-d' 옵션이 선택사항이지만, 'switch'에서는 필수다.
  $ git switch -d "commit hash 값"

  # HEAD가 있는 이 지점에서 hotfix 브랜치를 만들려면:
  $ git switch -c hotfix
  또는 두 명령어로:
  $ git branch hotfix
  $ git switch hotfix

  # 추가로 위의 'branch'와 'switch' 명령 사이에
  # 'git log'로 확인해보면 그 표시 방법의 차이를 알 수 있다:
  $ git log --oneline --graph --all
  ... (생략)
  * af18342 (HEAD, hotfix) c2: ...  <- 'branch' 명령만 했을 때
  * af18342 (HEAD -> hotfix) c2: ...  <- 'switch' 명령까지 했을 때
```

<br>

> 👉 `checkout` 대신 최신 버전의 `switch`를 사용하자!

<br>

##### 참고 URL:

- [새 버전에 맞게 git checkout 대신 switch/restore 사용하기(2020-10-21)](https://blog.outsider.ne.kr/1505)
- [git switch branch – Easily checkout git branches with this new command(2019-09-23)](https://bluecast.tech/blog/git-switch-branch/)

<div class="alert alert-warning" role="alert">
  <span class="badge rounded-pill bg-warning text-dark">Version</span>
  <code>switch</code>, <code>restore</code>는 <a href="https://github.com/git/git/blob/master/Documentation/RelNotes/2.23.0.txt" class="alert-warning">git 2.23.0</a>의 새 명령어이다.
</div>

<br>

---

### 🥔 git switch

`switch`는 `checkout`에서 브랜치를 변경하는 부분만 담당한다.

##### #. `git switch 브랜치명`으로 브랜치를 전환한다:

```
  $ git switch 브랜치명
```

<br>

##### #. 브랜치를 새로 만들어 전환하려면, `checkout`의 `-b` 옵션 처럼 `-c`를 사용한다:

```
  $ git switch -c 새브랜치명
```

<br>

##### #. 특정 `commit hash`에서 브랜치를 만들려면:

```
  $ git switch -c 새브랜치명 커밋해시값

  ex) $ git switch -c hotfix ec0a1fe
```

<br>

##### #. 브랜치 전환에 `'cd -'` 처럼 `'switch -'`로 이전 브랜치로 토글할 수 있다:

```
  $ git switch -

  ex) 이를테면, 'hotfix'와 'master'를 번갈아 전환한다.
```

<br>

#### 실습#1 (checkout -b 새브랜치)

상황을 만들어서 알아보자.

```
  $ mkdir ex01
  $ cd ex01
  $ git init

  $ echo '1' > file1.txt
  $ git add file1.txt
  $ git commit -m 'c1: file1 add'

  $ echo '2' > file2.txt
  $ git add file2.txt
  $ git commit -m 'c2: file2 add'

  $ echo '3' > file3.txt
  $ git add file3.txt
  $ git commit -m 'c3: file3 add'

  # 커밋해시값 확인
  $ git log --oneline

  $ git checkout -b hotfix 커밋해시값(c2의)
  $ git log --oneline --graph --all
  * 73c56c3 (master) c3: file3 add
  * b916c0f (HEAD -> hotfix) c2: file2 add
  * 4dc747a c1: file1 add

  $ echo '4' > file4.txt
  $ git add file4.txt
  $ git commit -m 'c4: file4 add'
  $ git log --oneline --graph --all
  * ec0a1fe (HEAD -> hotfix) c4: file4 add
  | * 73c56c3 (master) c3: file3 add
  |/
  * b916c0f c2: file2 add
  * 4dc747a c1: file1 add

  $ git checkout master
  # 아래 명령에서 커밋 메시지는 "c5: Merge branch 'hotfix'"으로 입력한다.
  $ git merge hotfix
  $ git log --oneline --graph --all
  *   b9c9a79 (HEAD -> master) c5: Merge branch 'hotfix'
  |\
  | * ec0a1fe (hotfix) c4: file4 add
  * | 73c56c3 c3: file3 add
  |/
  * b916c0f c2: file2 add
  * 4dc747a c1: file1 add
```

<br>

#### 실습#2 (switch -c 새브랜치)

**실습#1**을 `git switch`로 대체해보자.

```
  $ mkdir ex02
  $ cd ex02
  $ git init

  # 파일 3개를 만들어 커밋하고 커밋해시값 확인까지는 위 "실습#1"과 동일하게 한다.

  $ git switch -c hotfix 커밋해시값(c2의)
  $ git log --oneline --graph --all
  * 8350d34 (master) c3: file3 add
  * 82f77e2 (HEAD -> hotfix) c2: file2 add
  * 38856c0 c1: file1 add

  $ echo '4' > file4.txt
  $ git add file4.txt
  $ git commit -m 'c4: file4 add'
  $ git log --oneline --graph --all
  * bba4254 (HEAD -> hotfix) c4: file4 add
  | * 8350d34 (master) c3: file3 add
  |/
  * 82f77e2 c2: file2 add
  * 38856c0 c1: file1 add

  $ git switch -
  또는, $ git switch master
  # 아래 명령에서 커밋 메시지는 "c5: Merge branch 'hotfix'"으로 입력한다.
  $ git merge hotfix
  $ git log --oneline --graph --all
  *   a8d64d0 (HEAD -> master) c5: Merge branch 'hotfix'
  |\
  | * bba4254 (hotfix) c4: file4 add
  * | 8350d34 c3: file3 add
  |/
  * 82f77e2 c2: file2 add
  * 38856c0 c1: file1 add
```

<br>

---

### 🍠 git restore

`restore`는 워킹 디렉토리의 파일을 복원해 준다.\
**⚠️ 주의: 워킹 디렉토리에 수정한 파일 내용은 덮어져 사라진다.**

<br>

##### #. 워킹 디렉토리의 파일을 되돌리고 싶다면, `git restore`를 사용한다:

```
  $ git restore 파일
```

바로 앞 단계에서 복원한다.\
즉, **스테이징 영역**에 파일이 있으면 그 파일로, 없으면 **저장소** 파일로\
**워킹 디렉토리** 파일을 덮어쓴다. (🚨 각주 참조)\
**⚠️ 덮어쓰기 때문에, 워킹 디렉토리에 수정하고 있던 내용이 사라진다. 주의하자!**

<br>

##### #. 스테이징 영역에 추가한 파일을 취소하고 싶다면, `git restore --staged`를 사용한다:

```
  $ git restore --staged 파일
```

단지, 스테이징 영역의 파일만 삭제된다. (🚨 각주 참조)

즉, 저장소(버전1)의 파일을 수정하여 스테이징 영역(버전2)에 추가한 후,\
워킹 디렉토리에서 다시 수정한 상태(버전3)이지만 마음에 들지 않아서 저장소(버전1) 내용으로 만들고 싶다면
`--staged` 옵션을 사용하여 스테이징 영역의 파일을 삭제해야 가능하다: (🚨)

```
  $ git status -s
  MM 파일

  $ git restore --staged 파일
  $ git restore 파일
```

<br>

<div class="alert alert-danger" role="alert">
  <h4>🚨 (각주)스테이징 영역 "삭제" 의미?</h4>
  <ul><em>
    1. '스테이징 영역에 <strong>파일이 없으면</strong>'<br>
    2. '스테이징 영역의 파일만 <strong>삭제</strong>된다'<br>
    3. '스테이징 영역의 파일을 <strong>삭제</strong>해야 가능하다'
  </em></ul>
  <p>
    "삭제"라는 표현을 사용하고 있지만, 엄밀히 말하면 저장소의 내용과 스테이징 영역의 내용이 같은 상황을 말한다.
    이 상황으로 위의 1~3번을 다시 설명해보면,
  </p>
  <ul>
    [명령어#1] <strong>'git restore'</strong>는 스테이징 영역의 내용을 워킹 디렉토리에 덮어쓴다.<br>
    [명령어#2] <strong>'git restore --staged'</strong>는 저장소 내용을 스테이징 영역에 덮어쓴다.<br>
    <br>
    <strong><del>"--staged"</del> 옵션 없이,</strong><br>
    <strong>"저장소(버전1):스테이징(버전2):워킹(버전3)" 일때,</strong><br>
    '--staged' 옵션이 없으면 스테이징(버전2) 내용으로 워킹(버전3을 버전2로)을 덮어쓴다.
    이부분을 "스테이징 영역에 파일이 있으면"으로 기록했다. 정확히는 저장소와 스테이징 내용이 달라서이다.<br>
    <br>
    <strong><del>"--staged"</del> 옵션 없이,</strong><br>
    <strong>"저장소(버전1):스테이징(버전1):워킹(버전2)"일때,</strong><br>
    '--staged' 옵션이 없으면 스테이징(버전1) 내용으로 워킹(버전2을 버전1로)을 덮어쓴다.
    이부분은 "파일이 없으면"으로 기록했다. 실질적으로는 저장소와 스테이징 내용이 같아서
    마치 "스테이징에 파일이 없다"라고 생각할 수 있다.<br>
    다시 한번 상기하자. '--staged' 옵션이 없으면 저장소는 아무 상관없고,
    "스테이징 영역의 내용을 워킹 디렉토리에 덮어쓴다."<br>
    <br>
    <strong>"--staged" 옵션 있고,</strong><br>
    <strong>"저장소(버전1):스테이징(버전2):워킹(버전 상관 없음)" 일때,</strong><br>
    '--staged' 옵션은 저장소(버전1) 내용으로 스테이징(버전2를 버전1로)을 덮어쓴다.
    이부분을 "스테이징 영역의 파일만 삭제된다."로 기록했다.
    정확히는 삭제가 아니고 단지 저장소의 내용을 스테이징 영역에 덮어쓴다.<br>
  </ul>
  <hr>
  <br>
  🌟 <strong>스테이징 영역은 삭제되는 것이 아니다.
    각 명령어를 실행할 때 마치 저장소의 내용을 가져오는 것처럼 보일때,
    "스테이징이 삭제되었다. 없다."라고 생각할 수 있지만,
    그것은 저장소의 내용과 스테이징 영역의 내용이 동일한 것이다.</strong>
</div>
