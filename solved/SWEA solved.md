# [SWEA D1](https://swexpertacademy.com/main/code/problem/problemList.do?problemLevel=1&contestProbId=&categoryId=&categoryType=&problemTitle=&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)

## 1545. 거꾸로 출력해 보아요

```python
N = int(input())		#8
for i in range(N,-1,-1):
    print(i, end=' ')	#8 7 6 5 4 3 2 1 0
```



## 2019. 더블더블

```python
num = int(input())          #8
num_lst=[]
for i in range(num+1):
    print(2**i, end=' ')    #1 2 4 8 16 32 64 128 256
```



## 1936. 1대1 가위바위보

```python
a, b = map(int, input().split())	#가위 1 바위 2 보 3
if not a == b:
    if a == 1:
        if b == 2:
            print('B')
        else:
            print('A')
    if a == 2:
        if b == 1:
            print('A')
        else:
            print('B')
    if a == 3:
        if b == 1:
            print('B')
        if b == 2:
            print('A')
'''
3으로 나눈 나머지 코드를 사용하면 더 빠르게 가능하다.
A가 이기는 경우: '2 1' '3 2' '1 3'에서 보면 A ≡ B+1 (mod3) 을 만족하면 A승리
B가 이기는 경우: '1 2' '2 3' '3 1'에서 보면 A+1 ≡ B (mod3) 을 만족하면 B승리 
이 문제의 경우 경우의 수가 적어 그냥 코딩해도 괜찮은 듯
'''
```



## 1933. 간단한 N의 약수

```python
N = int(input())
for i in range(1, N+1):
    if N % i == 0:
        print(i, end=' ')	#정수 N의 모든 약수를 오름차순으로 출력한다.
```



## 1938. 아주 간단한 계산기

```python
'''
1. 두 개의 자연수 a, b는 1부터 9까지의 자연수이다. (1 ≤ a, b ≤ 9)
2. 사칙연산 + , - , * , / 순서로 연산한 결과를 출력한다.
3. 나누기 연산의 결과에서 소수점 이하의 숫자는 버린다
'''
a, b = map(int, input().split())
print(a+b)
print(a-b)
print(a*b)
print(a//b)
```



## 2025. N줄덧셈

```python
n = int(input())			#1부터 주어진 숫자까지의 합
sum = 0
for i in range(1, n+1):
    sum += i
print(sum)
```



## 2027. 대각선 출력하기

```python
print('''#++++
+#+++
++#++
+++#+
++++#''')
```



## 2029. 몫과 나머지 출력하기

* 가장 첫 줄에는 테스트 케이스의 개수 T가 주어지고, 그 아래로 각 테스트 케이스가 주어진다.
* 출력의 각 줄은 '#t'로 시작하고 공백을 한 칸 둔 다음, 몫을 출력하고 공백을 한 칸 둔 다음 나머지를 출력한다.

```python
T = int(input())	#테스트케이스
for i in range(T):
    a, b = map(int, input().split())
    quo = a // b
    remain = a % b
    print(f'#{i+1} {quo} {remain}')
```



## 2043. 서랍의 비밀번호

* 주어진 번호 K부터 1씩 증가하며 비밀번호 확인
* P, K 주어지면 K부터 시작하여 몇 번만에 P 맞출 수 있는가

```python
a, b = map(int, input().split())
print(b - a + 1)
```



## 2046. 스탬프 찍기

* 주어진 숫자만큼 # 출력하기

```python
a = int(input())
print('#' * a)
```



## 2047. 신문 헤드라인

* 입력으로 주어진 문장에 모든 소문자 알파벳을 찾아 대문자로 변환한 다음, 그 결과를 출력하는 프로그램을 작성하라

```python
sen = input()
new_sen = []
#print(sen.upper())
#대문자 아스키코드 = 소문자 아스키코드 - 32
for i in list(sen):
    if 97<=ord(i)<=122:
        i = chr((ord(i)-32))
    new_sen.append(i)
for j in new_sen:
    print(j, end='')
```



## 2050. 알파벳을 숫자로 변환

