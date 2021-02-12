
네이버 검색 open api를 이용하여 네이버 쇼핑 검색결과를 json 형태로 받아와서 파싱하는 것을 공부했다.  
json파싱시에 json-simple 라이브러리를 다운받아 사용하면 된다. -> [다운로드 링크](https://code.google.com/archive/p/json-simple/downloads)

```java
package com.shop.test;
// 네이버 검색 API 예제 - shop 검색
import java.io.*;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.URL;
import java.net.URLEncoder;
import java.util.HashMap;
import java.util.Map;

import org.json.simple.JSONArray;
import org.json.simple.JSONObject;
import org.json.simple.parser.JSONParser;

public class ShopApiTest {

	public static void main(String[] args) {
		String clientId = ""; //애플리케이션 클라이언트 아이디값"
		String clientSecret = ""; //애플리케이션 클라이언트 시크릿값"

		String text = null;
		try {
			text = URLEncoder.encode("식자재", "UTF-8");
		} catch (UnsupportedEncodingException e) {
			throw new RuntimeException("검색어 인코딩 실패",e);
		}

		String apiURL = "https://openapi.naver.com/v1/search/shop?query=" + text;    // json 결과
		//String apiURL = "https://openapi.naver.com/v1/search/shop.xml?query="+ text; // xml 결과

		Map<String, String> requestHeaders = new HashMap<>();
		requestHeaders.put("X-Naver-Client-Id", clientId);
		requestHeaders.put("X-Naver-Client-Secret", clientSecret);
		String responseBody = get(apiURL,requestHeaders);

		//System.out.println(responseBody);

		try {
			JSONParser parser = new JSONParser();
			JSONObject obj = (JSONObject) parser.parse(new StringReader(responseBody));
			JSONArray products = (JSONArray) obj.get("items");

			System.out.println("---식자재 검색 결과---");
			for(int i = 0; i<products.size(); i++) {
				JSONObject tmp = (JSONObject)products.get(i);
				System.out.println("상품명 >> " + tmp.get("title"));
				System.out.println("최저가 >> " + tmp.get("lprice"));
				System.out.println();
			}

		} catch (Exception e) {
			System.out.println("e >> " + e.getMessage());
		}
	}

	private static String get(String apiUrl, Map<String, String> requestHeaders){
		HttpURLConnection con = connect(apiUrl);
		try {
			con.setRequestMethod("GET");
			for(Map.Entry<String, String> header :requestHeaders.entrySet()) {
				con.setRequestProperty(header.getKey(), header.getValue());
			}

			int responseCode = con.getResponseCode();
			if (responseCode == HttpURLConnection.HTTP_OK) { // 정상 호출
				return readBody(con.getInputStream());
			} else { // 에러 발생
				return readBody(con.getErrorStream());
			}
		} catch (IOException e) {
			throw new RuntimeException("API 요청과 응답 실패", e);
		} finally {
			con.disconnect();
		}
	}

	private static HttpURLConnection connect(String apiUrl){
		try {
			URL url = new URL(apiUrl);
			return (HttpURLConnection)url.openConnection();
		} catch (MalformedURLException e) {
			throw new RuntimeException("API URL이 잘못되었습니다. : " + apiUrl, e);
		} catch (IOException e) {
			throw new RuntimeException("연결이 실패했습니다. : " + apiUrl, e);
		}
	}

	private static String readBody(InputStream body){
		InputStreamReader streamReader = new InputStreamReader(body);

		try (BufferedReader lineReader = new BufferedReader(streamReader)) {
			StringBuilder responseBody = new StringBuilder();

			String line;
			while ((line = lineReader.readLine()) != null) {
				responseBody.append(line);
			}

			return responseBody.toString();
		} catch (IOException e) {
			throw new RuntimeException("API 응답을 읽는데 실패했습니다.", e);
		}
	}
}
```

실행결과는 아래와 같다.
![image](https://user-images.githubusercontent.com/64109506/107774971-12e3e280-6d83-11eb-9a4e-6c739813d6e6.png)
