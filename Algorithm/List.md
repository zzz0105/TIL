# 배열

> 좋은 알고리즘을 이해하고 활용하기
>
> 하나의 문제에 모든 코드를 모을 필요는 없다.

## 알고리즘

> 유한한 단계를 통해 **문제를 해결하기 위한 절차**나 방법. 
>
> 컴퓨터가 어떤 일을 수행하기 위한 단계적 방법

### 알고리즘 표현하는 방법

* 의사코드(슈도코드, Pseudocode)와 순서도

### 알고리즘의 성능은 무엇으로 측정하는가

1. *정확성: 얼마나 정확하게 동작하는가
2. 작업량: 얼마나 적은 연산으로 원하는 결과를 얻어내는가
3. 메모리 사용량: 얼마나 적은 메모리를 사용하는가 => 불필요한 반복문 줄이기
4. 단순성: 얼마나 단순한가
5. 최적성: 더 이상 개선할 여지없이 최적화되었는가



#### 시간복잡도

* 알고리즘의 작업량을 표현할때 사용
* 실제 걸리는 시간을 측정
* 실행되는 명령문의 개수를 계산

* 빅-오(O) 표기법

  * 시간  복잡도 함수 중에서 가장 큰 영향력을 주는 n에 대한 항만을 표시(계수는 생략하여 표시)

  * ex. 

    O(3n+2) = O(n)

    O(2n^2 + 10n + 100) = O(n^2)	

    O(4) = 1 : 항상 일정하다

    O(n): n개의 데이터를 입력 받아 저장한 후 각 데이터에 1씩 증가시킨 후 각 데이터를 화면에 출력하는 알고리즘의 시간복잡도 



#### + 왜 알고리즘의 성능 분석이 필요한가?

* 주어진 문제를 해결하기 위해 여러 개의 다양한 알고리즘이 가능 => 어떤 알고리즘을 사용해야하는가? 

* 많은 문제에서 성능 분석의 기준으로 알고리즘의 작업량을 비교

  ex. 1부터 100까지 합을 구하기 -> 100번의 연산(직접 더하기) vs 3번의 연산(공식 이용)

  

## 배열

> 일정한 자료형의 변수들을 하나의 이름으로 열거하여 사용하는 자료구조
>
> 여러 개의 변수 사용해야하는 경우 배열로 바꾸어 사용하자

### 배열의 필요성

* 프로그램 내에서 여러 개의 변수가 필요할 때, 일일이 다른 변수명을 이용하여 자료에 접근하는 것은 매우 비효율적일 수 있다.
* 배열을 사용하면 하나의 선언을 통해서 둘 이상의 변수를 선언할 수 있다.
* 단순히 다수의 변수 선언을 의미하는 것이 아니라, 다수의 변수로는 하기 힘든 작업을 배열을 활용해 쉽게 할 수 있다.



### 1차원 배열

#### 1차원 배열의 선언

* 별도의 선언 방법이 없으면 변수에 처음 값을 할당할 때 생성

* 이름: 프로그램에서 사용할 배열의 이름

  * Arr = list()	Arr = [ ]

    Arr = [1,2,3] # 선언과 초기화를 동시에. 크기 정해진 배열을 쓸 때 속도가 더 빠를 때가 있다.

    Arr = [0] * 10

#### 1차원 배열의 접근

* Arr[idx] = n #배열 Arr의 idx번 원소에 n을 저장하라



## 정렬

> 2개 이상의 자료를 특정 기준(키: 자료를 정렬하는 기준이 되는 특정 값)에 의해 작은 값부터 큰 값(오름차순, ascending) 혹은 그 반대의 순서대로(내림차순, descending) 재배열하는 것



### 대표적인 정렬 방식의 종류

* 버블 정렬
* 카운팅 정렬
* 선택 정렬
* 퀵 정렬
* 삽입 정렬
* 병합 정렬



### 버블 정렬

> 인접한 두 개의 원소를 비교하며 자리를 계속 교환하는 방식
>
> 선택 정렬과 헷갈리지 말자

