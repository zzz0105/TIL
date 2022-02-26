# Queue

- 삽입, 삭제의 위치 제한적  : 삽입은 큐의 뒤에서, 삭제는 큐의 앞에서만 이루어진다.

- 선입선출구조(FIFO First In Fist Out)

  - 큐에 삽입한 순서대로 원소가 저장되어 가장 먼저 삽입된 원소는 가장 먼저 삭제 된다.

  - Index

    - 머리(Front): 저장된 원소 중 첫번째 원소(또는 삭제된 위치)
    - 꼬리(Rear): 저장된 원소 중 마지막 원소

  - 큐의 주요 연산

    - enQueue(item): 삽입
    - deQueue(): 삭제
    - createQueue(0: 공백상태의 큐 생성
    - isEmpty(): 큐가 공백상태인지 확인
    - isFull(): 포화상태인지
    - Qpeek(): 앞쪽에서 원소를 삭제없이 반환

  - 연산 과정

    1. 공백 큐 생성: createQueue()

       - front와 rear의 위치를 -1로 둔다.(초기값)
         - front: 마지막으로 삭제된 위치
         - rear: 마지막으로 저장된 위치

    2. 원소 A 삽입: enQueue(A)

       - rear 1 증가시키고 rear가 가르키는 자리에 원소 삽입

    3. 원소 A 삽입: enQueue(B)

       - rear 1 증가시키고 rear가 가르키는 자리에 원소 삽입

    4. 원소 반환/삭제: deQueue()

       - front  1 증가시키고 front가 가르키는 자리의 원소를 꺼냄

    5. 원소 반환/삭제: deQueue()

       - front  1 증가시키고 front가 가르키는 자리의 원소를 꺼냄

       - 삽입 삭제가 같은 횟수 진행됨 => front와 rear가 같은 곳을 가르킨다. => 큐가 비어있다.

## 큐의 구현

### 선형큐

- 1차원 배열을 이용한 큐
  
- 큐의 크기 =배열의 크기
  
- 상태 표현
  - 초기상태: front = rear = -1
  - 공백상태:  front == rear
  - 포화상태: rear == n-1 (n: 배열의 크기)
  
- 초기 공백 큐 생성: 크기 n인 1차원 배열 생성. front=rear=-1

- 삽입: enQueue(item)

  - 마지막 원소 뒤에 새로운 원소 삽입

  ```python
  def enQueue(item):
      global rear
      if isFull(): print('Queue_Full')
      else:
          rear += 1
          Q[rear] = item
  ```

- 삭제: deQueue

  - 가장 앞에 있는 원소 삭제
  - 실제로 제거되는 것은 아님

  ```python
  def deQueue():
      if isEmpty(): print('Queue_Empty')
      else:
          front += 1
          return Q[front]
  ```

- 공백상태 및 포화상태 검사: isEmpty(),isFull()

  - 공백상태: front == rear
  - 포화상태: rear == n-1

  ```python
  def isEmpty():
      return front==rear
  def Full():
      return rear==len(Q)-1
  ```

- 검색: Qpeek

  - 가장 앞에 있는 원소를 검색하여 반환
  - front 한자리 뒤에 있는 원소. 큐의 첫번째에 있는 원소

  ```python
  def Qpeek():
      if is Empty(): print('Queue Empty')
      else: return Q[front+1]
  ```

- 선형 큐 이용 시 문제점
  - 잘못된 포화상태 인식
    - 삽입과 삭제는 계속할 경우 배열의 앞부분에 활용할 수 있는 공간이 있으나 포화상태로 인식해 더 이상 삽입 수행x
  - 해결방법1
    - 연산이 이루어질 때마다 저장된 원소들을 배열의 앞부분으로 모두 이동 => 원소 이동에 많은 시간이 소요되어 큐의 효용성이 급격히 떨어짐
  - 해결방법2
    - 1차원 배열을 사용하되 논리적으로 배열의 처음과 끝이 연결되어 원형 형태의 큐를 이룬다고 가정하고 사용

### 원형큐

- 초기 공백 상태 

  - front=rear=0

- Index의 순환

  - front와 rear의 위치가 배열의 마지막 인덱스인 n-1을 가리킨 후, 그 다음에는 논리적 순환을 이루어 배열의 처음 인덱스인   0으로 이동
  - 이를 위해 나머지 연산자 mod 사용. rear =  (rear+1)%len(Q)

- front 변수

  - 공백 상태와 포화상태 구분을 위해 front가 가리키는 자리는 비워둔다

- 삽입 위치 및 삭제 위치

  |        | 삽입 위치                  | 삭제 위치                    |
  | ------ | -------------------------- | ---------------------------- |
  | 선형큐 | rear += 1                  | front += 1                   |
  | 원형큐 | rear = (rear + 1) % len(Q) | front = (front + 1) % len(Q) |

- 연산 과정

  1. create Queue
     - front=rear=0 
     - 예시로 크기가 4인 Queue 만들었다고 가정
  2. enQueue(A)
     - rear 1 증가( (rear + 1) % len(Q) 연산의 결과). 그 자리에 A를 삽입.
  3. enQueue(A)
     - rear 1 증가( (rear + 1) % len(Q) 연산의 결과). 그 자리에 B를 삽입.
  4. deQueue()
     - front 1 증가. 그 자리의 요소 읽어옴.
  5. enQueue(C)
     - rear 1 증가( (rear + 1) % len(Q) 연산의 결과). 그 자리에 C를 삽입.
  6. enQueue(D)
     - rear 1 증가( (rear + 1) % len(Q) 연산의 결과). 그 자리에 D를 삽입.
     - 현재 가득찬 상태

#### 원형 큐의 구현

- 공백상태 및 포화상태 검사: isEmpty(), isFull()

  - 공백상태: frot == rear
  - 포화상태: 삽입한 rear의 다음 위치 == 현재 front
    - (rear+1) % len(Q) == front

  ```python
  def isEmpty():
      return front==rear
  def isFull():
      return (rear+1) % len(Q) == front
  ```

- 삽입: enQueue

  ```python
  def enQueue(item):
      global rear
      if isFull():
          print('Queue Full')
      else:
          rear = (rear+1) % len(Q)
          Q[rear] = item
  ```

- 삭제: deQueue(), delete()

  ```python
  def deQueue():
      global front
      if isEmpty():
          print('Queue Empty')	#디버깅 용도
      else:
          front = (front+1)%len(Q)
          return Q[front]
  ```

  

### 우선순위 큐

- 특징
  - 우선순위를 가진 항목들을 저장하는큐
  - FIFO 순서가 아닌 우선순위가 높은 순서대로 먼저 나가게 된다
- 구현(실제로는 트리 사용)
  - 배열 활용
    - 원소를 삽입하는 과정에서 우선순위를 비교하여 적절한 위치에 삽입
    - 가장 앞에 최고 우선순위의 원소 위치
    - 문제점
      - 배열을 사용하므로 삽입이나 삭제 연산이 일어날 때 원소의 재배치 발생 => 소요되는 시간이나 메모리 낭비
  - 리스트 활용
- 기본 연산
  - 삽입: enQueue
  - 삭제: deQueue



## 큐의 활용 : 버퍼

- 버퍼
  - 데이터를 한 곳에서 다른 한 곳으로 전송하는 동안 **일시적으로 그 데이터를 보관**하는 메모리의 영역
  - 버퍼링: 버퍼를 활용하는 방식 또는 버퍼를 채우는 동작
- 버퍼의 자료구조
  - 버퍼는 일반적으로 <u>입출력 및 네트워크와 관련된 기능</u>에서 이용
  - 순서대로 입력>출력>전달되어야 하므로 FIFO 방식의 자료구조인 **큐**가 활용됨
- 키보드 버퍼
  - 사용자 키보드 입력> 키보드 입력 버퍼> 키보드 입력 버퍼에 Enter 키 입력이 들어오면 프로그램 실행 영역에서 실행 영역



## BFS

- 탐색 시작점의 인접한 정점들을 먼저 모두 차례로 방문한 후에, 방문했던 정점을 시작점으로 하여 다시 인접한 정점들을 차례로 방문하는 방식

  - 인접한 정점들에 **탐색**을 한 후, **차례로 다시 너비 우선 탐색을 진행**해야하므로, 선입선출 형태의 자료 구조인 **큐**를 활용

  ```python
  def BFS(G, v):				#그래프 G, 탐색 시작점 v
      #준비과정
      visited = [0] * (n+1)	#정점의 개수 n
      queue = []				#큐 생성
      queue.append(v)			#시작점 enQueue 
      
      #처리과정
      while queue:			#queue가 비어있지 않을 때
          t = queue.pop()	    #dequeue
          if not visited[t]:	#방문 안했던 곳이라면 방문한 것으로 표시
              visited[t] = True
              visit(t)		#방문해서 할 일 처리
          for i in G[t]:		#t와 연결된 모든 정점에 대해 방문되지 않았던 곳이면 enQueue
              if not visited[i]:
                  queue.append(i)
  ```

- 연산과정

  1. 초기 상태

     - Visited 배열 초기화
     - Q 생성(append,   pop 사용할 것이라면 크기 안정해도 됨)
     - 시작점 enQueue

  2. A점부터 시작

     - deQueue A
     - A 방문한 것으로 표시
       - visited=[T,F,F,F,F,F,F,F,F]
     - A의 인접점 enQueue
       - Q=[B,C,D, , , , , ]

  3. 탐색 진행 1

     - deQueue B
     - B 방문한 것으로 표시
       - visited=[T,T,F,F,F,F,F,F,F]
     - B의 방문하지 않은 인접점 enQueue
       - Q=[C,D,E,F, , , , ]

  4. 탐색 진행 2

     - deQueue C
     - C 방문한 것으로 표시
       - visited=[T,T,T,F,F,F,F,F,F]
     - C의 방문하지 않은 인접점 enQueue
       - Q=[D,E,F, , , , ,]

  5. 탐색진행 3...

     - deQueue D
     - D 방문한 것으로 표시
       - visited=[T,T,T,T,F,F,F,F,F]
     - D의 방문하지 않은 인접점 enQueue
       - Q=[E,F, G, H, I, , ,]

  6. 탐색진행8

     - deQueue I

     - I 방문한 것으로 표시
       - visited=[T,T,T,T,T,T,T,T,T]

     - I의 방문하지 않은 인접점 enQueue
       - Q=[ ,  , , , , , , ]
     - Q가 비어있으므로 탐색 끝

  

- 그래프가 순환하게 되면 방문검사 시 큐에 중복되어 append되는 문제 발생

  - 중복(ex. A-BCD / B-CEF)이 얼마나 나올지 모르기 때문에 Queue의 크기 지정하기 어렵다

  - 해결방안

    - visited에 방문했던 요소 대신 몇 번 그룹(거리가 같은 정점들의 모임)인지에 대한 정보를 넣는다.

      - 출발지를 1번 그룹으로보고, 1번 그룹에 인접한 요소는 2번 그룹, ..., n번 그룹에 인접한 요소는 n+1번 그룹. 
      - 3번 그룹에 의해 왔다 -> visited에 4 저장

    - 인접이면서 줄 안서있는 애만 올려~! while문 전에 올리기

      =>중복x. Q 크기 결정 쉬워진다. if 문 빠져서 간단해짐

    ```python
    def BFS(G, v, n):			#그래프 G, 탐색 시작점 v
        visited = [0] * (n+1)	#정점의 개수 n
        queue = []				#큐 생성
        queue.append(v)			#시작점 enqueue
        visited[v] = 1			
        while queue:			#큐가 비어있지 않은 경우
            t = queue.pop(0)	#dequeue
            visit(t)			#방문해서 할 일 처리
            for i in G[t]:		#t와 연결된 모든 정점에 대해 방문되지 않았던 곳이라면 enqueue
                if not visited[i]:
                    queue.append(i)
                    visited[i]=visited[t]+1	
    ```

    


- DFS로 최단거리 구할 수 있다. 돌 수 있다. 특징은 갈 수 있는 모든 애들 다 가본다. return 횟수가 더 많다. 한번 가본 곳을 또 가야되는 상황 => 목적에 따라 선택해야된

