- [네이버 블로그에 이미지와 함께 정리한 글](https://blog.naver.com/wintersnow3/222227666348)  

### 셀레니움을 쓰는 이유

- selenium은 웹사이트 테스트를 위한 도구로 **브라우저 동작을 자동화**할 수 있다. 프로그래밍으로 브라우저 동작을 제어하여 마치 사람이 이용하는 것처럼 웹페이지를 요청하고 응답을 받아올 수 있다.
- 웹크롤링시에 아래와 같은 경우 셀레니움을 사용하여 해결할 수 있다.
    - 웹사이트가 로그인을 요구하는 경우

### 셀레니움 설치

```bash
pip install selenium
```

- chrome driver 설치 : [https://chromedriver.chromium.org/downloads](https://chromedriver.chromium.org/downloads)

자신의 크롬 버전을 확인한 후 이에 맞게 설치하면 된다.

```java
from selenium import webdriver

driver = webdriver.Chrome("./driver/chromedriver")
driver.get("https://google.com")
```

위 코드를 실행하면, selenium이 크롬 브라우저를 작동시켜 구글 사이트를 연다.

---

### 셀레니움으로 네이버 로그인하기

네이버 로그인의 경우 send_keys()로 아이디와 비밀번호를 입력할 경우 네이버 캡차(CAPCHA)가 이를 탐지하여 자동으로 로그인을 할 수 없게 된다.

```bash
from selenium import webdriver

id = ""#아이디
pw =""#패스워드
driver = webdriver.Chrome("./driver/chromedriver") #다운받은 드라이버 경로
#네이버 로그인 페이지로 이동
driver.get("https://nid.naver.com/nidlogin.login")

driver.find_element_by_id("id").send_keys(id)
driver.find_element_by_id("pw").send_keys(pw)
driver.find_element_by_id("log.login").click()
```

그래서 `pyperclip`을 이용하여 클립보드에 아이디와 비밀번호를 복사하여 넣어두고 이를 ctrl+v(붙여넣기) 키를 보내어 로그인을 하는 방식으로 캡차를 우회할 수 있다.

```python
import pyperclip
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.common.keys import Keys
from selenium import webdriver

def clipboard_input(id, user_input):
    temp_user_input = pyperclip.paste() #사용자 클립보드 저장
    pyperclip.copy(user_input) #클립보드에 id또는pw붙여넣기
    driver.find_element_by_id(id).click()
    ActionChains(driver).key_down(Keys.CONTROL).send_keys('v').key_up(Keys.CONTROL).perform()
    #pyperclip.copy(temp_user_input)

id = ""#아이디
pw =""#패스워드
driver = webdriver.Chrome("./driver/chromedriver")
#네이버 로그인 페이지로 이동
driver.get("https://nid.naver.com/nidlogin.login")

clipboard_input("id",id)
clipboard_input("pw",pw)
driver.find_element_by_id("log.login").click()

```

---

# 참고자료

- 셀레니움이 좋은 이유 : [https://hogni.tistory.com/76](https://hogni.tistory.com/76)
- 네이버 캡차 우회 로그인 : [https://hyrama.com/?p=693](https://hyrama.com/?p=693)