#### 정렬 과정

* 첫 번째 원소부터 인접한 원소끼리 계속 자리를 교환하면서 맨 마지막 자리까지 이동한다
* 한 단계가 끝나면 가장 큰 원소가 마지막 자리로 정렬된다
* 교환하며 자리를 이동하는 모습이 물 위에 올라오는 거품 모양과 같다고 하여 버블 정렬이라고 한다.

#### 시간 복잡도

* O(n^2) 

  cf. O(n^2) & O(n^3): 좀 걸리겠네... / O(2^n): 오래 걸리겠네...

#### 과정

* 첫번째 패스

  나에게 주어진 idx 범위 확인. 리스트의 요소개수가 N개라면, 0번부터 n-1번까지 있다.

  비교할 기준 위치는 0에서 n-2까지(비교 원소의 왼쪽 idx)

* 2번째 패스 ~

  배열을 해야할 애가 하나 줄었다.(구간의 끝이 변함) 나머지 요소 중에 제일 큰 요소 찾으면 된다.


```python
def BubbleSort(a, N):			#정렬할 배열과 배열의 크기
    for i in range(N-1, 0, -1):	#i: 정렬될 구간의 끝
        for j in range(0, i):	#비교할 원소 중 왼쪽 원소의 인덱스
            if a[j] > a[j+1]:	#왼쪽 원소가 더 크면 오른쪽 원소와 교환
                a[j], a[j+1] = a[j+1], a[j]
```



### 카운팅 정렬

> 항목들의 순서를 결정하기 위해 집합에 각 항목이 몇 개씩 있는지 세는 작업을 하여, 선형 시간에 정렬하는 효율적인 알고리즘

#### 제한 사항

* 정수나 정수로 표현할 수 있는 자료에 대해서만 적용 가능: 각 항목의 발생 회수를 기록하기 위해, 정수 항목으로 인덱스 되는 카운트들의 배열을 사용하기 때문이다.

  * cf. 음수의 경우 idx를 shift 시켜서(=일정한 수를 더해서), 소수의 경우 일정한 수를 곱해서 사용한다.

    ​	 일정 범위를 넘어가면 이를 사용하지 않는다. 연산 과정에서 오차가 발생하는 문제도 존재.

* 카운트들을 위한 충분한 공간을 할당하려면 집합 내의 가장 큰 정수를 알아야 한다.

* 배열의 요소 100만개까지 괜찮다

#### 시간 복잡도

* O(n+k): n은 리스트 길이, k는 정수의 최대값

#### 과정

* 1단계: Data에서 각 항목들의 발생 회수를 세고, 정수 항목들로 직접 인덱스 되는 카운트 배열 counts에 저장한다. (counts[i]: i의 발생횟수)
* 2단계: 정렬된 집합에서 각 항목의 앞에 위치할 항목의 개수를 반영하기 위해 counts의 원소를 조정한다. (누적합으로 바꿔준다.)

* 3단계~: 결과리스트의 (counts의 (Data의 요소)번째 요소)번째 인덱스로 추가한 후 counts의 (Data의 요소)번째 요소를 1을 빼준다.

  => 제일 작은것부터 count의 요소만큼씩 출력하면 된다.

  

#### 알고리즘

```python
def Counting_Sort(A, B, k):
    #리스트 A: 입력 배열(1 ~ k)
    #리스트 B: 정렬된 배열
    #리스트 C: 카운트 배열
    C = [0] * (k + 1)
    for i in range(0, len(A)):
        C[A[i]] += 1
    for i in range(1, len(C)):
        C[i] += C(i-1)
    for i in range (len(B)-1, -1,-1):
        C[A[i]] -= 1
        B[C[A[i]]] = A[i]
      
```



#### 정렬 알고리즘 비교

