6203 국어, 영어, 수학의 총점

```python
class subject:   
	def __init__(self, k, e, m):
		self.k = k
		self.e = e
		self.m = m
	def total(self):
		return self.k + self.e + self.m

score1, score2, score3 = map(int, input().split(','))

student = subject(score1, score2, score3)

print("국어, 영어, 수학의 총점: %d" %(student.total()))
```



6223 원의 면적

```python
class Circle:
	def __init__(self, rad):
		self.rad = rad
	def area(self):
		return self.rad * self.rad * 3.14

ar = Circle(2)
print('원의 면적: %.2f'%(ar.area()))
```



6225 사각형의 면적

```python
class Rectangle:
  def __init__(self, wid, len):
    self.wid = wid
    self.len = len
  def area(self):
    return self.wid * self.len

ar = Rectangle(4, 5)
print(f'사각형의 면적: {ar.area()}')
```

