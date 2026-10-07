## 📌 목차
1. 전체 흐름 한눈에 보기
2. git config: 사용자 설정
3. git init/git clone: 저장소 만들기
4. git status: 상태 확인
5. git status: 스테이징
6. git commit: 기록 저장
7. git push: 원격 저장소로 올리기
8. git pull:원격 저장소에서 받아오기
9. 더 알아두면 좋은 명령어 (log, show, diff)
10. 되돌리기 (reset, amend, checkout)
11. 명령어 요약표

## 1. 전체 흐름 한눈에 보기

```
 Working Directory ──git add──▶ Staging Area ──git commit──▶ Local Repository ──git push──▶ Remote Repository
   (작업 중인 파일)              (커밋 대기)                    (내 컴퓨터의 기록)                 (GitHub)
                                                                    ◀───────────git pull────────────
```

|영역|설명|
|---|---|
|Working Directory|실제로 파일을 만들고 고치는 작업 폴더|
|Staging Area|다음 커밋에 포함할 파일을 모아 두는 대기 공간|
|Local Repository|커밋 기록이 저장되는 내 컴퓨터의 저장소(.git 폴더)|
|Remote Repository|GitHub처럼 인터넷에 있는 저장소|

## 2. git config: 사용자 설정
커밋에는 **누가 작성했는지**가 함께 기록된다. 그래서 처음 Git을 쓸 때 이름과 이메일을 등록해야 한다.

|명령어|설명|
|---|---|
|git config user.name "이름"|작성자 이름 설정(현재 저장소에만 적용)|
|git config user.email "이메일"|작성자 이메일 설정(현재 저장소에만 적용)|
|git config --global user.name "이름"|내 컴퓨터의 **모든 저장소**에 적용|
|git config --list|설정된 내용 전체 보기|
|git config --get user.name|특정 설정 값만 보기|
|git help config|명령어 도움말 보기|

```bash
git config --global user.name "having-all"       # 이름 설정
git config --global user.email "me@example.com"  # 이메일 설정
git config --list                                # 설정확인
git config -- get user.name                      # 이름만 확인
```
💡 --global을 붙이면 컴퓨터 전체에 한 번만 설정하면 된다. 붙이지 않으면 그 저장소에만 적용된다. 이메일은 GitHub 가입 이메일과 같아야 GitHub에서 commit이 내 계정과 연결된다.

## 3. git init/ git clone: Repository(저장소) 만들기
- git init: 새 저장소 만들기
    현재 폴더를 Git 저장소로 만든다. 폴더 안에 숨김 폴더 .git이 생기고, 여기에 모든 기록이 저장된다.
    - 사용 시점: 내 컴퓨터에서 새 프로젝트를 Git으로 관리하기 시작할 때
```bash
mkdir new_project     # 새 폴더 만들기
cd new_project        # 폴더로 이동
git init              # Git 저장소로 초기화
```

- git clone: 기존 저장소 복제하기
    GitHub에 있는 저장소를 통째로 내 컴퓨터로 복사한다. 원격 저장소는 자동으로 origin이라는 이름으로 연결된다.
    - 사용 시점: GitHub에 이미 있는 프로젝트를 가져올 때
```bash
git clone https://github.com/having-all/OZ_school.git
```
## 4. git status: 상태 확인
저장소의 현재 상태를 보여준다. **명령어를 입력하기 전후로 습관처럼 확인**하면 실수를 크게 줄일 수 있다.
```bash
git status       # 자세히 보기
git status -s    # 짧게 보기
```

git status -s 결과 기호
|기호|의미|
|---|---|
|??|Untracked: Git이 아직 추적하지 않는 새 파일|
|A|Added: 스테이징된 새 파일|
|M (오른쪽)|Modified: 수정했지만 아직 add 안 함|
|M  (왼쪽)|Modified: 수정 후 add까지 함|
|D|Deleted: 삭제된 파일|

## 5. git add: Staging
수정한 파일을 Staging Area에 올려 다음 commit에 포함시킨다.

