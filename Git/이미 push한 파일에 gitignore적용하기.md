

이미 git에 push한 상태에서 `.gitignore`을 적용하면 적용이 되지 않는다.

![Reverting Modified in 4 Stages in Git | by Jianping Zeng | Medium](https://miro.medium.com/max/3860/1*tjrF1ff5UjVNclwwe_GREg.png)

이유는 **이미 stage에 올라간 파일들은 캐시 처리가 되어 기록이 남기 때문**이다.

그래서 아래 명령어를 이용하여 캐시를 전부 삭제하고, 다시 올림으로써 `.gitignore`를 적용할 수 있다.

```
$ git rm -r --cached .
$ git add .
$ git commit -m "Apply .gitignore"
$ git push
```



-------

### 참고자료

- https://webruden.tistory.com/134