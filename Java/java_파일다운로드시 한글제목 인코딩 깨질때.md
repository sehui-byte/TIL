### 파일 다운로드시 한글제목 인코딩 깨질 때



파일 다운로드시 한글 제목이 깨지는 이슈가 발생했다.

![image-20210604153417747](C:\Users\nextree\AppData\Roaming\Typora\typora-user-images\image-20210604153417747.png)



`request header`정보에서 '**User Agent**' 정보를 통해 유저의 브라우저 정보를 확인하고, 브라우저마다 인코딩을 다르게 해주면 된다고 한다.

```java
  if (header.contains("Edge")){
            name = URLEncoder.encode(name, "UTF-8").replaceAll("\\+", "%20");
        } else if (header.contains("MSIE") || header.contains("Trident")) {
            name = URLEncoder.encode(name, "UTF-8").replaceAll("\\+", "%20");
        } else if (header.contains("Chrome")) {
            name = new String(name.getBytes("UTF-8"), "ISO-8859-1");
        } else if (header.contains("Opera")) {
            name = new String(name.getBytes("UTF-8"), "ISO-8859-1");
        } else if (header.contains("Firefox")) {
            name = new String(name.getBytes("UTF-8"), "ISO-8859-1");
        }
```



----



## 참고자료

- https://developersp.tistory.com/14

- https://www.manty.co.kr/bbs/detail/develop?id=12