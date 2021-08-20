



### 원격저장소의 브랜치 사용하기

```
git remote update
//원격저장소의 브랜치들을 확인한다
git branch -r
//원격저장소 branch로 checkout하기
git checkout -t origin/[브랜치명]
```



### 로컬에서 원격저장소와 연동되는 브랜치 생성

```
git checkout -b [브랜치명]
git push origin [브랜치명]
```



### 원격 브랜치 삭제하기

```
git push origin --delete [브랜치명]
```



### 로컬 브랜치 삭제하기

```
git branch -d [브랜치명]
```

