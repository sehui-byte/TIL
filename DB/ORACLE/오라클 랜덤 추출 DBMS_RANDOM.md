
2021-03-02 
  
 오늘 작업하면서 db에서 랜덤하게 3개의 데이터만 추출하는 쿼리문이 필요해서 찾아보다가 오라클 내장함수 패키지인 `DBMS_RANDOM`을 이용해서 랜덤 추출이 가능하다는 것을 알게 되었다.
 
 ```sql
SELECT * 
FROM 
    (SELECT * FROM RECIPE ORDER BY DBMS_RANDOM.RANDOM)
WHERE ROWNUM <= 3;
 ```

즉 랜덤하게 정렬한 다음에 rownum을 통해 3개의 행만 가져오게 되는 것이다.