|명령어|설명|
|---|---|
|git add 파일이름|특정 파일만 staging|
|git add 폴더이름|해당 폴더 안의 변경 파일 모두 staging|
|git add .|현재 폴더와 하위 폴더의 **모든 변경 파일** staging(새파일 포함)|
```bash
git add index.html    # 파일 하나만
git add src/          # src 폴더 전체
git add .             # 전부
```
💡 git add .는 새로 만든(untracked) 파일도 포함한다. 올리면 안 되는 파일(비밀번호, 용량이 큰 데이터 등)은 .gitignore 파일에 적어 두면 add에서 제외된다.


## 6. git commit : 기록 저장

Staging Area에 있는 변경 사항을 **하나의 기록(스냅샷)으로 저장**한다.

| 명령어 | 설명 |
|---|---|
| `git commit` | 에디터가 열리고, 거기서 메시지를 작성 |
| `git commit -m "메시지"` | 에디터 없이 바로 메시지 입력 |
| `git commit -am "메시지"` | add + commit을 한 번에 (단, **이미 추적 중인 파일만**) |

```bash
git commit -m "Fix bug in login feature"
git commit -am "Update README and fix typos"
```

> ⚠️ `-am`은 한 번이라도 커밋된 적 있는 파일에만 적용된다. 새로 만든 파일은 먼저 `git add` 해야 한다.

### 좋은 커밋 메시지
| ❌ 나쁜 예 | ✅ 좋은 예 |
|---|---|
| `수정` | `Fix login error when password is empty` |
| `최종` | `Add sign_up function` |

---

## 7. git push : 원격 저장소로 올리기

내 컴퓨터(Local)의 커밋을 GitHub(Remote)로 업로드한다.

```bash
git push                     # 현재 브랜치를 연결된 원격 브랜치로 올리기
git push origin main         # origin 저장소의 main 브랜치로 올리기
git push -u origin main      # 처음 올릴 때: 연결(-u)까지 설정, 다음부턴 git push만 해도 됨
```

| 용어 | 뜻 |
|---|---|
| `origin` | 원격 저장소의 기본 이름 (clone하면 자동으로 붙음) |
| `main` | 올릴 브랜치 이름 |
| `-u` | 지금 브랜치와 원격 브랜치를 연결해서 기억 (upstream 설정) |

> ⚠️ push가 거절(rejected)되면 GitHub에 내 컴퓨터에 없는 새 커밋이 있다는 뜻이다. 먼저 `git pull`로 받아온 뒤 다시 push한다.

---

## 8. git pull : 원격 저장소에서 받아오기

GitHub의 최신 변경 사항을 내 컴퓨터로 가져와서 합친다.

```bash
git pull                  # 연결된 원격 브랜치에서 받아와 합치기
git pull origin main      # origin의 main 브랜치에서 받아오기
```

> 💡 `git pull` = `git fetch`(받아오기) + `git merge`(합치기)
> 협업할 때는 **작업 시작 전에 pull, 작업 끝나면 push** 하는 습관을 들이자.

---

## 9. 더 알아두면 좋은 명령어

### git log : 커밋 기록 보기

| 명령어 | 설명 |
|---|---|
| `git log` | 커밋 기록 전체 (해시, 작성자, 날짜, 메시지) |
| `git log --oneline` | 한 줄씩 짧게 (짧은 해시 + 메시지) |
| `git log --pretty=oneline` | 한 줄씩 (전체 해시 + 메시지) |
| `git log --graph --oneline` | 브랜치 흐름을 그래프로 |
| `git log --decorate=full` | 브랜치·태그 정보까지 자세히 |

```bash
git log --oneline
git log --graph --oneline
```

### git show : 커밋 내용 자세히 보기

