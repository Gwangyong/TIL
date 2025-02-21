# Modify commit message already pushed to GitHub

- Git에서 이미 push한 commit 메시지를 수정하고 다시 push 하려면
- `git commit --amend`와 `git push --force` 명령어를 사용하면 된다.

<br>

### 1. commit 메시지 수정
```zsh
git commit --amend
```
- 위의 명령어를 실행하면 편집기가 열리고, 기존에 올린 커밋 메시지가 표시된다.
- `i`를 눌러서 메시지를 수정한 후, `Esc`룰 누르고 `:wq`를 입력하여 변경사항을 저장하고 종료한다.


### 2. 수정된 commit 메시지 push
```zsh
git push --force
```
- 이미 Git에 올라간 커밋을 덮어쓰려면 위의 명령어를 사용한다.
- 이 명령어는 기존의 커밋 메시지를 수정한 내용으로 원격 저장소에 `강제로` push한다.
- git push --force는 다른 사람과 협업 중일 경우, 공동 작업 중인 프로젝트 등에서는 원격 저장소의 히스토리를 덮어쓰게 되므로, 서로 변경사항을 공유한 후 사용하는 것이 안전하다.