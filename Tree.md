## Tree
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
  - Full Binary Tree 정 이진 트리 : 모든 노드가 0개 또는 2개의 자식 노드를 가지고 있다.
  - Complete Binary Tree 완전 이진 트리 : 마지막 레벨 전레벨까지 꽉 차 있어야 되고 마지막 레벨은 왼쪽부터 차있어야 된다.
  - Perfect Binary Tree 포화 이진 트리 : 모든 레벨이 빠짐없이 다 차있어야 된다.
  
  - Tree를 배열로 구현 하려면 완전 이진 트리여야만 한다.
  - 완전 이진 트리 배열
  ```
  complete_binary_tree = [None, 1, 5, 12, 11, 9, 10, 14, 2, 10]
  ```
  - 완전 이진 트리 배열에서 왼쪽 자식 노드를 찾는 방법 : 부모 노드 인덱스 X 2
  - 완전 이진 트리 배열에서 오른쪽 자식 노드를  찾는 방법 : 부모 노드 인덱스 X 2 + 1
```
def get_parent_index(complete_binary_tree, index):
    parent_index = index // 2
    
    if 0 < parent_index < len(complete_binary_tree):
        return parent_index
        
    return None


def get_left_child_index(complete_binary_tree, index):
    left_child_index = 2 * index
    
    if 0 < left_child_index < len(complete_binary_tree):
        return left_child_index
        
    return None


def get_right_child_index(complete_binary_tree, index):
    right_child_index = 2 * index + 1
    
    if 0 < right_child_index < len(complete_binary_tree):
        return right_child_index
        
    return None

root_node_index = 1

tree = [None, 1, 5, 12, 11, 9, 10, 14, 2, 10

left_child_index = get_left_child_index(tree, root_node_index)
right_child_index = get_right_child_index(tree,root_node_index)

print(tree[left_child_index])
print(tree[right_child_index])

parent_index = get_parent_index(tree, 9)

print(tree[parent_index])

parent_index = get_parent_index(tree, 1)
print(parent_index)

left_child_index = get_left_child_index(tree, 6)
print(left_child_index)

right_child_index = get_right_child_index(tree, 8)
print(right_child_index)
```
  - 트리 순회 : 주로 재귀 함수 사용
  - 기본 동작들 : 
    - 재귀적으로 왼쪽 부분 트리 순회
    - 재귀적으로 오른쪽 부분 트리 순회
    - 현재 노드 데이터를 출력한다
  - Pre-order 순회:
    - 현재 노드 데이터를 출력한다
    - 재귀적으로 왼쪽 부분 트리 순회
    - 재귀적으로 오른쪽 부분 트리 순회
  - Post-order 순회:
    - 재귀적으로 왼쪽 부분 트리 순회
    - 재귀적으로 오른쪽 부분 트리 순회
    - 현재 노드 데이터를 출력한다
  - In-order 순회:
    - 재귀적으로 왼쪽 부분 트리 순회
    - 현재 노드 데이터를 출력
    - 재귀적으로 오른쪽 부분 트리 순회
```
# In-order Example
class Node:

    def __init__(self, data):
        self.data = data
        self.left_child = None
        self.right_child = None

def traverse_inorder(node):
    if node is None:
        return None
    else:
        traverse_inorder(node.left_child)
        print(node.data)
        traverse_inorder(node.right_child)
        


node_A = Node("A")
node_B = Node("B")
node_C = Node("C")
node_D = Node("D")
node_E = Node("E")
node_F = Node("F")
node_G = Node("G")
node_H = Node("H")
node_I = Node("I")

node_F.left_child = node_B
node_F.right_child = node_G

node_B.left_child = node_A
node_B.right_child = node_D

node_D.left_child = node_C
node_D.right_child = node_E

node_G.right_child = node_I

node_I.left_child = node_H

root_node = node_F

traverse_inorder(root_node)
```
