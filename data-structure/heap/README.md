# heap

> [참고링크: 임베디드쥰의 독서기록장](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=leeinje66&logNo=221622360256)

## 설명

- 특정한 우선순위에서 가장 신경쓰이는 하나를 가장 빨리 뽑아낼 수 있는 자료구조
- 탐색을 하기에는 적절치 않으나 해당 우선순위에서 가장 중요한 요소 하나를 찾기에는 최적화된 구조
- BST보다 삽입과 삭제 연산이 빠르다.
- 삽입/삭제에는 O(logN)이 걸린다.
- 배열이나 클래스로 구현할 수 있다.
- 우선순위, 힙정렬, 다익스트라, 프림 알고리즘을 구현할 때 사용

```python
class MaxHeap:

    def __init__(self):
        self.data = [None]

    def insert(self, item):
        self.data.append(item)
        i = len(self.data) - 1

        while i > 1:
            if self.data[i] > self.data[(i // 2)]:
                self.data[i], self.data[(i // 2)] = self.data[(i // 2)], self.data[i]
                i = i // 2
            else:
                break

    def remove(self):
        if len(self.data) > 1:
            self.data[1], self.data[-1] = self.data[-1], self.data[1]
            data = self.data.pop(-1)
            self.maxHeapify(1)
        else:
            data = None
        return data

    def maxHeapify(self, i):
        left = 2 * i
        right = (2 * i) + 1
        smallest = i
        # 왼쪽 자식이 존재하는지, 그리고 왼쪽 자식의 (키) 값이 (무엇보다?) 더 큰지를 판단합니다.
        if left < len(self.data) and self.data[i] < self.data[left]:
            # 조건이 만족하는 경우, smallest 는 왼쪽 자식의 인덱스를 가집니다.          
            smallest = left
        # 오른쪽 자식이 존재하는지, 그리고 오른쪽 자식의 (키) 값이 (무엇보다?) 더 큰지를 판단합니다.
        if right < len(self.data) and self.data[i] > self.data[right]:
            # 조건이 만족하는 경우, smallest 는 오른쪽 자식의 인덱스를 가집니다.
            smallest = right
        if smallest != i:
            # 현재 노드 (인덱스 i) 와 최댓값 노드 (왼쪽 아니면 오른쪽 자식) 를 교체합니다.
            self.data[i], self.data[smallest] = self.data[smallest], self.data[i]
            # 재귀적 호출을 이용하여 최대 힙의 성질을 만족할 때까지 트리를 정리합니다.
            self.maxHeapify(smallest)
```