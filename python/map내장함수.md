## map내장함수

- 여러 개의 데이터를 한번에 다른 형태로 변환하기 위해서 사용된다.
- map의 리턴 값은 map object이므로 list나 tuple로 바꿔서 사용하는 것이 좋다.

### 예제

```python
a_list = [1.2, 2.5, 3.7, 4.6]
a_list = list(map(int, a))
```

map함수를 이용하여 a_list의 모든 요소를 int를 사용해서 변환했다. 그리고 list()로 map의 결과를 다시 리스트로 만들어준다.

![image](https://user-images.githubusercontent.com/64109506/107047013-add04000-680a-11eb-865e-a3d07d999b05.png)

### 1차원 배열 입력받기

```python
a = list(map(int, input().split()))
```

`input().split()`의 결과는 문자열 리스트로 반환된다. 

### 2차원 배열 입력받기

```python
b = [list(map(int, input().split())) for _ in range(n)]
```

---

# 참고자료

- map함수, map함수예제 이미지 출처 - [https://dojang.io/mod/page/view.php?id=2286](https://dojang.io/mod/page/view.php?id=2286)
