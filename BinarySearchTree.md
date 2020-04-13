## 9. 이진 탐색 트리 (Binary Search Tree)

  - Set, Dictionary를 만들 수 있다.
  - 이진 탐색 트리 속성 : Root노드를 기준으로 왼쪽은 Root보다 작은수 오른쪽은 Root보다 큰수.
  - 배열이나 파이썬 리스트로 구현하지 않는다.
  
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
  - 이진 탐색 트리 탐색
    - 주어진 노드의 데이터와 탐색하려는 데이터 비교
    - 탐색하려는 데이터가 더 크면 노드의 오른쪽 자식으로 간다
    - 탐색하려는 데이터가 더 작으면 노드의 왼쪽 자식으로 간다
    - 탐색하려는 노드를 찾으면 리턴한다
```
# Binary Search Tree에 in-order 순회를 사용하면 데이터를 순서대로 출력
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
        print_inorder(self.root)
```
  - 이진 탐색 트리 삽입 : 삽입 이후에도 속성이 유지되어야 함   // O(h)
    - 새로운 노드 생성                           // O(1)
    - Root노드부터 비교하면서 저장할 위치 찾음    // O(h)   h = height
    - 찾은 위치에 새롭게 만든 노드 연결           // O(1)
```
class Node:
    """이진 탐색 트리 노드 클래스"""
    def __init__(self, data):
        self.data = data
        self.parent = None
        self.right_child = None
        self.left_child = None


def print_inorder(node):
    """주어진 노드를 in-order로 출력해주는 함수"""
    if node is not None:
        print_inorder(node.left_child)
        print(node.data)
        print_inorder(node.right_child)


class BinarySearchTree:
    """이진 탐색 트리 클래스"""
    def __init__(self):
        self.root = None


    def insert(self, data):
        new_node = Node(data)  # 삽입할 데이터를 갖는 새 노드 생성

        # 트리가 비었으면 새로운 노드를 root 노드로 만든다
        if self.root is None:
            self.root = new_node
            return

        # 코드를 쓰세요
        temp = self.root  # 저장하려는 위치를 찾기 위해 사용할 변수. root 노드로 초기화한다

        # 원하는 위치를 찾아간다
        while temp is not None:
            if data > temp.data:  # 삽입하려는 데이터가 현재 노드 데이터보다 크다면
                # 오른쪽 자식이 없으면 새로운 노드를 현재 노드 오른쪽 자식으로 만듦
                if temp.right_child is None:
                    new_node.parent = temp
                    temp.right_child = new_node
                    return
                # 오른쪽 자식이 있으면 오른쪽 자식으로 간다
                else:
                    temp = temp.right_child
            else:  # 삽입하려는 데이터가 현재 노드 데이터보다 작다면
                # 왼쪽 자식이 없으면 새로운 노드를 현재 노드 왼쪽 자식으로 만듦
                if temp.left_child is None:
                    new_node.parent = temp
                    temp.left_child = new_node
                    return
                # 왼쪽 자식이 있다면 왼쪽 자식으로 간다
                else:
                    temp = temp.left_child

    def print_sorted_tree(self):
        """이진 탐색 트리 내의 데이터를 정렬된 순서로 출력해주는 메소드"""
        print_inorder(self.root)  # root 노드를 in-order로 출력한다


# 빈 이진 탐색 트리 생성
bst = BinarySearchTree()

# 데이터 삽입
bst.insert(7)
bst.insert(11)
bst.insert(9)
bst.insert(17)
bst.insert(8)
bst.insert(5)
bst.insert(19)
bst.insert(3)
bst.insert(2)
bst.insert(4)
bst.insert(14)

# 이진 탐색 트리 출력
bst.print_sorted_tree()
```
