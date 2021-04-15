
### git 에러 -  LF will be replaced by CRLF 해결하기

깃허브에서 add 하려는데 
```
 LF will be replaced by CRLF
 ```
 과 같은 에러가 발생했다.  
 이는 맥 또는 리눅스를 쓰는 개발자와 윈도우를 쓰는 개발자가 git으로 협업할 때 발생하는 Whitespace에러라고 한다.  
 유닉스 시스템에서는 한줄의 끝이 LF(Line Feed)로 이루어지는 반면,  
 윈도우에서는 줄 하나가 CR(Carriage Return)과 LF(Line Feed) 즉 CRLF로 이루어지기 때문이다.   
 그래서 git은 이 둘중에 어느 한쪽을 선택해야할지 혼란이 오기 때문에 해당 에러를 발생시킨 것이다.  
 
 나는 윈도우를 사용하고 있으므로
 ```
 git config core.autocrlf true
 ```
 를 통하여 해당 에러를 해결해주면 된다.
 --------------
 
 ### 참고자료
 - https://blog.jaeyoon.io/2018/01/git-crlf.html
