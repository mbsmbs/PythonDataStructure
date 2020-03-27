# PythonDataStructure
study Data Structure with python

# I) 기본 자료형

 ## 1. 정적 배열 (static array)
 
  - 크기가 고정돼 있다.
  - 같은 타입의 데이터만 담을 수 있다.
  - 접근 : O(1)
  - 탐색 : O(n)
  
 ## 2. 동적 배열 (dynamic  array)
 
  - 정적 배열로 만들어진 자료 구조
  - 정적 배열의 크기를 상황에 맞게 조절한다.
  - 추가 연산 :
      - 정적 배열에 남는 공간이 있을때 O(1)
      - 정적 배열에 남는 공간이 없을때 O(n)
  - 삽입 연산 :
      - 정적 배열에 남는 공간이 있을때 O(n)
      - 정적 배열에 난는 공간이 없을때 O(n)
  - 공간 낭비 : O(n) -> 더 큰 배열을 만들때 O(n-2)가 낭비
   
 |        | static array | dynamic array |
 | ------ | ------------ | ------------- |
 | Access | O(1) | O(1) |
 | Search | O(n) | O(n) |
 | Insert | N/A | O(n) or O(1) |
 | Delete | N/A | O(n) or O(1) |
 
 ## 3. Linked List

  - 데이터를 순서대로 저장해준다.
  - 요소를 계속 추가할 수 있다.
  - 각 Node는 데이터와 다음노드를 가리킨다.
       ```
       class Node:
           def __init__(self, data):
               self.data = data
               self.next = None
       ```
  - Linked List는 이런 Node들을 이어준다.
       ```
       # 노드 생성
        head_node = Node(1)
        node_1 = Node(2)
        node_2 = Node(3)
        tail_node = Node(4)
        
       #노드 연결
        head_node.next = node_1
        node_1.next = node_2
        node_2.next = tail_node
        
       ```
 ## 4. Doubly Linked List
 
  - 일반 링크드 리스트에서 하나가 추가되는데 바로 전 노드도 가리킬 수 있다.
       ```
       class Node:
           def __init__(self, data):
               self.data = data
               self.next = None
               self.prev = None
       
       class DoublyLinkedList:
           def __init__(self):
               self.head = None
               self.tail = None
               
           def append(self, data):    // append data
               new_node = Node(data)
               
               if self.head is None:
                   self.head = new_node
                   self.tail = new_node
               else:
                   self.tail.next = new_node
                   new_node.prev = self.tail
                   self.tail = new_node
                   
           def insert_after(self, previous_node, data):
               new_node = Node(data)
               
               if previous_node is self.tail:
                   previous_node.next = new_node
                   new_node.prev = self.tail
                   self.tail = new_node
               else:
                   new_node.next = previous_node.next
                   new_node.prev = previous_node
                   previous_node.next.prev = new_node
                   previous_node.next = new_node
                   
           def prepend(self,data):
               new_node = Node(data)
               
               if self.head is None:
                   self.head = new_node
                   self.tail = new_node
               else:
                   self.head.prev = new_node
                   new_node.next = self.head
                   self.head = new_node
                   
           def delete(self, node_to_delete):
           
               if node_to_delete is self.head and node_to_delete is self.tail:
                   self.head = None
                   self.tail = None
               elif node_to_delete is self.head:
                   self.head = self.head.next
                   self.head.prev = None
               elif node_to_delete is self.tail:
                   self.tail = self.tail.prev
                   self.tail.next = None
               else:
                   node_to_delete.next.prev = node_to_delete.prev
                   node_to_delete.prev.next = node_to_delete.next
               
               
           def find_node_at(self, index):       // access
               iterator = self.head
               
               for _ in range(index):
                    iterator = iterator.next
               
               return iterator
           
           def find_node_with_data(self, data):   // Search
               iterator = self.head
               
               while iterator is not None:
                   if iterator.data == data
                       return iterator
                       
                   iterator = iterator.next
                   
               return None
               
           def __str__(self):    // output
               res = "|"
               
               iterator = self.head
               
               while iterator is not None:
                   res_Str += " {} |".format(iterator.data)
                   iterator = iterator.next
                   
               return res_str
       ```
  
   | Operations | Linked List |
   | ---------- | ----------- |
   | Access | O(n) |
   | Search | O(n) |
   | Insert | O(n+1) |
   | Delete | O(n+1) |

 ## 5 Hash Table
 
  - key & value
  - Hash Function : 특정 값을 원하는 범위의 자연수로 바꿔주는 함수
  
  1. 고정된 크기의 배열을 만든다.
  2. 해시 함수를 이용해서 key를 원하는 범위의 자연수로 바꾼다.
  3. 해시 함수 결과 값 인덱스에 key - value쌍을 저장한다.
  
  - 해시 함수를 만드는 2가지 간단한 방법:
   1. 나누기 :
        ```
        def hash_function_remainder(key, array_size):
            return key % array_size
        ```
        
   2. 곱하기 :
    - 먼저 0 < a < 1인 아무 값을 정하고
    - 그다음 a * key. 결과 값의 소수점만 남기고
    - 남겨진 소수점을 배열의 크기로 곱해준다.
        ```
        def hash_function_multiplication(key, array_size, a):
            temp = a * key
            temp -= int(temp)
            
            return int(array_size * temp)
        ```
   
  - Python 해시함수는 불변 타입 자료형에만 사용 가능 :
    - Boolean
    - int
    - float
    - tuple
    - string

  - 해시 충돌 : 다른 데이터가 같은 자리에
  - 충돌 해결법 : Chaining
    - LinkedList
         ```
         class Node:
             def __init__(self, key, value):
                 self.key = key
                 self.value = value
                 self.next = None
                 self.prev = None
                 
         class LinkedList:
             def __init__(self):
                 self.head = None
                 self.tail = None
                 
             def find_node_with_key(self, key):
                 iterator = self.head
                 
                 while iterator is not None:
                     if iterator.key == key:
                         return iterator
                         
                     iterator = iterator.next
                     
                 return None
                 
             def append(self, key, value):
                 new_node = Node(key, value)

                 if self.head is None:
                     self.head = new_node
                     self.tail = new_node
                 else:
                     self.tail.next = new_node
                     new_node.prev = self.tail
                     self.tail = new_node
                     
             def delete(self, node_to_delete):
             
                 if node_to_delete is self.head and node_to_delete is self.tail:
                     self.tail = None
                     self.head = None
                 elif node_to_delete is self.head:
                     self.head = self.head.next
                     self.head.prev = None                   
                 elif node_to_delete is self.tail:
                     self.tail = self.tail.prev
                     self.tail.next = None
                 else:
                     node_to_delete.prev.next = node_to_delete.next
                     node_to_delete.next.prev = node_to_delete.prev
         ```
  - 탐색
  
 | Operations | Hash Table |
 | ---------- | ----------- |
 | Hash Function | O(1) |
 | Access | O(1) |
 | Linked List Search | O(n) |
  
  - 삽입
  
 | Operations | Hash Table |
 | ---------- | ----------- |
 | Hash Function | O(1) |
 | Access | O(1) |
 | Linked List Search | O(n) |
 | Append or modify | O(1) |
  
  - 삭제
  
 | Operations | Hash Table |
 | ---------- | ----------- |
 | Hash Function | O(1) |
 | Access | O(1) |
 | Linked List Search | O(n) |
 | Linked List Delete | O(1) |
 
 ### Hash Table collision solution :
 #### Chaining with LinkedList
 ```
 class Node:
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.next = None
        self.prev = None 


 class LinkedList:
     def __init__(self):
         self.head = None
         self.tail = None


     def find_node_with_key(self, key):
         iterator = self.head

         while iterator is not None:
             if iterator.key == key:
                 return iterator

             iterator = iterator.next

         return None


    def append(self, key, value):
        new_node = Node(key, value)

        if self.head is None:
            self.head = new_node
            self.tail = new_node
        else:
            self.tail.next = new_node 
            new_node.prev = self.tail
            self.tail = new_node  


    def delete(self, node_to_delete):
        if node_to_delete is self.head and node_to_delete is self.tail:
            self.tail = None
            self.head = None
        elif node_to_delete is self.head:
            self.head = self.head.next
            self.head.prev = None
        elif node_to_delete is self.tail:
            self.tail = self.tail.prev
            self.tail.next = None
        else:
            node_to_delete.prev.next = node_to_delete.next
            node_to_delete.next.prev = node_to_delete.prev

        return node_to_delete.value


    def __str__(self):
        res_str = ""

        iterator = self.head

        while iterator is not None:
            res_str += "{}: {}\n".format(iterator.key, iterator.value)
            iterator = iterator.next

        return res_str
 ```
 ```
 class HashTable:
     def __init__(self, capacity):   
         self._capacity = capacity          // 용량 설정
         self._table = [LinkedList() for _ in range(self._capacity)]    // 설정 크기로 리스트생성 후 각 자리에 빈 링크드 리스트 생성

     def _hash_function(self, key):
         return hash(key) % self._capacity  // 용량 범위안의 정수 반환


     def _get_linked_list_for_key(self, key):
     
         hashed_index = self._hash_function(key)   // 반환된 정수값 가져와서 인덱스 값으로 설정

         return self._table[hashed_index]          // 해당 인덱스에 있는 링크드 리스트를 반환


     def _look_up_node(self, key):
         linked_list = self._get_linked_list_for_key(key)    // 해당 링크드 리스트를 가져오고
         return linked_list.find_node_with_key(key)          // 그 링크드 리스트 안에서 key값과 일치하는 노드를 찾아서 반환

     def look_up_value(self, key):
     
         return self._look_up_node(key).value                // key값에 해당하는 노드에 있는 value를 반환


     def insert(self, key, value):

         existing_node = self._look_up_node(key)                 // 해당 노드를 가져오고

         if existing_node is not None:                           // 찾는 key값에 해당하는 노드가 있다면
             existing_node.value = value                         // 그 노드에 있는 value를 바꾸고
         else:
             linked_list = self._get_linked_list_for_key(key)    // 없다면 해당 링크드 리스트를 가져와서
             linked_list.append(key, value)                      // 가져온 링크드 리스트에 추가한다.
             
     def delete_by_key(self, key):
        node_to_delete = self._look_up_node(key)              // 지울 노드를 찾고
        
        if node_to_delete is not None:                        // 빈노드가 아니라면
            linked_list = self._get_linked_list_for_key(key)  // 노드의 링크드 리스트를 가져와서
            linked_list.delete(node_to_delete)                // 해당 노드를 지운다.

     def __str__(self):
         res_str = ""

         for linked_list in self._table:
             res_str += str(linked_list)

         return res_str[:-1]
 ```