* 알파벳으로 이루어진 문자열을 입력 받아 각 알파벳을 1부터 26까지의 숫자로 변환하여 출력하라.
* 각 알파벳을 숫자로 변환한 결과값을 빈 칸을 두고 출력한다.

```python
chr_lst = list(input())	#대문자만 들어온다.
for chr in chr_lst:
    print(ord(chr)-64, end=' ')
```



## 2056. 연월일 달력

* 연월일 순으로 8자리의 날짜가 입력.
* 날짜가 유효하다면 YYYY/MM/DD 형식으로 출력하고,
* 날짜가 유효하지 않을 경우 -1 을 출력하는 프로그램을 작성하라.
* 연월일로 구성된 입력에서 월은 1~12 사이 값을 가져야 한다. 2월은 28일까지

```python
T = int(input())	#테스트 케이스 개수
for i in range(T):
    res = 0
    ymd = list(input())
    y_s = (''.join(ymd[:4]))
    m_s = (''.join(ymd[4:6]))
    d_s = (''.join(ymd[6:]))
    y = int(y_s)		#int로 바로 형변환하면 02월이 안나오고 2가 나옴..
    m = int(m_s)
    d = int(d_s)
    print(y, m, d)
    if not 0 < m < 13:
        res = -1        
    elif m == 2:
        if not 0 < d < 29:
            res = -1            
    elif m == 4 or  m == 6 or  m == 9 or  m == 11:
        if not 0< d < 31:
            res = -1
            
    elif not 0<d<32:
        res = -1
        
    if res == -1:
        print(f'#{i+1} {res}')
    else:
        print(f'#{i+1} {y_s}/{m_s}/{d_s}')
```



## 2058. 자릿수 더하기

* 하나의 자연수를 입력받아 각 자릿수의 합을 계산하는 프로그램을 작성하라.

```python
lst = list(input())
tot = 0
for i in lst:
    tot+=int(i)
print(tot)
```



## 2063. 중간값 찾기

* 크기 순으로 배열했을 때 중앙에 위치하는 수치

```python
N = int(input())	#N개의 정수 입력한다~
num_lst = list(map(int, input().split()))	#정수형으로 바꾼 리스트
num_lst = sorted(num_lst)					#정렬하기 lst.sort는 리스트로 바꿔 봐야함. sorted(lst)는 괜찮
print(num_lst[(1+N)//2 - 1])
```



## 2068. 최대수 구하기

```python
T = int(input())
for i in range(T):
    n_lst = list(map(int, input().split()))	#map쓰고 리스트로 보기!!
    big_n = n_lst[0]
    for n in n_lst:
        if big_n < n:
            big_n = n
    print(f'#{i+1} {big_n}')
```



## 2070. 큰 놈, 작은 놈, 같은 놈

* 2개의 수를 입력받아 크기를 비교하여 등호 또는 부등호 출력하는 프로그램

```python
T = int(input())
for i in range(T):
    a, b = map(int, input().split())
    if a > b:
        print(f'#{i+1} >')
    elif a < b:
        print(f'#{i+1} <')
    else:
        print(f'#{i+1} =')    
```



## 2071. 평균값 구하기

* 10개 수 받아 평균값 출력하는 프로그램. 소수점 첫째 자리에서 반올림

```python
T = int(input())
for i in range(T):
    tot = 0
    lst = input().split()
    for n in lst:
        tot += int(n)
    print(f'#{i+1} {round(tot/10)}')	#round(반올림하고 싶은 것, 자릿수)
```



## 2072. 홀수만 구하기

* 10개 수 입력받아 홀수만 더한 값을 출력하는 프로그램. 테스트 케이스 개수 T. 

```python
T = int(input())	#테스트 케이스
for i in range(T):	#테스트 케이스만큼 반복
    tot = 0
    lst = input().split()   #공백을 기준으로 찢는다.
    for n in lst:
        n = int(n)
        if n % 2:		#홀수면 더해준다.
            tot += n
    print(f'#{i+1} {tot}')
```



# [SWEA D2](https://swexpertacademy.com/main/code/problem/problemList.do?problemLevel=2&contestProbId=&categoryId=&categoryType=&problemTitle=&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=1&pageSize=10&pageIndex=1)

