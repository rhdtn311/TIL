# eval

`eval()` 함수는 파라미터로 문자열을 입력 받으면 그 값을 실행하여 결과를 도출해준다. 

```python
# 식 계산
sentence = "1+2+3+4+5"
print(eval(sentence)) >>> 15

# 함수 
array = [1,2,3,4,5,10]
print(eval("len(array)")) >>> 6
print(eval("max(array)")) >>> 10
```

하지만 `eval()` 함수는 `string` 값을 이용하여 프로그램을 제어할 수 있기 때문에 사용자의 입력값(`input()`)을 통해 프로그램이 제어당할 수 있다. 따라서 프로젝트나 서비스 개발시에 사용하지 않는 것이 좋다.
