# 220125 

## 2차원 리스트

```python
numbers=[[1, 2, 3], [4, 5, 6]]			#[[1, 4],[2, 5], [3, 6]] 출력하자
#방법1
result=[]
for i in range(len(numbers[0])):		#긴 것부터 돌린다
    num_lst=[]							
    for j in range(len(numbers)):		
        num_lst.append(numbers[j][i])	#열과 행을 바꾸어 num_lst에 넣는다
        if j == len(numbers)-1:			#j가 끝에 도달할 때
            result.append(num_lst)  	#num_lst에 있는 것을 result에 넣는다.
print(result)

#방법2
list(zip(*numbers))
```



## 리스트 컴프리헨션으로 정사각형 넓이 구하기

```python
list1 = [1,2,3]
list2 = [2,3,4]
print(list(i*j for i in list1 for j in list2 if i == j))
```



## word count

```python
#포인트: 딕셔너리
#요소를 순회하며 key가 없으면 키를 추가하고, 있으면 value를 추가한다.
result = {}
for blood_type in blood_types:
    if blood_type in result:		#딕셔너리에 키가 있으면
        result[blood_type] += 1
    else:					    	#딕셔너리에 키가 없으면:
        result[blood_type] = 1

#get(이것, 없을 때의 초기값)
result = {}
for blood_type in blood_types:
    result[blood_type] = result.get(blood_type, 0) + 1
```



## 중복구하기

```python
#방법1 set 사용
def duplicated_letters(input_str):
    input_letters = list(input_str)
    result = []

    for letter in input_letters:
        if input_letters.count(letter) > 1:
            result.append(letter)

    return list(set(result))

#방법2
result = []
for char in word:
    if word.count(char) > 1 and char not in result:
        # 만약에 여러번 등장했다면, 그리고 char가 result 통에 없다면
        result.append(char)
```



## 소문자-대문자

```python
def low_and_up(word):
    result=''
    letters = list(word)
    for i in range(len(letters)):
        if i%2: #홀수일 때 대문자
            result+=letters[i].upper()
        else:   #짝수일 때 소문자
            result+=letters[i].lower()
    return result
```

* upper(), lower() 못쓴다면 아스키코드 떠올리기... 너무 복잡하게 생각하지 말자!!



## 솔로천국만들기

```python
def lonely(num_list):
    alone = [num_list[0]]
    for i in range(1, len(num_list)):
        if num_list[i] != num_list[i-1]:
            alone.append(num_list[i])
    print(alone)
```

* 같으면 겹치는 것을 삭제 => 안겹치는 것을 추가한다로 생각하는 게 훨씬 간단.