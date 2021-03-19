# git command

> git 기초 명령어 정리

<br>

## 설정

### init

- `git init`
- 폴더를 git으로 관리하기 위해 `.git` 폴더를 생성하는 명령어
- 최초에 한 번만 실행하면 된다.

### status

- `git status`
- 현재 git의 상태를 출력(변경된 파일, 새로 만든 파일 등)

### log

- `git log`
- 현재 쌓여있는 commit history를 출력
  - git log --oneline: 히스토리를 커밋 당 한 줄로 요약 출력

### diff

- `git diff`
- 마지막 commit과 지금 working directory의 상태를 비교

### remote add

- `git remote add <별명> <주소>` 
  - 주로 `git remote add origin <주소>`로 사용한다.
- 원격저장소 주소를 등록

<br>

## 조작

---

### add

- `git add <파일이름>`
  - `<파일 이름>`에 .을 입력하면 전체 파일이 추가된다.
- working directory에 있는 파일을 staging area(INDEX)에 올린다.

### rm --cached

- `git rm --cached <파일이름>`
- staging area에 `add`했던 내역을 취소한다.

### restore --staged

- `git restore --stage <파일이름>`
  - 이전 버전에서는 `git reset --stage <파일이름>`
- `rm --chaed`와의 차이? 
  - https://stackoverflow.com/questions/65434544/whats-the-difference-between-git-rm-cached-git-restore-staged-and-gi

<br>

### commit

- `git commit -m "커밋메시지"`
- staging area에 올라간 파일들을 스냅샷으로 저장

### git commit --amend

- `git commit --amend` - `i` - 수정 - `esc` - `:wq`
  - commit 메시지를 수정할 수 있음  

- 특정 파일을 add하지 않고 commit 한 경우
  - 빼먹은 파일을 add 한 후, `git commit --amend` - `:wq`
  - `git status`를 통해 확인

<br>

### push

- `git push <원격저장소 이름> <올릴 브랜치 이름>`
  - `git push origin master`
- commit history를 원격 저장소에 업로드

### clone

- `git clone <주소>`
- 주소의 repository 폴더를 내 배쉬 디렉토리에 복사

### pull

- `git pull <원격저장소 이름> <올릴 브랜치 이름>`
  - `git pull origin master`
- 원격 저장소의 변경사항을 다운로드

<br>

## 버전 관리 Version Control

0. `git log`(`git log --oneline`)를 통해 커밋들의 고유값(`512b0c` 형태) 확인

- `git reset --hard <log 번호>`
  - HEAD가 <log 번호>에 해당되는 시점으로 이동, Staging Area와 Working Directory가 모두 지정한 commit 시점의 내용으로 변경된다.
- `git reset --soft <log 번호>`
  - HEAD가 <log 번호>에 해당되는 시점으로 이동, Staging Area와  Working Directory에는 변화가 없다.
- `git reset --mixed <log 번호>` = `git reset <log 번호>`, 기본값
  - HEAD가 <log 번호>에 해당되는 시점으로 이동, Staging Area가 지정한 commit 시점의 내용으로 변경되고, Working Directory는 변화가 없다.

