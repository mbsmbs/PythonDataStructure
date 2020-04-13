## Heap
  - 2 가지 조건:
    - 형태 속성 : 완전 이진 트리 (Complete binary tree)
    - 힙 속성 : 모든 부모노드의 데이터는 자식노드들의 데이터보다 크거나 같다
  - 힙을 만드는 데 걸리는 시간 복잡도 : O(n x logn)
```
def swap(tree, index_1, index_2):
    temp = tree[index_1]
    tree[index_1] = tree[index_2]
    tree[index_2] = temp


def heapify(tree, index, tree_size):      // 힙 속성이 충족되지 못했을때 heapify!
    left_child_index = 2 * index
    right_child_index = 2 * index + 1
    
    largest = index

    if 0 < left_child_index < tree_size and tree[largest] < tree[left_child_index]:
        largest = left_child_index

    if 0 < right_child_index < tree_size and tree[largest] < tree[right_child_index]:
        largest = right_child_index
    
    if largest != index:
        swap(tree, index, largest)
        heapify(tree, largest, tree_size)
    
tree = [None, 15, 5, 12, 14, 9, 10, 6, 2, 11, 1]
heapify(tree, 2, len(tree))
print(tree) 
```
  - Heap Sort : O(nlg(n))
    - 힙을 만든다                            // O(n x log n) 
    - root와 마지막을 바꿔준다                // O(1)
    - 바뀐 마지막 노드는 없는 노드로 취급      // O(log n)
    - 새로운 Root노드를 Heapify.             // O(n x log n)
```
def heapsort(tree):
    tree_size = len(tree)

    for index in range(tree_size, 0, -1):
        heapify(tree, index, tree_size)         # Heapify
        
    for i in range(tree_size-1, 0, -1):
        swap(tree, 1, i)                        # Swap Root & Last 
        heapify(tree, 1, i)                     # heapify new Root

data_to_sort = [None, 6, 1, 4, 7, 10, 3, 8, 5, 1, 5, 7, 4, 2, 1]
heapsort(data_to_sort)
print(data_to_sort)
```

  - 우선순위 큐(Priority Queue): 추상 자료형
    - 힙을 이용하면 효율적으로 구현할 수 있다
    - 데이터가 우선순위 순서대로 나온다.
  - 힙에 데이터 삽입:
    - 힙의 마지막 인덱스에 데이터를 삽입
    - 부모 노드의 데이터와 비교후  부모 데이터가 더 작으면 Swap
```
# Heap insert example
def swap(tree, index_1, index_2):
    temp = tree[index_1]
    tree[index_1] = tree[index_2]
    tree[index_2] = temp


def reverse_heapify(tree, index):
    parent_index = index // 2 
    if 0 < parent_index < len(tree) and tree[index] > tree[parent_index]:
        swap(tree, index, parent_index)
        reverse_heapify(tree, parent_index)

class PriorityQueue:
    def __init__(self):
        self.heap = [None]


    def insert(self, data):
        self.heap.append(data)
        reverse_heapify(self.heap, len(self.heap)-1)

    def __str__(self):
        return str(self.heap)


priority_queue = PriorityQueue()

priority_queue.insert(6)
priority_queue.insert(9)
priority_queue.insert(1)
priority_queue.insert(3)
priority_queue.insert(10)
priority_queue.insert(11)
priority_queue.insert(13)

print(priority_queue)
```
  - 힙에서 최고 우선순위 데이터 추출:
    - Root 노드의 마지막 노드를 서로 바꿈
    - 마지막 노드의 데이터를 변수에 저장
    - 마지막 노드를 삭제
    - Root 노드에 Heapify를 호출해서 망가진 힙 속성을 고친다
    - 따로 저장해둔 데이터를 리턴
```
class PriorityQueue:
    def __init__(self):
        self.heap = [None]

    def insert(self, data):
        self.heap.append(data
        reverse_heapify(self.heap, len(self.heap)-1)

    def extract_max(self):
        swap(self.heap, 1, len(self.heap) - 1
        max_value = self.heap.pop()
        heapify(self.heap, 1, len(self.heap))
        return max_value

    def __str__(self):
        return str(self.heap)
        
priority_queue = PriorityQueue()

priority_queue.insert(6)
priority_queue.insert(9)
priority_queue.insert(1)
priority_queue.insert(3)
priority_queue.insert(10)
priority_queue.insert(11)
priority_queue.insert(13)

print(priority_queue.extract_max())
print(priority_queue.extract_max())
print(priority_queue.extract_max())
print(priority_queue.extract_max())
print(priority_queue.extract_max())
print(priority_queue.extract_max())
print(priority_queue.extract_max())
```
  - 힙의 삽입 시간 복잡도 : O(lg(n))
  - 힙의 추출 시간 복잡도 : O(lg(n))
  
  - 우선순위 큐를 힙 말고도 사용할 수 있는 자료구조:
    - 정렬된 동적 배열
      - 삽입 : O(n)     추출 : O(1)
    - 정렬된 더블리 링크드 리스트
      - 삽입 : O(n)     추출 : O(1)
  - 우선순위 큐를 만들때 자료구조 선택 팁:
    - 힙 : 새로운 데이터를 삽입할 일이 많으면
    - 동적 배열 or 더블리 링크드 릿트: 기존 데이터를 추출할 일이 더 많으면