| 알고리즘    | 평균 수행시간 | 최악 수행시간 | 알고리즘 기법 | 비고                                                |
| ----------- | ------------- | ------------- | ------------- | --------------------------------------------------- |
| 버블 정렬   | O(n^2)        | O(n^2)        | 비교와 교환   | 코딩이 가장 손쉽다.                                 |
| 카운팅 정렬 | O(n+k)        | O(n+k)        | 비교환 방식   | n이 비교적 작을 때만 가능하다.                      |
| 선택 정렬   | O(n^2)        | O(n^2)        | 비교와 교환   | 교환의 회수가 버블, 삽입정렬보다 작다.              |
| 퀵 정렬     | O(n log n)    | O(n^2)        | 분할 정복     | 최악의 경우 O(n^2)이지만, 평균적으로는 가장 빠르다. |
| 삽입 정렬   | O(n^2)        | O(n^2)        | 비교와 교환   | n개의 개수가 작을 때 효과적이다.                    |
| 병합 정렬   | O(n log n)    | O(n log n)    | 분할 정복     | 연결리스트의 경우 가장 효과적인 방식                |



## 완전 검색

> 문제의 해법으로 생각할 수 있는 모든 경우의 수를 나열해보고 확인하는 기법(Brute-force 혹은 generate-and-test 기법)
>

* 모든 경우의 수를 테스트한 후, 최종 해법을 도출한다. 일반적으로 경우의 수가 상대적으로 작을 때 유용
* 모든 경우의 수를 생성하고 테스트하기 때문에 수행 속도는 느리지만, 해답을 찾아내지 못한 확률이 작다.
* 주어진 문제를 풀 때, 우선 완전 검색으로 접근하여 해답을 도출한 후, 성능 개선을 위해 다른 알고리즘을 사용하고 해답을 확인하는 것이 바람직



#### 순열

> 서로 다른 것들 중 몇 개를 뽑아서 한 줄로 나열하는 것

* 서로 다른 n개 중 r개를 택하는 순열은 nPr= n*(n-1)*....(n-r+1)=n! / (n-r)!
* nPn = n!(팩토리얼)=n*(n-1)*...*1

* ex. {1,2,3}을 포함하는 모든 순열을 생성하는 함수
  * 동일한 숫자가 포함되지 않았을 때, 각 자리 수 별로 loop을 이용해 아래와 같이 구현할 수 있다.

```python
for i1 in range(1, 4):
    for i2 in range(1, 4):
        if i2 != i1:
            for i3 in range(1,4):
                if i3 ! = i1 and i3 ! = i2:
                    print(i1,i2,i3)
```



## 그리디

> 최적해를 구하는 데 사용되는 근시안적인 방법

* 여러 경우 중 하나를 결정해야 할 때마다 그 순간에 최적이라고 생각되는 것을 선택해나가는 방식으로 진행하여 최종적인 해답에 도달한다.

* 각 선택의 시점에서 이루어진 결정은 지역적으로는 최적이지만, 그 선택들을 계속 수집하여 최종적인 해답을 만들었다고 하여, 그것이 최적이라는 보장은 없다.

* 일반적으로, 머릿속에 떠오르는 생각을 검증 없이 바로 구현하면 Greedy 

  

#### 동작 과정

1. 해 선택: 현재 상태에서 부분 문제의 최적 해를 구한 뒤, 이를 부분해 집합(Solution Set)에 추가한다.
2. 실행 가능성 검사: 새로운 부분해 집합이 실행 가능한지를 확인한다. 곧, 문제의 제약 조건을 위반하지 않는지를 검사한다.
3. 해 검사: 새로운 부분해 집합이 문제의 해가 되는지를 확인한다. 아직 전체 문제의 해가 완성되지 않았다면, 1)의 해 선택부터 다시 시작한다.



## 배열: 2차원 배열

### 선언

- 1차원 List를 묶어놓은 List

- 2차원 이상의 다차원 List는 차원에 따라 Index를 선언

- 2차원 List의 선언: 세로길이(행의 개수), 가로길이(열의 개수)를 필요로 함

