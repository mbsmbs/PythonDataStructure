 ## 1. Linked List

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
 ## 2. Doubly Linked List
 
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
