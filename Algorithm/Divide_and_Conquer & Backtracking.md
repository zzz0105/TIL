# 분할정복 & 백트래킹

## 분할정복

- 설계전략
  - 분할(Divide): 해결할 문제를 여러 개의 작은 부분으로 나눈다
  - 정복(Conquer): 나눈 작은 문제를 각각 해결한다
  - 통합(Combine): 필요하다면, 해결된 해답을 모은다
- Top-down 방식

### 거듭제곱

- 반복 알고리즘 활용 시 시간 복잡도: O(n)
- 분할 정복 기반의 알고리즘: O(log n)

### 병합 정렬(Merge Sort)

- 여러 개의 정렬된 자료의 집합을 병합하여 한 개의 정렬된 집합으로 만드는 방식
- 외부 정렬의 기본이 되는 정렬 알고리즘
- 분할 정복 알고리즘 활용. top-down 방식
- 시간 복잡도: O(n logn)
- 과정
  - 분할단계: 전체 자료 집합에 대하여 최소 크기의 부분집합이 될때까지 분할 작업을 계속한다
  - 병합단계: 2개의 부분집합을 <u>정렬하면서</u> 하나의 집합으로 병합. 비교해서 작은 쪽을 택함
- 분할할 때마다 메모리 추가로 사용. 병합 시에는 분할하면서 만들어놓았던 메모리에 사용하면 된다

```python
#분할 단계
def mergeSort(arr):
    if len(arr)==1:
        return arr
    left, right = [], []
    middle = len(arr)//2
    for x in range(middle):
        left.append(x)
    for x in range(middle,len(arr)):
        right.append(x)
    left = mergeSort(left)
    right = mergeSort(right)
    return merge(left, right)
    
#병합 단계
def merge(left, right):
    result = []
    while len(left) > 0 or len(right) > 0:
        if len(left) > 0 and len(right) > 0:
            if left[0]<=right[0]:
                result.append(left.pop(0))
            else:
                result.append(right.pop(0))
        elif len(left)>0:
            result.append(left)
        elif len(right)>0:
            result.append(right)
	return result
```

### 퀵 정렬

- 주어진 배열을 두 개로 분할하고, 각각을 정렬한다
- 매우 큰 입력 데이터에 대해서 좋은 성능을 보이는 알고리즘
- 병합 정렬과 다른 점
  - 퀵정렬은 분할 할 때, pivot(기준) 중심으로, 이보다 작은 것은 왼편, 큰 것은 오른편에 위치시킨다.
  - 각 부분 정렬이 끝난 후, 병합 정렬은 후처리 작업(병합)이 필요하지만, 퀵정렬은 필요로 하지 않는다.
- 과정
  - 피봇 선택: 왼쪽 끝, 오른쪽 끝, 임의의 세개 값 중에 중간 값 
  - i는 왼쪽에서 시작하여 피봇 값보다 큰 요소를, j는 오른쪽에서 시작하여 피봇값보다 작은 요소을 찾는다. 찾은 후에 i,j가 가리키고 있는 요소의 자리를 교환시킨다.
  - i와 j가 교차하면 i, j는 피봇을 기준으로 작은 값과 큰 값들의 경계에 위치한다.
  - 새로 생긴 왼쪽/오른쪽 집합에서 퀵 정렬 수행

```python
#1 Hoare-Partition 알고리즘
#Lomuto partition 알고리즘보다 빠르다
def partition(arr, l, r):
    p = arr[l]	#피봇 값
    i = l
    j = r
    while i<=j:	#교차하기 전까지 
        while i<j and arr[i]<=p:
            i+=1
        while i<j and arr[j]>=p:
            j-=1
        #i는 피봇보다 작은 애 중에 가장 오른쪽에 있는 요소를 가리킴
        #j는 피봇보다 큰 애 중에 가장 왼쪽에 있는 요소를 가리킴
        if i<j:	 
            arr[i],arr[j] = arr[j],arr[i]
    arr[l],arr[j] = arr[j],arr[l]	#피봇의 자리를 j로 잡아준다~
    return j

#2 Lomuto-partition 알고리즘
def partition(arr,p,r):
    x = arr[r]
    i = p-1
    for j in (p,r):
        if arr[j]<=x:
            i+=1
            arr[i],arr[j] = arr[j], arr[i]
        arr[i+1],arr[r] = arr[r], arr[i+1]
        return i+1
    
#quicksort
def quickSort(arr, l, r):
    if l<r:
        s = partition(a,l,r)
        quickSort(arr,l,s-1)
        quickSort(arr,s+1,r)
```

### 이진 검색(Binary Search)

- 자료의 가운데에 있는 항목의 **키 값과 비교**하여 **다음 검색의 위치를 결정**하고 검색을 계속 진행하는 방법.
  - 목적 키를 찾을 때까지 이진 검색을 순환적으로 반복 수행함으로써 **검색 범위를 반으로 줄여가면서** 보다 빠르게 검색을 수행함
- 이진 검색을 하기 위해서는 **자료가 정렬된 상태**여야 한다
- 과정
  1. 자료의 중앙에 있는 원소 고른다
  2. 중앙 원소의 값과 찾고자 하는 값을 비교
  3. 중앙 원소의 값보다 작다면 왼쪽에 있는 원소들에 대해 새로 검색을 수행한다. 크다면 오른쪽 반에 대해 새로 검색 수행
  4. 찾을 때까지 반복

```python
#반복 활용
def binarySearch(arr, k):	#k는 찾을 요소 
    low = 0
    n = len(arr)
    high = n-1
    while low<=high:
        mid = low + (high-low)//2
        if arr[mid] == key:
            return mid
        elif s[mid]>key:
            high = mid-1
        else:
            low = mid + 1
    return -1

#재귀 활용
def binarySearch(arr, low, high, key):
    if low>high:
        return -1
    else:
        mid = (low+high)//2
        if key == arr[mid]:
            return mid
        elif key<arr[mid]:
            return binarySearch(arr, low, mid-1, key)
        else:
            return binarySearch(arr, mid+1, high, key)  
```