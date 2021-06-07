### git - 특정 파일 히스토리 삭제하는 법



git에 올리지 말아야할 정보가 담긴 파일을 업로드했을 때, 히스토리 삭제와 함께 해당 파일도 지우고 싶다면 아래 명령어를 통해서 해당 파일과 관련된 히스토리를 전부 지울 수 있다.



```bash
$ git filter-branch --force --index-filter "git rm --cached --ignore-unmatch [삭제할 파일]" --prune-empty --tag-name-filter cat-- --all


$ git push origin master --force

```



#### filter-branch

```
git filter-branch [--setup <command>] [--subdirectory-filter <directory>]
	[--env-filter <command>] [--tree-filter <command>]
	[--index-filter <command>] [--parent-filter <command>]
	[--msg-filter <command>] [--commit-filter <command>]
	[--tag-name-filter <command>] [--prune-empty]
	[--original <namespace>] [-d <directory>] [-f | --force]
	[--state-branch <branch>] [--] [<rev-list options>…​]
```

- `git filter-branch`는 상당히 위험한 명령어이다.  해당 명령어를 수행한 경우 백업파일은 다음 경로에 생성된다. -> *.git/refs/original/refs/heads/master*

  ```bash
  //백업본으로 되돌리기
  git reset --hard refs/original/refs/heads/master
  ```

- `filter-branch` : **브랜치 내에서 특정 이력을 다시 쓰는 history rewrite가 가능한 옵션.** 

- `--index-filter` : **인덱스를 다시 쓰기 위한 필터.** `git rm --cached --ignore-unmatch]`와 자주 함께 쓰인다. tree filter와 비슷하지만 tree를 체크하지 않기 때문에 훨씬 더 빠르다.

  - > --index-filter <command>
    >
    > This is the filter for rewriting the index. It is similar to the tree filter but does not check out the tree, which makes it much faster. Frequently used with `git rm --cached --ignore-unmatch ...`, see EXAMPLES below. For hairy cases, see [git-update-index]

- `--prune-empty`: **unreachable한 git object들을 local에서 clean한다.  `prune`은 remote의 것을 지우는 것이 아니라 local에서 remote를 참조(ref)하는 것 중 유효하지 않은 것들을 제거하는 작업이다. 즉, 유효하지 않는 빈 커밋들을 완전히 제거한다.**

  - >--prune-empty
    >
    >Some filters will generate empty commits that leave the tree untouched. This option instructs git-filter-branch to remove such commits if they have exactly one or zero non-pruned parents; merge commits will therefore remain intact. This option cannot be used together with `--commit-filter`, though the same effect can be achieved by using the provided `git_commit_non_empty_tree` function in a commit filter.

- `ignore-unmatch`: **언제 원치 않는 파일이 add 되었는지 몰라도, 즉 이 파일이 존재하지 않는 커밋을 돌 때도 error를 내지 않고 그냥 무시한다는 옵션이다.**



---

### 참고자료

- https://rudalson.tistory.com/entry/git-history%EC%97%90%EC%84%9C-%ED%8C%8C%EC%9D%BC-%EC%98%81%EA%B5%AC%EC%A0%81%EC%9C%BC%EB%A1%9C-%EC%A7%80%EC%9A%B0%EA%B8%B0

- https://git-scm.com/docs/git-filter-branch/en

- https://aluc.io/2018-05-23-git-filter-branch.html

- [번역-github/advanced git/민감한 데이터 제거하가](http://minsone.github.io/git/github-advanced-remove-sensitive-data)

- https://ndb796.tistory.com/273

- [How remove files completely from git repository history](https://myopswork.com/how-remove-files-completely-from-git-repository-history-47ed3e0c4c35)

- https://medium.com/code-states/%EA%B3%BC%EA%B1%B0%EB%A5%BC-%EC%A7%80%EC%9A%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4%EC%9A%94-git-history-82e081b51122

- [git prune이란?](https://medium.com/code-states/%EA%B3%BC%EA%B1%B0%EB%A5%BC-%EC%A7%80%EC%9A%B0%EA%B3%A0-%EC%8B%B6%EC%96%B4%EC%9A%94-git-history-82e081b51122)

- [remove files from git history](https://blog.tinned-software.net/remove-files-from-git-history/)