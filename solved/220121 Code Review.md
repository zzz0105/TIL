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
def my_abs(num):
    if type(num) is complex:	#복소수일 때
        return (num.imag**2 + num.real**2)**0.5
    elif type(num) == int or type(num) == float:    #정수나 실수일 때
        if n < 0:
            return -n
        elif n > 0:			
            return n
        else:			#-0 == 0이므로 num==0에 걸려서 처리됨. 따라서 제곱해서 반환.
            return n**2    
    
#type(num) is float or type(num) is int == type(num)이 float이거나 int이거나
#(type(num) is float) or (int) 이렇게 쓰는 것으로 인식.
#type(num) is (float or int)   이것도 안됨
```




## 자릿수 더하기

```python
#풀이1
def sum_of_digit(number):
    all_sum = 0
    for num in str(number):	#입력을 문자열로 변환하고 for문 사용
        all_sum += int(num)
    return all_sum

#풀이2. 정석풀이. 자릿수하면 몫과 나머지를 떠올리자!!
	def sum_of_digit(num):
	ans = 0
	while(n/10):			#n/10이 0이 아닐 때
    	#m = n % 10			#m은 나머지
    	#n //= 10			#n은 몫
    	n, m = divmod(n, 10)
    	ans += m
	return ans
```

