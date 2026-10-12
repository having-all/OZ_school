# 3. Branch

## 📌 목차
1. [브랜치란?](#1-브랜치란)
2. [git branch 명령어](#2-git-branch-명령어)
3. [브랜치 관리 전략 (main, develop, feature, hotfix, release)](#3-브랜치-관리-전략)
4. [Merge 방식 1 : Fast-forward](#4-merge-방식-1--fast-forward)
5. [Merge 방식 2 : 3-way merge](#5-merge-방식-2--3-way-merge)
6. [Merge 옵션 (--ff, --no-ff, --squash)](#6-merge-옵션)
7. [Merge conflict (충돌)](#7-merge-conflict-충돌)
8. [더 알아두면 좋은 명령어 (rebase, cherry-pick)](#8-더-알아두면-좋은-명령어)
9. [명령어 요약표](#9-명령어-요약표)

---

## 1. 브랜치란?

**원본을 건드리지 않고 독립적으로 작업할 수 있는 갈래.** 평행 세계를 하나 만들어 실험하는 것과 같다.

```
main      A───B───────────E
               \         /
feature         C───────D
```

- 브랜치는 사실 **특정 커밋을 가리키는 이름표(포인터)** 다.
- 새 커밋을 만들면 이름표가 새 커밋으로 한 칸 이동한다.
- **HEAD**는 "지금 내가 있는 브랜치"를 가리킨다.

---

## 2. git branch 명령어

### 만들기 · 보기 · 이동하기

| 명령어 | 설명 |
|---|---|
| `git branch` | 브랜치 목록 (`*` 표시가 현재 브랜치) |
| `git branch 이름` | 새 브랜치 만들기 (이동은 안 함) |
| `git switch 이름` | 브랜치 이동 (최신 방식) |
| `git switch -c 이름` | 만들면서 바로 이동 (최신 방식) |
| `git checkout 이름` | 브랜치 이동 (예전 방식) |
| `git checkout -b 이름` | 만들면서 바로 이동 (예전 방식) |

```bash
git branch                    # 목록 보기
git branch new-feature        # 만들기만
git switch new-feature        # 이동
git switch -c new-feature     # 만들면서 이동 (= git checkout -b new-feature)
```

> 💡 `checkout`은 기능이 너무 많아서 헷갈리기 쉽다. Git 2.23부터 브랜치 이동은 `switch`, 파일 되돌리기는 `restore`로 나뉘었다. 둘 다 동작하니 편한 걸 쓰면 된다.

### 이름 바꾸기 · 삭제하기

| 명령어 | 설명 |
|---|---|
| `git branch -m 새이름` | 현재 브랜치 이름 바꾸기 |
| `git branch -m 옛이름 새이름` | 다른 브랜치 이름 바꾸기 |
| `git branch -d 이름` | 브랜치 삭제 (병합된 브랜치만 가능) |
| `git branch -D 이름` | 병합 안 된 브랜치도 강제 삭제 ⚠️ |

```bash
git branch -m old-feature new-feature
git branch -d old-feature
```

### ⚠️ 브랜치 이동이 안 될 때

```
error: Your local changes to the following files would be overwritten by checkout
```

커밋하지 않은 수정이 있는 상태에서 이동하려 할 때 생기는 오류다.

| 상황 | 해결 |
|---|---|
| 수정 내용을 저장하고 싶다 | `git add .` → `git commit -m "..."` → `git switch main` |
| 잠깐 보관하고 싶다 | `git stash` → `git switch main` → (돌아와서) `git stash pop` |
| 버려도 된다 | `git restore 파일명` → `git switch main` ⚠️ 되돌릴 수 없음 |

---

## 3. 브랜치 관리 전략

여러 사람이 함께 개발할 때 **브랜치마다 역할을 정해 두는 규칙**이다. 대표적인 방식이 **Git Flow**다.

| 브랜치 | 역할 | 만드는 곳 → 합치는 곳 | 수명 |
|---|---|---|---|
| **main** | 실제 서비스(배포)되는 안정된 코드 | - | 계속 유지 |
| **develop** | 다음 배포를 준비하며 기능을 모으는 곳 | main → - | 계속 유지 |
| **feature** | 새 기능 하나를 개발 | develop → develop | 기능 완성 후 삭제 |
| **release** | 배포 직전 최종 점검, 버그 수정 | develop → main + develop | 배포 후 삭제 |
| **hotfix** | 배포된 서비스의 급한 버그 수정 | main → main + develop | 수정 후 삭제 |

```
main     ●─────────────────────●──────────●───▶   (v1.0)     (v1.0.1)
          \                   /          / \
hotfix     \                 /          ●───\──────────▶ (긴급 수정)
            \               /                \
release      \         ●───●                  \
              \       /     \                  \
develop        ●───●─●───────●──────────────────●───▶
                \     /
feature          ●───●     (로그인 기능)
```

### 브랜치 이름 규칙 예시

```bash
git switch -c feature/login        # 기능: feature/기능이름
git switch -c release/1.0.0        # 배포: release/버전
git switch -c hotfix/login-error   # 긴급 수정: hotfix/문제이름
```

> 💡 혼자 하는 작은 프로젝트라면 **main + feature** 정도만 써도 충분하다. (GitHub Flow)

---

## 4. Merge 방식 1 : Fast-forward

**main에 새 커밋이 없고, feature만 앞으로 나아간 경우** 일어나는 병합이다.

```
병합 전                              병합 후
main      A───B                     main               A───B───C───D
               \                                                    ↑
feature         C───D               feature                     (같은 곳)
```

- 합칠 게 없으므로 **main 이름표를 D로 앞으로 옮기기만** 한다. (빨리 감기 ⏩)
- 새 커밋(merge commit)이 **생기지 않는다.**
- 기록이 일직선으로 깔끔하다.

```bash
git switch main
git merge feature        # Fast-forward로 병합됨
```

실행 결과에 `Fast-forward`라는 문구가 나온다.

---

## 5. Merge 방식 2 : 3-way merge

**main과 feature 둘 다 각자 새 커밋이 생긴 경우** 일어나는 병합이다.

```
병합 전                              병합 후
main      A───B───E                 main      A───B───E───M
               \                                   \     /
feature         C───D               feature         C───D
```

Git은 **세 개의 커밋**을 비교해서 합친다. 그래서 3-way다.

| 비교 대상 | 이 예시에서 |
|---|---|
| ① 공통 조상 (두 브랜치가 갈라진 지점) | B |
| ② 현재 브랜치의 최신 커밋 | E |
| ③ 합칠 브랜치의 최신 커밋 | D |

- 두 갈래를 합친 **새 커밋 M(merge commit)이 생긴다.**
- M은 부모가 두 개(E, D)인 특별한 커밋이다.
- 같은 파일의 **같은 줄**을 서로 다르게 고쳤다면 → **충돌(conflict)** 발생

```bash
git switch main
git merge feature        # 에디터가 열리면 merge commit 메시지 저장 후 닫기
```

### Fast-forward vs 3-way merge

| | Fast-forward | 3-way merge |
|---|---|---|
| 조건 | main에 새 커밋 없음 | 양쪽 모두 새 커밋 있음 |
| merge commit | 생기지 않음 | 생김 |
| 기록 모양 | 일직선 | 갈라졌다 합쳐짐 |
| 충돌 가능성 | 없음 | 있음 |

---

## 6. Merge 옵션

| 명령어 | 설명 | 사용 시점 |
|---|---|---|
| `git merge 브랜치` | 가능하면 Fast-forward, 아니면 3-way (기본값) | 일반적인 병합 |
| `git merge --ff 브랜치` | 기본값과 같음 | - |
| `git merge --no-ff 브랜치` | Fast-forward가 가능해도 **merge commit을 꼭 생성** | "이 기능을 여기서 합쳤다"는 기록을 남기고 싶을 때 |
| `git merge --squash 브랜치` | 브랜치의 여러 커밋을 **하나로 뭉쳐서** 스테이징만 함 (커밋은 직접 해야 함) | 지저분한 작업 커밋들을 하나로 정리하고 싶을 때 |

```bash
git merge --no-ff new-feature

git merge --squash new-feature
git commit -m "Add login feature"     # squash는 커밋을 직접 해야 완료됨
```

> 💡 `--squash`는 merge commit을 만들지 않고, 브랜치에서 왔다는 연결 정보도 남지 않는다. 결과적으로 main에는 커밋 하나만 깔끔하게 추가된다.

---

## 7. Merge conflict (충돌)

**두 브랜치가 같은 파일의 같은 부분을 서로 다르게 수정**했을 때, Git이 어느 쪽을 택할지 몰라서 사람에게 묻는 상황이다.

```
CONFLICT (content): Merge conflict in hello.py
Automatic merge failed; fix conflicts and then commit the result.
```

### 충돌 난 파일의 모습

```python
<<<<<<< HEAD
print("Hello, World!")
=======
print("Hello, Python!")
>>>>>>> feature
```

| 표시 | 의미 |
|---|---|
| `<<<<<<< HEAD` ~ `=======` | 현재 브랜치(main)의 내용 |
| `=======` ~ `>>>>>>> feature` | 합치려는 브랜치(feature)의 내용 |

### 해결 순서

1. `git status`로 충돌 난 파일 확인 (`both modified`로 표시됨)
2. 파일을 열어서 남길 내용으로 고치고, `<<<<<<<`, `=======`, `>>>>>>>` 표시를 **모두 지운다**
3. 저장 후 add, commit

```bash
git status                       # 충돌 파일 확인
# 파일 수정 후
git add hello.py                 # "충돌 해결했음" 표시
git commit -m "Resolve merge conflict in hello.py"
```

병합을 그만두고 원래대로 돌아가고 싶다면:

```bash
git merge --abort
```

> 💡 VS Code에서는 충돌 부분 위에 **Accept Current Change / Accept Incoming Change / Accept Both Changes** 버튼이 떠서 클릭으로 해결할 수 있다.

### 충돌 줄이는 습관
- 작업 시작 전 `git pull`로 최신 상태 받기
- 브랜치를 오래 두지 말고 자주 병합하기
- 한 커밋에는 한 가지 작업만

---

## 8. 더 알아두면 좋은 명령어

### rebase : 브랜치 시작점 옮기기

현재 브랜치의 커밋들을 **다른 브랜치의 끝으로 옮겨 붙인다.** merge commit 없이 기록을 일직선으로 만든다.

```
rebase 전                            git switch feature → git rebase main 후
main      A───B───E                 main      A───B───E
               \                                       \
feature         C───D               feature             C'───D'
```

```bash
git switch feature
git rebase main            # feature를 main 끝으로 옮기기
git rebase --continue      # 충돌 해결 후 계속 진행
git rebase --abort         # rebase 취소, 원래 상태로
```

> ⚠️ 이미 push해서 다른 사람과 공유한 브랜치는 rebase하지 말자. 커밋이 새로 만들어져(C', D') 다른 사람의 기록과 어긋난다.

### cherry-pick : 원하는 커밋만 골라 가져오기

다른 브랜치의 **특정 커밋 하나(또는 여러 개)만** 현재 브랜치에 복사한다.

```bash
git cherry-pick abcd1234               # 커밋 하나
git cherry-pick abcd1234 efgh5678      # 여러 개
git cherry-pick abcd1234^..efgh5678    # abcd1234부터 efgh5678까지 구간
git cherry-pick --continue             # 충돌 해결 후 계속
git cherry-pick --abort                # 취소
```

> 💡 `A..B`는 A를 **빼고** B까지, `A^..B`는 A를 **포함해서** B까지 가져온다.

---

## 9. 명령어 요약표

| 분류 | 명령어 | 한 줄 설명 |
|---|---|---|
| 보기 | `git branch` | 브랜치 목록 |
| 만들기 | `git branch 이름` | 브랜치 생성 |
| 이동 | `git switch 이름` | 브랜치 이동 |
| 만들고 이동 | `git switch -c 이름` | 생성 + 이동 |
| 이름 변경 | `git branch -m 새이름` | 브랜치 이름 바꾸기 |
| 삭제 | `git branch -d 이름` | 병합된 브랜치 삭제 |
| 병합 | `git merge 이름` | 현재 브랜치에 합치기 |
| 병합 | `git merge --no-ff 이름` | merge commit 꼭 남기기 |
| 병합 | `git merge --squash 이름` | 커밋 하나로 뭉쳐서 합치기 |
| 충돌 | `git merge --abort` | 병합 취소 |
| 재배치 | `git rebase 이름` | 브랜치 시작점 옮기기 |
| 골라오기 | `git cherry-pick 해시` | 특정 커밋만 가져오기 |
