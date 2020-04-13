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


    def search(self, data):
        temp = self.root  # 탐색용 변수, root 노드로 초기화

        # 원하는 데이터를 갖는 노드를 찾을 때까지 돈다
        while temp is not None:
            # 원하는 데이터를 갖는 노드를 찾으면 리턴
            if data == temp.data:
                return temp
            # 원하는 데이터가 노드의 데이터보다 크면 오른쪽 자식 노드로 간다
            if data > temp.data:
                temp = temp.right_child
            # 원하는 데이터가 노드의 데이터보다 작으면 왼쪽 자식 노드로 간다
            else:
                temp = temp.left_child

        return None # 원하는 데이터가 트리에 없으면 None 리턴

    def insert(self, data):
        """이진 탐색 트리 삽입 메소드"""
        new_node = Node(data)  # 삽입할 데이터를 갖는 노드 생성

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

# 노드 탐색과 출력
print(bst.search(7).data)
print(bst.search(19).data)
print(bst.search(2).data)
print(bst.search(20))
```
```
# 가장 작은 노드를 찾자
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


    @staticmethod
    def find_min(node):
        """(부분)이진 탐색 트리의 가장 작은 노드 리턴"""
        # 코드를 쓰세요
        temp = node  # 도우미 변수. 파라미터 node로 초기화

        # temp가 node를 뿌리로 갖는 부분 트리에서 가장 작은 노드일 때까지 왼쪽 자식 노드로 간다
        while temp.left_child is not None:
            temp = temp.left_child      
    
        return temp  


    def search(self, data):
        """이진 탐색 트리 탐색 메소드, 찾는 데이터를 갖는 노드가 없으면 None을 리턴한다"""
        temp = self.root  # 탐색용 변수, root 노드로 초기화
    
        # 원하는 데이터를 갖는 노드를 찾을 때까지 돈다
        while temp is not None:
            # 원하는 데이터를 갖는 노드를 찾으면 리턴
            if data == temp.data:
                return temp
            # 원하는 데이터가 노드의 데이터보다 크면 오른쪽 자식 노드로 간다
            if data > temp.data:
                temp = temp.right_child
            # 원하는 데이터가 노드의 데이터보다 작으면 왼쪽 자식 노드로 간다
            else:
                temp = temp.left_child
    
        return None # 원하는 데이터가 트리에 없으면 None 리턴


    def insert(self, data):
        """이진 탐색 트리 삽입 메소드"""
        new_node = Node(data)  # 삽입할 데이터를 갖는 노드 생성

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

print(bst.find_min(bst.root).data)  # 전체 이진 탐색 트리에서 가장 작은 노드
print(bst.find_min(bst.root.right_child).data)  # root 노드의 오른쪽 부분 트리에서 가장 작은 노드
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

  - 이진 탐색 트리 삭제
    - 삭제하려는 노드에 먼저 접근해야 함
    - 경우 1 : 삭제하려는 데이터가 leaf노드의 데이터일때
    - 경우 2 : 삭제하려는 데이터 노드가 하나의 자식 노드만 있을때
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


          def delete(self, data):
              """이진 탐색 트리 삭제 메소드"""
              node_to_delete = self.search(data)  # 삭제할 노드를 가지고 온다
              parent_node = node_to_delete.parent  # 삭제할 노드의 부모 노드

              # 경우 1: 지우려는 노드가 leaf 노드일 때
              if node_to_delete.left_child is None and node_to_delete.right_child is None:
                  if self.root is node_to_delete:
                      self.root = None
                  else:  # 일반적인 경우
                      if node_to_delete is parent_node.left_child: 
                          parent_node.left_child = None
                      else:
                          parent_node.right_child = None

              # 경우 2: 지우려는 노드가 자식이 하나인 노드일 때:

              # 코드를 쓰세요
              elif node_to_delete.left_child is None:  # 지우려는 노드가 오른쪽 자식만 있을 때:
              # 지우려는 노드가 root 노드일 때
                  if node_to_delete is self.root:
                      self.root = node_to_delete.right_child
                      self.root.parent = None
                  # 지우려는 노드가 부모의 왼쪽 자식일 때
                  elif node_to_delete is parent_node.left_child:
                      parent_node.left_child = node_to_delete.right_child
                      node_to_delete.right_child.parent = parent_node
                  # 지우려는 노드가 부모의 오른쪽 자식일 때
                  else:
                      parent_node.right_child = node_to_delete.right_child
                      node_to_delete.right_child.parent = parent_node

              elif node_to_delete.right_child is None:  # 지우려는 노드가 왼쪽 자식만 있을 때:
                  # 지우려는 노드가 root 노드일 때
                  if node_to_delete is self.root:
                      self.root = node_to_delete.left_child
                      self.root.parent = None
                  # 지우려는 노드가 부모의 왼쪽 자식일 때
                  elif node_to_delete is parent_node.left_child:
                      parent_node.left_child = node_to_delete.left_child
                      node_to_delete.left_child.parent = parent_node
                  # 지우려는 노드가 부모의 오른쪽 자식일 때
                  else:
                      parent_node.right_child = node_to_delete.left_child
                      node_to_delete.left_child.parent = parent_node



          @staticmethod
          def find_min(node):
              """(부분)이진 탐색 트리의 가장 작은 노드 리턴"""
              # 코드를 쓰세요
              temp = node  # 탐색 변수. 파라미터 node로 초기화

              # temp가 node를 뿌리로 갖는 부분 트리에서 가장 작은 노드일 때까지 왼쪽 자식 노드로 간다
              while temp.left_child is not None:
                  temp = temp.left_child      

              return temp  


          def search(self, data):
              """이진 탐색 트리 탐색 메소드, 찾는 데이터를 갖는 노드가 없으면 None을 리턴한다"""
              temp = self.root  # 탐색 변수. root 노드로 초기화

              # 원하는 데이터를 갖는 노드를 찾을 때까지 돈다
              while temp is not None:
                  # 원하는 데이터를 갖는 노드를 찾으면 리턴
                  if data == temp.data:
                      return temp
                  # 원하는 데이터가 노드의 데이터보다 크면 오른쪽 자식 노드로 간다
                  if data > temp.data:
                      temp = temp.right_child
                  # 원하는 데이터가 노드의 데이터보다 작으면 왼쪽 자식 노드로 간다
                  else:
                      temp = temp.left_child

              return None # 원하는 데이터가 트리에 없으면 None 리턴


          def insert(self, data):
              """이진 탐색 트리 삽입 메소드"""
              new_node = Node(data)  # 삽입할 데이터를 갖는 노드 생성

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

        # 자식이 하나만 있는 노드 삭제
        bst.delete(5)
        bst.delete(9)

        bst.print_sorted_tree()
    ```

  