- Python 에서는 데이터 초기화를 통해 변수선언과 초기화가 가능함

  ex. [[0,1,2,3] [[4,5,6,7]]: 2행 4열의 2차원 List

```python
'''
3
1 2 3 
4 5 6
7 8 9
'''
N = int(input())
arr = [list(map(int, input().split())) for _ in range[N]]
#split(' ')	이렇게 하면 빈칸이 하나일 때를 기준으로 split.
#split() 	이렇게 하면 빈칸을 기준으로 split

'''
3
123 
456
789
'''
N = int(input())
arr = [list(map(int, input())) for _ in range[N]]
```

###  배열의 접근

* 배열 순회: nxm 배열의 nxm 개의 모든 원소를 빠짐없이 조사하는 방법

```python
arr = [[1]*3]*4	#arr = [[1,1,1],[1,1,1],[1,1,1],[1,1,1]]
arr[0][1] = 0	#arr = [[1,0,1],[1,0,1],[1,0,1],[1,0,1]] => 얕은복사되어서 그렇다!!
#해결방법
arr=[[0]*3 for -  in range(4)]	#[[0,0,0],[0,0,0],[0,0,0],[0,0,0]]
arr[0][0]=1		#[[1,0,0],[0,0,0],[0,0,0],[0,0,0]]

#행 우선 순회	i: 행의 좌표	j: 열의 좌표
for i in range(n):		#모든 행 i
    for j in range(m):	#각 행의 모든 열 j
        arr[i][j]	#필요한 연산 수행

#열 우선 순회
for j in range(m):
    for i in range(n):
        arr[i][j]
        
#지그재그 순회 처음엔 오른쪽으로 읽어나가고, 다음엔 왼쪽으로 읽어나가고, 다음엔 오, 그리고 왼...
for i in range(n):
    for j in range(m):
        arr[i][j+(m-1-2*j)*(i%2)]#[j] 또는 [m-1-j]
        
#델타를 이용한 2차 배열 탐색: 2차 배열의 한 좌표에서 4방향의 인접 배열 요소를 탐색하는 방법
#다양하게 활용할 수 있다. 주변 8칸 모두 출력, 한칸 떨어진 주변 출력 등등
#우 0 하 1 좌2 상3 => 0번은 오른쪽으로만 한칸(0,1),1번은 아래로 한칸(1,0) ...
#방법1
di = [0,1,0,-1]
dj = [1,0,-1,0]
for k in range(4):
    ni = i+di[k]
    nj = j+dj[k]
    if 0<=ni<N  and 0<=nj<M:	#유효 인덱스
        arr[ni][nj]
#방법2
arr=[[1,2,3], [4,5,6], [7,8,9]]	#주위 원소 출력
N=3
for i in range(N):
    for j in range(N):
        for di, dj in [(0,1), (1,0), (0,-1), (-1,0)]:
            ni = i+di
            nj = j+dj
            if 0<=ni<N  and 0<=nj<M:	#유효 인덱스
                print(i,j, arr[ni][nj])
        print()    
'''
0 0 2
0 0 4

0 1 3
0 1 5
0 1 1

0 2 6
0 2 2 ...
'''

#전치행렬 대각선(y=-x) 기준으로 뒤집기
arr = [[1,2,3],[4,5,6],[7,8,9]]
for i in range(3):
    for j in range(3):
        if i < j:
            arr[i][j], arr[j][i] = arr[j][i],arr[i][j]
```

```python
#입력받은 배열 주위를 0으로 채우기
arr1 = [0]*N +arr + [list(map(int, input().split())) for _ in range[N]]+ [0]*N
#N=2	[0, 0, [1,2,3], [4,5,6], [7,8,9], 0, 0]
#N=3	[0, 0, 0, [1,2,3], [4,5,6], [7,8,9], 0, 0, 0]
arr2 = [[0]*(N+2)] + [[0]+list(map(int, input().split()))+[0] for _ in range[N]] + [[0]*(N+2)]
# N=3 [[0,0,0,0,0],[0,1,2,3,0],[0,4,5,6,0],[0,7,8,9,0]]
```



## 부분집합 생성

- 부분집합 합(Subset sum) 문제

  - 유한 개의 정수로 이루어진 집합이 있을 때,  이 집합의 부분집합 중에서 그 집합의 원소를 모두 더한 값이 0이 되는 경우가 있는지를 알아내는 문제

    => 완전검색 기법으로 부분집합 합 문제를 풀기 위해서는, 우선 집합의 모든 부분집합을 생성한 후에 각 부분집합의 합을 계산해야 한다.

- 부분집합의 수: 집합의 원소가 n개일 때, 공집합을 포함한 부분집합의 수는 2^n개이다. 이는 각 원소를 부분집합에 포함시키거나 포함시키지 않는 2가지 경우를 모든 원소에 적용한 경우의 수와 같다.

```python
#각 원소가 부분집합에 포함되었는지를 loop 이용하여 확인하고 부분집합을 생성하는 방법
bit = [0,0,0,0]
for i in range(2):
    bit[0] = i						#0번째 원소
    for j in range(2):
        bit[1] = j					#1번째 원소
        for k in range(2):
            bit[2] = k				#2번째 원소
            for l in range(2):
                bit[3] = l			#3번째 원소
                print(bit)			#생성된 부분집합 출력
```



## 비트연산자

- 비트연산자

  | 연산자 | 의미                                                         |
  | ------ | ------------------------------------------------------------ |
  | &      | 비트 단위로 AND 연산을 한다.                                 |
  | \|     | 비트 단위로 OR 연산을 한다.                                  |
  | ^      | 비트 단위로 exclusive or 연산을 한다.                        |
  | <<     | 피연산자의 비트 열을 왼쪽으로 이동시킨다. <br />맨 오른쪽은 0이 채움. 제일 왼쪽에 있던 것은 out |
  | >>     | 피연산자의 비트 열을 오른쪽으로 이동시킨다. <br />맨 왼쪽은 0이 채움. 제일 오른쪽에 있던 것은 out |

- << 연산자

  - 1<<n: 2^n. 즉, 원소가 n개일 경우의 모든 부분집합의 수를 의미

    ex. 1<<5 : 5번 비트가 1인 값 

- & 연산자

  - i & (1<<j):  i의 j번째 비트가 1인지 아닌지 검사한다.
    - 1<<j: j번 비트만 1이 된다.
    - 1이면 연산의 결과가 0이 아니고, 0이면 0이 나온다.



+) 8bit =1byte. 상태구분할 수 있는 최소 단위는 bit(0/1. 이진수).  memory에 접근을 하는 최소단위는 byte
    제일 작은 번호 LSB(제일 오른쪽) 큰쪽은 MSB(제일 왼쪽). 비트연산은 같은 번호의 비트끼리만 연산.

