# binary-search-tree

> [참고링크 션지니어 블로그](https://velog.io/@seanlion/bstimplementation)

## 이진 탐색 트리

- Array로 구현할 때 부모 자식 노드의 index 관계
    - 부모 인덱스가 i일 때 자식 (2*i , 2*i + 1)
    - 자식 인덱스가 i일 때 부모 인덱스 i // 2
- 노드가 왼쪽 자식과 오른쪽 자식만 갖는 트리
- 완전이진트리
    - 루트로부터 아래층까지 완전히 꽉찬 이진트리
- 이진탐색트리 조건
    - 왼쪽 자식 노드는 무조건 부모 노드보다 작은 수로 이루어져 있어야 한다.
    - 오른쪽 자식 노드는 무조건 부모 노드보다 큰 수로 이루어져 있어야 한다.
    - 같은 값을 갖는 노드는 없다.
- 전위/중위/후위 순회

```python
# 트리를 구성하는 노드 클래스
class Node:
    """생성자"""

    def __init__(self, key, value, left, right):
        self.key = key  # 키
        self.value = value  # 값
        self.left = left  # 왼쪽 자식 참조
        self.right = right  # 오른쪽 자식 참조


class BinarySearchTree():
    # 생성자
    def __init__(self) -> None:
        self.root = None  # 루트 설정

    # 검색하는 메소드
    def search(self, key) -> int:
        node = self.root  # 루트에 주목
        while True:
            if node is None:  # 더 이상 진행할 수 없으면
                return -1  # 검색 실패
            if key == node.key:  # key와 노드 p의 키가 같으면
                return node.value  # 검색 성공
            elif key < node.key:  # key가 작으면
                node = node.left  # 왼쪽 서브 트리에서 검색
            else:  # key가 작으면
                node = node.right  # 오른쪽 서브 트리에서 검색

    # 노드 추가하는 메소드
    def add(self, key, value) -> bool:
        # 노드 추가하는 내부 함수
        def add_node(node, key, value) -> None:
            # 탐색하고 적절한 자리에 삽입
            if key == node.key:  # 이미 삽입하려는 키가 있으면 false 처리
                return False
            # 삽입하려는 키가 현재 탐색 노드의 키보다 작다면
            elif key < node.key:
                # 그 탐색 노드의 왼쪽 자식이 없다면 바로 그 자리에 삽입
                if node.left is None:
                    node.left = Node(key, value, None, None)
                else:
                    # 자식이 있으면 재귀함수 호출로 한번 더 들어감
                    add_node(node.left, key, value)
            # 삽입하려는 키가 현재 탐색 노드의 키보다 크거나 같다면
            else:
                # 그 탐색 노드의 오른쪽 자식이 없다면 바로 그 자리에 삽입
                if node.right is None:
                    node.right = Node(key, value, None, None)
                else:
                    # 자식이 있으면 재귀함수 호출로 한번 더 들어감
                    add_node(node.right, key, value)
            return True

        # 루트가 없는 경우
        if self.root is None:
            self.root = Node(key, value, None, None)
            return True
        # 루트가 있는 경우
        else:  # 리턴값은 내부함수 리턴 값
            return add_node(self.root, key, value)

    # 노드 삭제하는 메소드
    def remove(self, key) -> bool:
        node = self.root  # 현재 노드로 지정
        parent = None  # 현재 노드의 부모 노드
        is_left_child = True  # node는 parent의 왼쪽 자식 노드인지 오른쪽 자식 노드인지 확인

        # 삭제할 노드 탐색
        while True:
            if node is None:
                return False
            if key == node.key:
                break
            else:
                parent = node
                if key < node.key:
                    node = node.left
                    is_left_child = True  # 왼쪽 자식 노드로 내려가니까 플래그를 True로 설정
                else:
                    node = node.right
                    is_left_child = False  # 오른쪽 자식 노드로 내려가니까 플래그를 True로 설정

        # 키를 찾은 뒤에 자식이 없는 노드이면 or 자식이 1개 있는 노드이면
        if node.left is None:  # 왼쪽 자식이 없으면
            if node is self.root:  # 만약 삭제 노드가 root이면, 바로 오른쪽 자식으로 대체한다.
                self.root = node.right
            # 아래의 parent는 탐색 시 찾은 노드의 바로 위 부모가 됨.(탐색 로직에서 그렇게 적용)
            # parent - node - node의 자식의 구도가 있으면 node라는 중간이 빠지기 때문에 parent의 자식과 node의 자식을 연결
            # (node의 자식이 없으면 자연스레 None이 들어감)
            elif is_left_child:  # 왼쪽 자식 노드가 있는 것이니까
                parent.left = node.right  # 부모의 왼쪽 참조가 오른쪽 자식을 가리킴
            else:  # 오른쪽 자식 노드가 있는 것이니까
                parent.right = node.right  # 부모의 오른쪽 참조가 오른쪽 자식을 가리킴

        elif node.right is None:  # 오른쪽 자식이 없으면
            if node is self.root:
                self.root = node.left  # 만약 삭제 노드가 root이면, 바로 왼쪽 자식으로 대체한다.
            elif is_left_child:
                parent.left = node.left  # 부모의 왼쪽 참조가 왼쪽 자식을 가리킴
            else:
                parent.right = node.left  # 부모의 오른쪽 참조가 왼쪽 자식을 가리킴

    # 노드 출력하는 메소드
    def dump(self):
        def print_subtree(node):
            # 전위 순회로 출력
            if node is not None:
                print(f'{node.key} {node.value}')
                print_subtree(node.left)
                print_subtree(node.right)

        root = self.root
        print_subtree(root)
```