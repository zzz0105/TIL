# 0121 Code Review

## 단축키

* Ctrl + / : 여러 줄 주석
* 선택 + tab : 여러 줄 tab
* shift + tab : tab 취소



## 함수 반환값

* 함수 정의했을 때 return을 해주지 않으면 결과값을 반환해주지 않는다.
* print()의 경우 값만 출력해준다. 결과값 반환은 아님!

   +. 함수 정의할 때 parameter에 팩 연산자 붙여놓으면 튜플로 들어온다. 

​		그러고 나서 parameter에 대해 for문 쓰면 통째로 들어와서 Error 뜬다.



## 딕셔너리

```python
dic = {
    ['A': '1', 'B':'2'],
    ['C': '3', 'D': '4']
}
dic[0]['A']		#'1'
dic[0].keys()	#'A', 'B'
```