변수 단위 안에서 비트로 쪼개진다고 생각

```python
#비트 연산자를 사용하여 부분집합 생성하기
arr = [3,6,7,1,5,4]
n = len(arr)							#n: 원소의 개수
for i in range(1<<n):					#n=6이므로 [0, 1, 2, ..., 62, 63]
    for j in range(n):					#원소의 수만큼 비트를 비교
        if i&(1<<j):					#i의 j번 비트가 1인 경우
            print(arr[j], end=', ')		#j번 원소 출력
    print()
print()
```

## 검색

- 저장되어 있는 자료중에서 원하는 항목을 찾는 작업
- 목적하는 탐색 키를 가진 항목을 찾는 것
  - 탐색 키(search key): 자료를 구별하여 인식할 수 있는 키
- 검색의 종류
  - 순차 검색(sequential search)
  - 이진 검색(binary  search)
  - 해쉬(hash)

###  순차 검색

- 일렬로 되어있는 자료를 순서대로 검색하는 방법

  - 가장 간단하고 직관적인 검색 방법
  - 배열이나 연결 리스트 등 순차구조로 구현된 자료구조에서 원하는 항목을 찾을 때 유용
  - 알고리즘이 단순하여 구현이 쉽지만,검색 대상의 수가 많은 경우에는 수행시간이 급격히 증가 -> 비효율적임

