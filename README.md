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
