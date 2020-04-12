## 추상화 (Abstract)
  - 기능 : 무엇
  - 구현 : 어떻게
  - 추상화 : 구현내용을 몰라도 기능만 보고도 무엇을 알게끔 해주면 추상화를 했다 할 수 있다.
  - 추상 자료형 : 자료 구조를 추상화 한 것, 데이터를 저장/사용할 때 기능만 생각
  - List (추상 자료형) : 기능
  - Dynamic Array, Linked List (자료구조) : 기능 + 구현
  - 추상 자료형을 먼저 생각하는 이유는 기능위주로 생각하면 코드의 흐름에 집중할 수 있다. 그리고나서 어떻게 구현할 것인지를 생각한다.
### List 구현 : 동적 배열 || 링크드 리스트 : Python -> 동적 배열
### Queue 구현 : 동적 배열 || 링크드 리스트 : Python -> Linked List : FIFO 가장 먼저 들얼온 데이터가 가장 먼저 삭제된다. 
### Deque 구현 : 동적 배열 || 링크드 리스트 : Python -> Doubly Linked List : 맨 앞과 뒤에 데이터를 삽입+삭제
```
# deque Example
# 서비스 센터 문의 처리

from collections import deque

class CustomerComplaint:
    def __init__(self, name, email, content):
        self.name = name
        self.email = email
        self.content = content
        
class CustomerServiceCenter:
    def __init__(self):
        self.queue = deque()
        
    def process_complaint(self):
       if self.queue:
          complaint = self.queue.popleft()
          print(f"{complaint.name}님의 {complaint.content} 문의 내용 접수 되었습니다. 담당자가 배정되면 {complaint.email}로 연락드리겠습니다!")
       else:
          print("더 이상 대기 중인 문의가 없습니다!")
    def add_complaint(self, name, email, content):
        new_complaint = CustomerComplaint(name, email, content):
        self.queue.append(new_complaint)
        
# 문의 접수한다
center.add_complaint("강영훈", "younghoon@codeit.com", "음식이 너무 맛이 없어요")

# 문의를 처리한다
center.process_complaint()
center.process_complaint()

# 문의 세 개를 더 접수한다
center.add_complaint("이윤수", "yoonsoo@codeit.kr", "에어컨이 안 들어와요...")
center.add_complaint("손동욱", "dongwook@codeit.us", "결제가 제대로 안 되는 거 같군요")
center.add_complaint("김현승", "hyunseung@codeit.ca", "방을 교체해주세요")

# 문의를 처리한다
center.process_complaint()
center.process_complaint()
  
```
### Stack 구현 : 동적 배열 || 링크드 리스트 : LIFO 가장 나중에 들어온 데이터가 먼저 삭제된다. : Python -> Stack X 대신 deque 사용 즉 Doubly Linked List
```

from collections import deque

def parentheses_checker(string):
    print(f"테스트하는 문자열: {string}")
    stack = deque() # 사용할 스택 정의

    for i in range(len(string)):
        if string[i] == "(":
            stack.append(i)
        if string[i] == ")":
            if stack:
                stack.pop()
            else:
                print(f"문자열 {i} 번째 위치에 있는 닫는 괄호에 맞는 열리는 괄호가 없습니다")

    while stack:
        print(f"문자열 {stack.pop()} 번째 위치에 있는 괄호가 닫히지 않았습니다")

case1 = "(1+2)*(3+5)"
case2 = "((3*12)/(41-31))"
case3 = "((1+4)-(3*12)/3"
case4 = "(12-3)*(56/3))"
case5 = ")1+14)/3"
case6 = "(3+15(*3"

parentheses_checker(case1)
parentheses_checker(case2)
parentheses_checker(case3)
parentheses_checker(case4)
parentheses_checker(case5)
parentheses_checker(case6)
```

### Dictionary or Map : No order, Key + Value : Python -> Hash Table
### Set : No order, Value : 구현은 원래 Key만 저장하는 것, Key = Value : Python -> Hash Table
