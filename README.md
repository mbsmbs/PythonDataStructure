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