#### Open addressing

 - 충돌이 있을때 다른 비어있는 곳을 찾는다.
 - Linear Probing : 바로 다음것들이 비어있는지 하나씩 확인
 - Quadratic Probing : 제곱을 한 값들을 이용해서 인덱스를 찾습니다.
    - 1의 제곱은 1 : 11    못찾으면 다음
    - 2의 제곱은 4 : 15    못찾으면 다음
    - 3의 제곱은 9 : 24    이런식으로....
 - Insert, Search, Delete : O(n)
 
## 6. 추상화
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

## 7. Tree
  - Root node : 트리의 시작 노드
  - Parent Node
  - Child Node
  - Sibling Node : 같은 부모를 갖는 노드
  - Leaf Node : 자식이 없는 노드. 맨 밑 노드.
  - 깊이 : Root노드에서 떨어져 있는 거리.
  - Level : 깊이 + 1
  - 높이 : 트리에서 가장 깊이 있는 노드의 깊이.
  - 부분 트리 : 어떤 트리의 일부분.

### 이진 트리 (Binary Tree)
  - 각 노드는 최대 2개의 자식 노드를 가질 수 있는 트리.
```
# Binary Tree Example
class Node:
    def __init__(self, data):
            self.data = data
            self.left_child = None
            self.right_child = None


root_node = Node("A")
node_B = Node("B")
node_C = Node("C")
node_D = Node("D")
node_E = Node("E")
node_F = Node("F")
node_G = Node("G")
node_H = Node("H")

root_node.left_child = node_B
root_node.right_child = node_C

node_B.left_child = node_D
node_B.right_child = node_E
node_E.left_child = node_G
node_E.right_child = node_H

node_C.right_child = node_F


test_node = root_node.right_child.right_child    # Tests
print(test_node.data)

test_node = root_node.left_child.right_child.left_child
print(test_node.data)

test_node = root_node.left_child.right_child.right_child
print(test_node.data)
```
  - Full Binary Tree 정 이진 트리 : 모든 노드가 개 또는 2개의 자식 노드를 가지고 있다.
  - Complete Binary Tree 완전 이진 트리 : 마지막 레벨 전레벨까지 꽉 차 있어야 되고 마지막 레벨은 왼쪽부터 차있어야 된다.
  - Perfect Binary Tree 포화 이진 트리 : 모든 레벨이 빠짐없이 다 차있어야 된다.
  
  - Tree를 배열로 구현 하려면 완전 이진 트리여야만 한다.
