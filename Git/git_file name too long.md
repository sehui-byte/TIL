### git Filename too long 에러

git clone을 하는데 file name too long 에러가 발생하면서 정상적으로 clone되지 않는 상황이 발생했다. 



- https://dlibs.tistory.com/2

위 글을 참고하여 해결했다.



1. **git bash 관리자 권한으로 실행**
2. **git config --system core.longpaths true**

를 하고나서 정상적으로 git clone을 할 수 있었다.

