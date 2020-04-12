## 9. 이진 탐색 트리 (Binary Search Tree)

  - Set, Dictionary를 만들 수 있다.
  - Root노드를 기준으로 왼쪽은 Root보다 작은수 오른쪽은 큰수.
```
# Binary Search Tree
class Node:
    def __init__(self, data):
        self.data = data
        self.parent = None
        self.left_child = None
        self.right_child = None
        
class BinarySearchTree:
    def __init__(self):
        self.root = None
```
```
# 탐색
# Binary Search Tree의 데이터를 순서대로 출력
def print_inorder(node):
    """주어진 노드를 in-order로 출력해주는 함수"""
    if node is not None:
        print_inorder(node.left_child)
        print(node.data)
        print_inorder(node.right_child)

class BinarySearchTree:
    def __init__(self):
        self.root = None
        
    def print_sorted_tree(self):
        print_inorder(self.root
```
  - 이진 탐색 트리 삽입 : 삽입 이후에도 속성이 유지되어야 함