```
def get_parent_index(complete_binary_tree, index):
    """배열로 구현한 완전 이진 트리에서 index번째 노드의 부모 노드의 인덱스를 리턴하는 함수"""
    # 코드를 쓰세요
    parent_index = index // 2
    
    if 0 < parent_index < len(complete_binary_tree):
        return parent_index
        
    return None


def get_left_child_index(complete_binary_tree, index):
    """배열로 구현한 완전 이진 트리에서 index번째 노드의 왼쪽 자식 노드의 인덱스를 리턴하는 함수"""
    # 코드를 쓰세요
    left_child_index = 2 * index
    
    if 0 < left_child < len(complete_binary_tree):
        return left_child_index
        
    return None


def get_right_child_index(complete_binary_tree, index):
    """배열로 구현한 완전 이진 트리에서 index번째 노드의 오른쪽 자식 노드의 인덱스를 리턴하는 함수"""
    # 코드를 쓰세요
    right_child_index = 2 * index + 1
    
    if 0 < right_child_index < len(complete_binary_tree):
        return right_child_index
        
    return None

# 실행 코드
root_node_index = 1 # root 노드

tree = [None, 1, 5, 12, 11, 9, 10, 14, 2, 10]  # 과제 이미지에 있는 완전 이진 트리

# root 노드의 왼쪽과 오른쪽 자식 노드의 인덱스를 받아온다
left_child_index = get_left_child_index(tree, root_node_index)
right_child_index = get_right_child_index(tree,root_node_index)

print(tree[left_child_index])
print(tree[right_child_index])

# 9번째 노드의 부모 노드의 인덱스를 받아온다
parent_index = get_parent_index(tree, 9)

print(tree[parent_index])

# 부모나 자식 노드들이 없는 경우들
parent_index = get_parent_index(tree, 1)  # root 노드의 부모 노드의 인덱스를 받아온다
print(parent_index)

left_child_index = get_left_child_index(tree, 6)  # 6번째 노드의 왼쪽 자식 노드의 인덱스를 받아온다
print(left_child_index)

right_child_index = get_right_child_index(tree, 8)  # 8번째 노드의 오른쪽 자식 노드의 인덱스를 받아온다
print(right_child_index)
```
