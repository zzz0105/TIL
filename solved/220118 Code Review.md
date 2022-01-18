# 0118 Code Review

## Floating point rounding error(부동소수점 반올림 오차)

* 파이썬은 부동소수점 방식으로 실수를 표현하는데, 부동소수점은 실수를 정확히 표현할 수 없는 문제가 있다.
* abs, sys.float_info.epsilon, math.isclose 활용

```python
x = 0.1 + 0.2
abs(x = 0.3) <= 1e-10	#임의의 작은 수와 비교

import sys
abs(x - 0.3) <= sys.float_info.epsilon
#sys.float_info.epsilon에 저장된 것은 머신 엡실론. 
#어떤 실수를 가장 가까운 부동소수점 실수로 반올림 했을 때 상대 오차는 항상 머신 엡실론 이하.

import math
math.isclose(0.1 + 0.2, 0.3)
```



## 형 변환 오류

int 함수는 정수 문자열이나 실수를 인자로 받는데, 실수 문자열로 입력이 되면 오류 발생



## 네모 출력

두 정수가 입력되었을 때 반복문을 사용하지 않고 *로 직사각형 형태를 출력하기

```python
n = 5
m = 9
print(('*' * n + '\n') * m)

#반복문 사용시
for i in range(m):
    print('*' * n)
```



## mutable과 immutable의 차이

* mutable(변경 가능): List, Set, Dictionary
* immutable(변경 불가): String, Tuple, Range

```python
a = 'string'
a[0] = '1'	
#이 같은 코드로 요소를 변경 가능한 것이 mutable. 문자열 형태는 불가능하기 떄문에 immutable.
```



## 홀수만 출력

```python
print(list(range(1,51,2)))
print(list(range(1,51)[::2]))	
#[a:b:c]: list[a]부터 list[b-1]까지 c step만큼 이동하며 가져온다.
```



## 숫자 계단 출력

```python
in_num = int(input())
for i in range(1, in_num+1):
    for j in range(1,i+1):
        print(j, end='  ')
    print('')
```