- 2가지 경우

  - 정렬되어 있지 않은 경우

    - 검색 과정
      - 첫번째 원소부터 순서대로 검색 대상과 키 값이 같은 원소가 있는지 비교하며 찾는다.
      - 키 값이 동일한 원소를 찾으면 그 원소의 인덱스를 반환한다.
      - 자료구조의 마지막에 이를 때까지 검색 대상을 찾지 못하면 검색 실패
    - 찾고자 하는 원소의 순서에 따라 비교회수가 결정됨
      - 첫번째 원소를 찾을 때는 1번 비교, 두 번째 원소를 찾을 때는 2번 비교
      - 정렬되지 않은 자료에서의 순차 검색의 평균 비교 회수는?
        - (1/n)*(1+2+3+...+n) = (n+1)/2
      - 시간복잡도  O(n)

    ```python
    #and 연산자는 앞이 거짓이면 뒤에 검사 안하고 거짓이라고 판단함. 
    #인덱스 범위 검사하고 원소가 맞는지 확인하자 
    ```

  - 정렬되어 있는 경우

    - 검색 과정
      - 자료가 오름차순으로 정렬된 상태에서 검색을 실시한다고 가정하자
      - 자료를 순차적으로 검색하면서 키 값을 비교하며, 원소의 키 값이 검색 대상의 키 값보다 크면 찾는 원소가 없다는 것이므로, 더 이상 검색하지 않고 검색을 종료한다. 
    - 찾고자 하는 원소의 순서에 따라 비교회수가 결정됨
      - 정렬이 되어있으므로, 검색 실패를 반환하는 경우 평균 비교 회수가 반으로 줄어든다.
      - 시간복잡도: O(n)

### 이진검색

- 자료의 가운데에 있는 항목의 키 값과 비교하여 다음 검색의 위치를 결정하고 검색을 계속 진행하는 방법

  - 목적 키를 찾을 때까지 이진 검색을 순환적으로 반복 수행함으로써 검색 범위를 반으로 줄여가면서 보다 빠르게 검색을 수행함

- 이진 검색을 하기 위해서는 자료가 **정렬된 상태**여야 한다.

- 검색 과정

  - 자료의 중앙에 있는 원소를 고른다
  - 중앙 원소의 값과 찾고자 하는 목표 값을 비교한다
  - 목표 값이 중앙 원소의 값보다 작으면 자료의 왼쪽 반에 대해서 새로 검색을 수행하고, 크다면 자료의 오른쪽 반에 대해서 새로 검색을 수행한다
  - 찾고자 하는 값을 찾을 때까지 1~3의 과정을 반복한다.

- 시간복잡도: log n

- 구현

  - 검색 범위의 시작점과 종료점을 이용하여 검색을 반복 수행한다
  - 이진 검색의 경우, 자료에 삽입이나 삭제가 발생했을 때 배열의 상태를 항상 정렬 상태로 유지하는 추가 작업이 필요하다.

  ```python
  def binarySearch(a, N, key):
      start = 0
      end = N-1
      while start <= end:
          middle = (start+end)//2
          if a[middle] ==  key:	#검색 성공
              return true
          elif a[middle]  > key:
              end = middle -1
          else:
              start = middle +1
          return false
  
  #재귀함수 이용
  def binarySearch2(a, low, high, key):
      if low>high:	#검색 실패
          return False
      else:
          middle = (low + high)//2
          if key == a[middle]:	#검색 성공
              return True
          elif key<a[middle]:
              return binarySearch2(a, low, middle-1, key)
          elif a[middle] < key:
              return binarySearch2(a, middle+1, high, key)              
  ```



## 인덱스

