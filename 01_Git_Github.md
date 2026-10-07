# 1. Git & Github
## Git & GitHub를 사용해야 하는 이유
-
|이유 | 설명|
|---|---|
|버전관리| 파일을 복사하지 않아도 모든 변경 기록이 저장된다. 언제든 과거 시점으로 되돌릴 수 있다.|
|변경 이력 추적| 누가, 언제, 무엇을, 왜 바꿨는지 기록이 남는다.|
|안전한 실험| Branch를 만들어 원본을 건드리지 않고 새로운 기능을 시도할 수 있다.|
|협업| 여러 사람이 같은 프로젝트를 동시에 작업하고 결과를 합칠 수 있다.|
|백업| GitHub에 올려두면 컴퓨터가 고장 나도 코드가 안전하다.|
|포트폴리오| GitHub 프로필의 Commit 기록과 저장소가 곧 개발 이력서가 된다.|

# 2. Git과 GitHub 차이
Git은 도구, GitHub는 그 도구로 만든 결과물을 올려두는 장소

|구분|Git|GitHub|
|---|---|---|
|종류|버전 관리 프로그램|Git 저장소를 올리는 웹 서비스|
|위치|내 컴퓨터(local)|인터넷 (원격, 클라우드)|
|인터넷|없어도 사용 가능|필요함|
|주요기능|commit, branch, merge등 기록 관리|저장소 공유, 협업, Pull Request, GitHub Pages|
|비유|일기는 쓰는 방법|일기장을 보관하는 클라우드|

 - Git은 2005년 리누스 토르발스(리눅스 개발자)가 만들었다
 - GitHub 외에서 GitLab, Bitbucket 같은 비슷한 서비스가 있다.

 ```bash
git --version   # 내 컴퓨터에 Git이 설치되어 있는지 확인
```

# 3. Repository(저장소)
**Git이 관리하는 프로젝트 폴더.** 파일들과 그 파일들의 모든 변경기록(.git 폴더)이 함께 들어 있다.

|종류|설명|
|---|---|
|Local Repository|내 컴퓨터에 있는 저장소|
|Remote Repository|GitHub 같은 서버에 있는 저장소|

**주요 명령어**
```bash
git init               # 현재 폴더를 새 저장소로 만들기
git clone <저장소 주소>   # GitHub 저장소를 내 컴퓨터로 복제
git remove -v          # 연결된 원격 저장소 확인
git push               # 로컬 -> GitHub로 올리기
git pull               # Github -> 로컬로 받아오기
```

**예시**
```bash
git clone https://github.com/having-all/OZ_school.git
```
🎯.git 폴더는 숨김 폴더이며, 지우면 모든 기록이 사라지므로 건드리지 않는다.

# 4. Commit
**프로젝트의 현재 상태를 하나의 기록(스냅샷)으로 저장하는것.** 게임의 세이브 포인트와 같다.

 # Git의 3단계 영역
- Working Directory (작업중인 파일)
  - git add
- Staging Area (commit할 파일 대기)
  - git commit
- Repository (기록으로 저장)

**주요 명령어**
```bash
git status               # 현재 상태 확인(수정된 파일, 대기 중인 파일, 현재 작업중인 commit 확인)
git add 파일명             # 특정 파일을 Staging Area에 올리기
git add .                # 변경된 모든 파일 올리기
git commit -m "커밋 메시지" # 기록으로 저장
git log --oneline        # 커밋 기록 한 줄씩 보기
git diff                 # 아직 add하지 않은 변경 내용 보기
```



