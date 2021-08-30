

## git stash

B브랜치에서 작업해야하는데 실수로 A브랜치에서 작업하고 있었다. 이럴 경우 `git checkout [B브랜치]` 로 B브랜치로 이동하려고 할 경우 working directory에 있던 작업내용을 커밋하든가 날려버리고 이동해야한다. 

이럴 땐 어떻게 해야할지 찾아보다가 `git stash` 명령어를 알게 되었다.



### git stash란?

> Use `git stash` when you want to record the current state of the working directory and the index, but want to go back to a clean working directory. The command saves your local modifications away and reverts the working directory to match the `HEAD` commit.



stash에 로컬에서 작업한 내용들을 담아두고, 원하는 브랜치로 checkout한다. 그 다음에 내가 작업한 내용을 pop하면 내가 작업한 내용들이 원하는 브랜치에 적용된다.

```shell
git stash push
git checkout 브랜치
git stash pop
```

`git stash push`를 하면 현재 내가 작업중인 unstage, stage 내용들이 모두 stash에 저장된다.



-------------

```sh
// stash 저장 (working directory clean)
git stash save

//stash 목록 확인하기
git stash list

// stash 적용
git stash apply

// stash 제거
git stash drop

// drop + apply
git stash pop

```



---

## 참고자료

- https://bgpark.tistory.com/51

- https://git-scm.com/docs/git-stash

- https://gmlwjd9405.github.io/2018/05/18/git-stash.html