- 인덱스라는 용어는 Database에서 유래했으며, 테이블에 대한 동작 속도를 높여주는 자료 구조를 일컫는다. Database 분야가 아닌 곳에서는 Look up table 등의 용어를 사용하기도 한다
- 인덱스를 저장하는데 필요한 디스크 공간은 보통 테이블을 저장하는데 필요한 디스크 공간보다 작다. 왜냐하면 보통 인덱스는 키-필드만 갖고 있고, 테이블의 다른 세부 항목들은 갖고 있지 않기 때문이다.
- 배열을 사용한 인덱스
  - 대량의 데이터를 매번 정렬하면, 프로그램의 반응은 느려질 수 밖에 없다. 이러한 대량 데이터의 성능 저하 문제를 해결하기 위해 배열 인덱스를 사용할 수 있다.

- 다음예에서 원본 데이터 배열과 별개로, 배열 인덱스를 추가한 예를 보여주고 있다
  - 원본 데이터에 데이터가 삽입될 경우 상대적으로 크기가 작은 인덱스 배열을 정렬하기 때문에 속도가 빠르다.



## *선택 정렬

- 주어진 자료들 중 가장 작은 값의 원소부터 차례대로 선택하여 위치를 교환하는 방식
  - 앞서 살펴본 셀렉션 알고리즘을 전체 자료에 적용한 것이다.
- 정렬과정
  - 주어진 리스트중에서 최소값을 찾는다
  - 그 값을 리스트의 맨 앞에 위치한 값과 교환한다
  - 맨 처음 위치를 제외한 나머지 리스트를 대상으로 위의 과정을 반복한다.

- 시간 복잡도: O(n^2)

```python
def SelecionSort(a[], n):
    for i in range(N-1):
        minIdx =i
        for j in range(i+1, N):
            if a[minIdx] > a[j]:
                minIdx =  j
            a[i], a[minidx] = a[minIdx], a[i]	#비교하고 바꿀 필요 x
```



## 셀렉션 알고리즘

- 저장되어 있는 자료로부터 k번째로 큰 혹은 작은 원소를 찾는 방법

  - 최소값, 최대값 혹은 중간값을 찾는 알고리즘을 의미하기도 한다

- 선택 과정

  - 정렬 알고리즘을 이용하여 자료 정렬하기
  - 원하는 순서에 있는 원소 가져오기

- k번째로 작은 원소를 찾는 알고리즘

  - 1번부터 k번째까지 작은 원소들을 찾아 배열의 앞쪽으로 이동시키고, 배열의 k번째를 반환한다.
  - k가 비교적 작을 때 유용하며 O(kn)의 수행시간을 필요로 한다.
    - k가 크면 전체 정렬 속도가 빠른 것을 쓰는게 낫다.

  ```python
  def select(arr, k):
      for i in range(0, k):
          minIndex = i
          for j in range(i+1, len(arr)):
              if arr[minIndex] > arr[j]:
                  minIndex = J
          arr[i], arr[minindex] = arr[minIndex], arr[i]
      return arr[k-1]
  ```

  

## 정렬 알고리즘 비교

| 알고리즘    | 평균 수행시간 | 최악 수행시간 | 알고리즘 기법 | 비고                                                      |
| ----------- | ------------- | ------------- | ------------- | --------------------------------------------------------- |
| 버블 정렬   | O(n^2)        | O(n^2)        | 비교와 교환   | 코딩이 가장 손쉽다.                                       |
| 카운팅 정렬 | O(n+k)        | O(n+k)        | 비교환 방식   | n이 비교적 작을 때만 가능하다.                            |
| 선택 정렬   | O(n^2)        | O(n^2)        | 비교와 교환   | 교환의 회수가 버블, 삽입정렬보다 작다.                    |
| 퀵 정렬     | O(n log n)    | O(n^2)        | 분할 정복     | 최악의 경우 O(n^2)이지만, <br />평균적으로는 가장 빠르다. |
| 삽입 정렬   | O(n^2)        | O(n^2)        | 비교와 교환   | n의 개수가 작을 때 효과적이다.                            |
| 병합 정렬   | O(n log n)    | O(n log n)    | 분할 정복     | 연결리스트의 경우 가장 효율적인 방식                      |




