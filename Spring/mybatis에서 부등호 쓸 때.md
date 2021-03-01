
mybatis xml문에서 `>`나 `<`같은 부등호를 쓸 때 오류가 난다.
그럴 경우 `<![CDATA[ 내용 ]]>`로 감싸서 부등호를 사용할 수 있다.

```xml
<select id="selectFiveAlarm" resultType="avo" parameterType="avo">
		SELECT *
		FROM (SELECT * FROM ALARM ORDER BY INSERTDATE DESC )
		WHERE RECEIVER = #{receiver, jdbcType=VARCHAR}
		<![CDATA[AND ROWNUM <= 5]]>
	</select>
```
