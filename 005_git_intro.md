# Git intro

## 자주 쓰는 명령

### 도움말 보기

```bash
git help
```

- 주요 command에 대한 설명

```bash
git commit --help
```

- 특정 command에 대해 궁금할 경우 `--help`를 붙여서 도움말을 볼 수 있음.

## 설정하기 (git config)

```bash
git config --global user.email "email@example.com"
git config --global user.name "Bashful Smith"
```

- commit 에 표시할 이메일 설정 (필수)
- commit 에 표시할 이름 설정

```bash
git config --global -l
git config --local -l
```

- global 설정 목록 보기
- local 설정 목록 보기

```bash
git config --global diff.wsErrorHighlight all
 ```

 whitespace 차이 보기

### 새롭게 Git repository를 시작함

```bash
git init
```

- 해당 프로젝트 폴더에서 실행
- `.git` 폴더가 생김

### 처음 다른 사람 코드 다운로드 받기

```bash
git clone xxx://xxx@xxx.xxx/xxx
cd xxx
```

- xxx 폴더가 만들어지고 받아짐.
- 나머지는 Git 명령들은 거기 폴더 들어가서 실행

### 작업한 내용확인하기

```bash
git status
```

- 현재 작업중인 브랜치가 어디인지 보여줌
- 작업중인 브랜치에서 내가 수정/삭제/생성한 파일의 목록을 보여줌
- index 에 올라간 변경사항 목록도 함께 보여줌

```bash
git diff
```

- 작업중인 브랜치에서 변경된 파일의 중 index에 올라가진 않은 파일의 변경 내용을 보여줌

```bash
git diff --cached
```

- 작업중인 브랜치에서 변경된 파일의 중 index에 올라간 변경 내용을 보여줌

```bash
git log
```

- 최근 커밋들에 대한 정보를 보여줌
- 현재 작업중인 브랜치를 기준

```bash
git log --oneline --decorate --graph
```

- `--online` 한줄씩
- `--decorate` 브랜치나 태그 정보도 보여줌
- `--graph` merge 된 경우 그 관계를 그래프로 보여줌

### 특정 파일만 덮어 씌우기

```bash
git checkout file_or_folder
git checkout origin/issue-1 -- file_or_folder
```

- `--` 이후에는 브랜치 이름이 올 수 없음. 대상 파일이나 폴더를 지칭하겠다는 것을 명시.

### 작업할 브랜치 바꾸면서 내용 덮어 씌우기

```bash
git checkout issue-2
```

- issue-1 브랜치에서 작업하고 있다가 issue-2 브랜치에서 작업하고 싶을때
- 파일의 내용들이 issue-2 브랜치에 해당하는 내용들로 일괄 수정됨.
- issue-2 가 브랜치 이름이 아닌경우 파일 이름인지 체크하게 됨.
- 브랜치 이름 대신 tag 이름이나 commit id 를 쓰면 현재 작업 중인 브랜치 가 없는 detached head 상태가 됨.

### 작업 중인 브랜치를 옮기면서 내용 덮어 씌우기

(issue-1 브랜치에서 작업하고 있다가 issue-1을 다른 커밋으로 옮겨서거기서 계속 issue-1 브랜치에서 작업하고 싶을때)

```bash
git reset --hard HEAD~3
git reset --hard origin/issue-1
git reset --hard issue-1-hoyeong
```

### 작업한거 index 에 올리기

```bash
git add file_or_folder
```

### 작업한거 index 에서 다시 내리기

```bash
git reset file_or_folder
```

### 작업한거 로컬에 commit 하기

```bash
git commit
```

- 편집창에서 저장하면 완료됨

```bash
git commit --amend
```

- 새로운 커밋을 만들지 않고, 직전 커밋에 변경사항을 추가함.
- 커밋 메시지가 틀린경우에 수정하기 위해 실행할 수도 있음.

### 리모트에 바뀐거 받아오기

```bash
git fetch
```

- 실재 파일들에는 직접적 영향 없음
- `git pull` 은 현재 브랜치에서 merge commit 만들면서 실재 파일들도 수정하게 됨

### 작업중 브랜치랑 다른 브랜치 통합하는 1개의 커밋 만들기 (merge)

(누가 새로운 내용을 origin/master에 올렸다면 git fetch 한 상태애서 아래 명령 실행하여 새로운 커밋 만들기)

```bash
git merge origin/master
```

### 작업중 브랜치의 시작 지점 옮기기 (rebase)

```bash
git rebase origin/master
```

- 내 브랜치에서 작업한 커밋들이 대상 브랜치 위로 올라가도록 새로운 커밋들을 만듬

```bash
git rebase -i HEAD~4
```

- `-i` 는 commit 들의 내용을 보면서 작업함
  - drop: 해당 commit 제외하기.
  - squash: 해당 commit 을 이전 commit 과 합치고 commit 메시지도 합치기. (편집창이 새롭게 뜸)
  - fixup: 해당 commit 을 이전 commit 과 합치고 commit 메시지는 버리기.
  - 줄을 통째로 옮겨 놓으면 commit 들 간의 순서 바꾸기 가능

### 특정 커밋만 현재 브랜치로 가지고 옴

```bash
git cherry-pick commit_id
```

- 특정 커밋을 현재 브랜치로 콕 찍어서 가지고 옴
- commit ID 대신 브랜치 이름을 지정할 경우에도 그 브랜치가 가리키고 있는 commit 하나만 가지고 옴.

### pull/merge/rebase/cherry-pick 에서 conflict 해결하기

```c
void main() {
  <<<<<<< HEAD
  int a = 4;
  =======
  int b = 3;
  >>>>>>> new_branch_to_merge_later
}
```

- `git status` 에서 conflict가 난 파일을 찾을 수 있으며 혹은 `<<<<<<<` 등으로 전체 프로젝트에서 검색해서 conflict 가 발생한 파일을 찾아볼 수 있음.
- `main.c` 파일에서 conflict가 났다면 `main.c`의 conflict가 난 부분이 위의 예시 처럼 바뀌어 있음.
- `new_branch_to_merge_later`의 커밋을 HEAD로 가져오다가 conflict 가 발생하였다는 의미임.

```c
void main() {
  int b = 4;
}
```

- text editor 에서 `main.c`파일을 위와 같이 원하는 방식으로 직접 수정하면 됨.

```bash
git add main.c
git rebase --continue
```

- `main.c` 의 수정이 끝났다면 위와 같이 하려고 했던 작업(pull/merge/rebase/cherry-pick)을 진행할 수 있음.

```bash
git rebase --abort
```

만약 conflict를 해결하고 싶지 않다면 위와 같이 `--abort` 해서 원래의 하려던 작업 진행 전 상태로 돌아갈 수 있음.

### 작업한거 리모트에 올리기

```bash
git push
git push -f
```

- 강제로 올릴땐 `-f`

### 태깅

```bash
git tag v1.0.0
```

### 임시 보관소 stash 사용하기

```bash
git stash
```

- Untracked files 을 제외한 나머지 현재 작업중인 변경사항들을 stash 에 보관함.
- 다시 파일을 수정 후 `git stash` 하면 추가로 다시 stash 에 보관할 수 있음.

```bash
git stash pop
```

- stash 에 있는 변겨사항을 꺼내와서 다시 파일들에 적용함.
- 마지막에 보관한 내용이 제일 먼저 나옴. (LIFO)

## References

[Git Branching 연습](https://learngitbranching.js.org/)
