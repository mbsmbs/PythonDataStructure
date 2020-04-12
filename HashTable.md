 ## Hash Table
 
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