## 1204. [S/W 문제해결 기본] 1일차 - 최빈수 구하기

* 첫째 줄 테스트 케이스의 수 T / 둘째 줄 테스트 케이스의 번호 / 셋째 줄~ 점수

```python
#enumerate 얘 쓰면 접근이 복잡함.#[(0, (41, 15)), (1, (85, 6)), (2, (72, 10)),...

#zip
T = int(input())	#테스트 케이스 수
for i in range(T):	#테스트 케이스만큼 반복
    n = int(input())	#테스트 케이스의 번호
    scores_dic = {}
    many = 0    #최빈값의 인덱스 할당
    scores_lst = map(int, input().split())	#입력을 띄어쓰기로 분리하고 int형으로 형변환시켜 저장 
    for score in scores_lst:
        scores_dic[score] = scores_dic.get(score, 0) + 1    # 점수 : 횟수
    score_item_lst = list(zip(scores_dic.keys(), scores_dic.values()))

    for j in range(len(score_item_lst)):
        if score_item_lst[many][1] < score_item_lst[j][1]:
            many = j

    print(f'#{n} {score_item_lst[many][0]}')
```



## 1284. 수도 요금 경쟁

* 종민이의 집에서 한 달간 사용하는 수도의 양: W리터
* A사 : 1리터당 P원의 돈을 내야 한다.
* B사 : 기본 요금이 Q원이고, 월간 사용량이 R리터 이하인 경우 요금은 기본 요금만 청구된다. 하지만 R 리터보다 많은 양을 사용한 경우 초과량에 대해 1리터당 S원의 요금을 더 내야 한다.
* 첫 번째 줄에 테스트 케이스의 수 T가 주어진다. 각 테스트 케이스마다 첫 번째 줄에 위 본문에서 설명한 대로 P, Q, R, S, W(1 ≤ P, Q, R, S, W ≤ 10000, 자연수)가 순서대로 공백 하나로 구분되어 주어진다.
* 각 테스트 케이스마다 ‘#x’(x는 테스트케이스 번호를 의미하며 1부터 시작한다)를 출력하고, 종민이가 내야 하는 수도 요금을 출력한다.

```python
T = int(input())	#테스트 케이스 수
for i in range(T):	#테스트 케이스 수만큼 반복
    P, Q, R, S, W = map(int, input().split())
    #A사
    A = P * W
    #B사
    if W < R:
        B = Q
    else:
        B = Q + S * (W - R)
    money = A if A < B else B
    print(f'#{i + 1} {money}')
```



## 1285. 아름이의 돌 던지기

* 아름이 포함 N명. 가장 0에 가깝게 돌이 떨어진 위치와 0 사이의 거리 차이와 몇 명이 그렇게 돌을 던졌는지를 구하는 프로그램을 작성하라. ( 돌이 떨어지는 위치는 항상  -100,000에서 100,000사이 범위의 정수)
* 입력: 테스트케이스 \n 명 수 \n 떨어진 위치(숫자 사이 공백)

```python
T = int(input())    #테스트 케이스
for i in range(T):
    people = int(input())   #사람 수 
    pos = map(int, input().split()) #돌 떨어진 위치
    cnt = 1
    min = 100000    #0과 가까운 정도를 비교할 변수. 최대값 부여
    for p in pos:
        if abs(p) < abs(min):
            min = p
            cnt = 1
        elif abs(p) == abs(min):
            cnt += 1        
    print(f'#{i+1} {abs(min)} {cnt}')   #거리 차이 및 그렇게 던진 사람의 수
```



## 1945. 간단한 소인수분해

```python
T = int(input())
for i in range(T):
    in_num = int(input())
    nums_dic = {2:0, 3:0, 5:0, 7:0, 11:0}

    for num in nums_dic.keys():
        while(in_num/num).is_integer():	#정수형인지 판별(5.0도 정수로 판별)
            in_num/=num
            nums_dic[num] += 1

    ans = ' '.join(map(str, list(nums_dic.values())))
    print(f'#{i+1} {ans}')
```





