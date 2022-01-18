# 0118 Code Review

## 리스트 안 해당 요소의 개수

```python
words = ['a', 'b', 'a', 'c', 'b', 'c', 'a', 'a']
print(students.count('a'))
```



## 최댓값 & 등장 횟수

```python
#최댓값을 판별할 때 변수에 가장 작은 값을 할당하고 비교를 시작할 때가 있다.
#inf의 경우 어떤 숫자와 비교해도 무조건 크다고 판정되므로, -inf는 가장 작은 값이다.
#최댓값과 등장 횟수를 각각 구하는 것보다 한 루프에서 돌면 복잡도가 줄어든다.
nums =[7, 50, 22, 27, 50]
big_num = nums[0]
big_num_cnt = 0
for num in nums:
    if big_num < num:
        big_num = num
        big_num_cnt = 0	#큰 수가 바뀌면 지금까지 센 것 초기화
    if big_num == num:
        big_num_cnt += 1	#'+='은 붙여서 쓴다.
print(big_num, big_num_cnt)
```



## 요소 찾기

```python
#리스트 컴프리헨션
#변수명 지을 때 i, idx는 순서(인덱싱)를, 리스트 안 요소일 때는 다른 이름을 사용하면 좋다.
nums= [2, 5, 6, 8, 5, 4, 3, 7, 2, 1]
#nums 리스트의 요소 num. 만약 num이 2이면 num을 num_cnt에 넣는다. 그 후 길이를 잰다.
num_cnt = [num for num in nums if i==2]	
print(len(num_cnt))
```



## 요소 빼기

```python
#리스트 활용
word = input()
word = list(word)
result = []
for i in word:
    if i != 'a':
        result.append(i)
print(''.join(result))	#리스트를 문자열로 출력할 때. 리스트 안의 요소들을 붙여서 출력
print(*result, sep='')	#result 언패킹. 출력하면서 사이에 ''출력해라(=공백없이 출력)
print(result, sep='')	#결과는 리스트인 result가 나온다.
#continue 활용. a를 만나면 뒤에 있는 print문을 실행하지 말고 바로 다음 요소로 넘어가라
for char in word:
    if char == 'a':
        continue
    print(char, end='')
#replace 메서드 사용. word의 a요소를 ''으로 대신 출력
print(word.replace('a',''))
#문자열
new_word=''
for char in word:
    if char != 'a':
        new_word += char
print(new_word)
#리스트 컨프리헨션
new_word = [char for char in word if not char = 'a']
print(''.join(new_word))
```



## 단어 뒤집기

```python
word = input()
#리스트 슬라이싱 사용. 처음부터 끝까지 왼쪽으로 한칸씩 움직이며 출력해라
print(word[::-1]) 
#for문을 활용. print('a', end='b'): ab. a 출력하고 뒤에 b 붙인다(줄바꿈x)(초기값='\n').
#print('a', 'b', sep='c'): acb. a와 b 사이에 c를 출력한다.(초기값=' ')
for i in range(len(word)):
    print(word[len(word)-i-1], end='')
#문자열을 만들어나가는 코드
rev_word = ''
for alphabet in word:
    rev_word = alphabet + rev_word
print(rev_word)
```



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