| 명령어 | 설명 |
|---|---|
| `git show` | 가장 최근 커밋의 정보와 변경 내용 |
| `git show 커밋해시` | 특정 커밋의 정보 |
| `git show HEAD` | 현재 위치(HEAD)의 커밋 |
| `git show HEAD^` | 1단계 전 커밋 (`^^^`이면 3단계 전) |
| `git show HEAD~3` | 3단계 전 커밋 |

> 💡 **HEAD** = "내가 지금 보고 있는 위치". 보통 현재 브랜치의 가장 최근 커밋을 가리킨다.

### git diff : 변경 내용 비교

| 명령어 | 비교 대상 |
|---|---|
| `git diff` | 작업 폴더 ↔ Staging Area (아직 add 안 한 변경) |
| `git diff --staged` | Staging Area ↔ 최근 커밋 (add했지만 커밋 안 한 변경) |
| `git diff 해시1 해시2` | 두 커밋 사이 |

```bash
git diff
git diff --staged
git diff abc123 def456
```

---

## 10. 되돌리기

### 스테이징 취소

```bash
git reset               # 스테이징된 파일 전체를 add 이전으로 (수정 내용은 유지)
git reset example.txt   # 특정 파일만 add 취소
git restore --staged example.txt   # 위와 같은 기능 (최신 방식)
```

### 최근 커밋 수정 : amend

```bash
git commit --amend                       # 최근 커밋 내용·메시지 수정 (에디터 열림)
git commit --amend -m "수정된 커밋 메시지"   # 메시지만 바로 수정
```

> ⚠️ 이미 push한 커밋은 amend하지 말자. GitHub 기록과 내 기록이 달라져 충돌이 생긴다.

### 커밋 되돌리기 : reset

| 명령어 | 커밋 기록 | Staging Area | 작업 폴더(파일 내용) |
|---|---|---|---|
| `git reset --soft 해시` | 되돌림 | **유지** | **유지** |
| `git reset 해시` (= `--mixed`, 기본값) | 되돌림 | 비움 | **유지** |
| `git reset --hard 해시` | 되돌림 | 비움 | **삭제** ⚠️ |

```bash
git reset --soft HEAD^     # 직전 커밋만 취소, 변경 내용은 add된 상태로 남음
git reset HEAD~3           # 3단계 전으로, 변경 내용은 파일에 남음
git reset --hard abcd1234  # 해당 커밋 상태로 완전히 되돌림 (이후 변경 모두 삭제)
```

> ⚠️ `--hard`는 수정 내용이 사라지므로 정말 필요할 때만 쓴다.

### 과거 커밋 둘러보기 : checkout

```bash
git checkout abcd1234   # 해당 커밋 시점으로 이동해서 살펴보기
git checkout HEAD~2     # 2단계 전 커밋으로 이동
git checkout -          # 직전 위치로 돌아가기
git checkout main       # main 브랜치로 돌아오기
```

> 💡 커밋 해시로 이동하면 **detached HEAD(분리된 HEAD)** 상태가 된다. 브랜치에서 떨어져 과거를 구경하는 상태라서, 여기서 만든 커밋은 브랜치를 만들지 않으면 사라질 수 있다. 다 봤으면 `git checkout main`으로 돌아오자.

---

## 11. 명령어 요약표

| 분류 | 명령어 | 한 줄 설명 |
|---|---|---|
| 설정 | `git config` | 이름·이메일 등 설정 |
| 시작 | `git init` | 새 저장소 만들기 |
| 시작 | `git clone 주소` | GitHub 저장소 복제 |
| 확인 | `git status` | 현재 상태 보기 |
| 확인 | `git log --oneline` | 커밋 기록 보기 |
| 확인 | `git diff` | 변경 내용 비교 |
| 저장 | `git add` | Staging Area에 올리기 |
| 저장 | `git commit -m ""` | 기록으로 저장 |
| 공유 | `git push` | GitHub로 올리기 |
| 공유 | `git pull` | GitHub에서 받아오기 |
| 취소 | `git reset` | 스테이징·커밋 되돌리기 |
| 취소 | `git commit --amend` | 최근 커밋 수정 |
