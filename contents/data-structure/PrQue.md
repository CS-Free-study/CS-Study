# 우선순위 큐 (Priority Queue)
> 힙(Heap)을 통해 구현되며 FIFO(First In First Out)인 Queue와는 다르게 우선순위가 높은 데이터가 먼저 나가는 형태의 자료구조이다.

<br>

## 힙(Heap)
> 완전이진트리로 최댓값, 최솟값 탐색이 빠르다

 * 이진탐색트리(BST)와는 다르게 중복된 값이 허용된다
 * 최대 힙(Max Heap): 부모 노드의 키 값이 자식 노드보다 크거가 같은 완전이진트리
 * 최소 힙(Min Heap): 부모 노드의 키 값이 자식 노드보다 작거나 같은 완전이진트리

<br>

<img src = "./images/PrQue/Heap.png" width=400>
> 힙은 동적배열로 구현되며 완전이진트리기 때문에 그림과 같은 idx를 갖는다

<br>

 * idx 0은 root 노드를 의미한다
 * i번째 왼쪽 자식 노드의 idx: (i * 2) + 1
 * i번째 오른쪽 자식 노드의 idx: (i * 2) + 2
 * i번째 자식 노드의 root 노드 idx: (i / 2)
 * 원소 삽입/삭제: O(logn)
 * 원소 탐색: O(1)

<br>

### ***원소를 추가한 이후에 Heap을 만족시키기 위해서 정렬하는 과정이 존재한다***

<br>

``` cpp
int now = static_cast<int>(_heap.size()) - 1;
	// 루트 노드까지
	while (now > 0)
	{
	    // 부모 노드와 비교해서 더 작으면 패배
		int next = (now - 1) / 2;
		if (max(_heap[now], _heap[next]))
			break;

		// 데이터 교체
		::swap(_heap[now], _heap[next]);
		now = next;
		}
```

<br>


