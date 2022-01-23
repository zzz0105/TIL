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
dic = {						#변수 이름 지을 때 유의하기
    ['A': '1', 'B':'2'],
    ['C': '3', 'D': '4']
}
dic[0]['A']		#'1'
dic[0].keys()	#'A', 'B'
```



## List 내 전체 합 구하기

```python
#재귀함수 사용
def list_sum(lst):
    result = 0
    for i in lst:
        if type(i) == list:
            result += list_sum(i)
        else:
            result += i
    return result
#입력 예시: list_sum([[9],2,[1,3,2, [1, 5]],[6,8]])
```



## abs() 함수 구현

```python

```



## all() 함수 구현
```python

```




## any() 함수 구현
```python

```




## 자릿수 더하기

```python

```





