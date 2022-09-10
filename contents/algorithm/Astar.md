# A*(AStar) 알고리즘
> 시작 노드와 목적지 노드를 분명하게 지정해 두 노드 간의 최단 경로를 파악하는 알고리즘

 * A* 알고리즘은 정확한 최단 경로 보다는 최단 경로의 `근사값`을 구한다
 * 현재 위치가 얼마나 좋은 위치인지 `적당한 휴리스틱 함수`를 통해 추정하여 점수를 매긴다
 * 정확한 정답을 포기한 대신 탐색 속도는 다익스트라에 비해 훨씬 빠르다

<br>

### ***다익스트라는 시작 노드로부터 모든 노드까지의 최단 경로를 구한다***

<br>

## 경로 채점
> 다음에 어떤 노드를 선택할지에 대한 채점이 이루어진다 

<br>

### F = G + H
 * F: 현재까지 이동하는데 걸린 비용과 예상 비용을 합친 총 비용
 * G: 시작점으로부터 현재 노드까지의 경로를 따라 이동하는데 소요되는 비용
 * H: 현재 노드로부터 목적지까지의 소요되는 예상 비용

<br>

### H(Heuristic) 휴리스틱
> 어림짐작, 주먹 구구식 등으로 불리며 경험에 기반하여 문제를 해결하거나 발견해내는 방법이다.

 * 어원은 그리스어 `Heutiskein`으로 찾아내다, 발견하다 라는 뜻이다

<br>

### ***휴리스틱이란 상황과 직관에 따라 행동하여 시행착오를 겪고 지식을 얻어 생각을 발전시키는 방법이다***

<br>

## 맨해튼 거리(Manhattan Distance)
> 각 좌표의 차를 모두 더한 것을 거리로 한다

<br>

<img src = "./images/Astar/Manhattan.png" width = 300>

<br>

### 맨해튼 거리는 다음과 같은 수식으로 거리를 구한다

<br>

* $|x1-x2| + |y1-y2|$

<br>

### 우리가 실생활에서 사용하는 거리는 `유클리드 거리`로 일반적으로 다음과 같이 거리를 구한다

<br>

* $\sqrt{(x1-x2)^2 + (y1-y2)^2}$

<br>


### A* Code
``` cpp
// 점수 매기기
	// F = G + H
	// F = 최종 점수 (작을 수록 좋음, 경로에 따라 달라짐)
	// G = 시작점에서 해당 좌표까지 이동하는데 드는 비용 (작을 수록 좋음, 경로에 따라 달라짐)
	// H = 목적지에서 얼마나 가까운지 (작을 수록 좋음, 고정)

	Pos start = _pos;
	Pos dest = _board->GetExitPos();

	enum
	{
		DIR_COUNT = 8
	};

	Pos front[] =
	{
		Pos { -1, 0},	// UP
		Pos { 0, -1},	// LEFT
		Pos { 1, 0},	// DOWN
		Pos { 0, 1},	// RIGHT
		Pos {-1, -1},	// UP_LEFT
		Pos {1, -1},	// DOWN_LEFT
		Pos {1, 1},		// DOWN_RIGHT
		Pos {-1, 1},	// UP_RIGHT
	};

	int32 cost[] =
	{
		10, // UP
		10, // LEFT
		10, // DOWN
		10, // RIGHT
		14,
		14,
		14,
		14
	};

	const int32 size = _board->GetSize();

	// ClosedList
	// close[y][x] -> (y, x)에 방문을 했는지 여부
	vector<vector<bool>> closed(size, vector<bool>(size, false));

	// best[y][x] -> 지금까지 (y, x)에 대한 가장 좋은 비용 (작을 수록 좋음)
	vector<vector<int32>> best(size, vector<int32>(size, INT32_MAX));

	// 부모 추적 용도
	map<Pos, Pos> parent;

	// OpenList
	priority_queue<PQNode, vector<PQNode>, greater<PQNode>> pq;

	// 1) 예약(발견) 시스템 구현
	// - 이미 더 좋은 경로를 찾았다면 스킵
	// 2) 뒤늦게 더 좋은 경로가 발견될 수 있음 -> 예외 처리 필수
	// - openList에서 찾아서 제거한다거나.
	// - pq에서 pop한 다음에 무시한다거나.
	
	// 초기값
	{
		int32 g = 0;
		int32 h = 10 * (abs(dest.y - start.y) + abs(dest.x - start.x));
		pq.push(PQNode{ g + h, g, start });
		best[start.y][start.x] = g + h;
		parent[start] = start;
	}

	while (pq.empty() == false)
	{
		// 제일 좋은 후보를 찾는다
		PQNode node = pq.top();
		pq.pop();

		// 동일한 좌표를 여러 경로로 찾아서\
		// 더 빠른 경로로 인해서 이미 방문(closed)된 경우 스킵
		// [선택]
		if (closed[node.pos.y][node.pos.x])
			continue;
		if (best[node.pos.y][node.pos.x] < node.f)
			continue;

		// 방문
		closed[node.pos.y][node.pos.x] = true;

		// 목적지에 도착했으면 바로 종료
		if (node.pos == dest)
			break;

		for (int32 dir = 0; dir < DIR_COUNT; dir++)
		{
			Pos nextPos = node.pos + front[dir];
			// 갈 수 있는 지역은 맞는지 확인
			if (CanGo(nextPos) == false)
				continue;
			// [선택] 이미 방문한 곳이면 스킵
			if (closed[nextPos.y][nextPos.x])
				continue;

			// 비용 계산
			int32 g = node.g + cost[dir];
			int32 h = 10 * (abs(dest.y - nextPos.y) + abs(dest.x - nextPos.x));
			// 다른 경로에서 더 빠른 길을 찾았으면 스킵
			if (best[nextPos.y][nextPos.x] <= g + h)
				continue;

			// 예약 진행
			best[nextPos.y][nextPos.x] = g + h;
			pq.push(PQNode{ g + h, g, nextPos });
			parent[nextPos] = node.pos;
		}
	}

	// 거꾸로 거슬러 올라간다
	Pos pos = dest;

	_path.clear();
	_pathIndex = 0;

	while (true)
	{
		_path.push_back(pos);

		// 시작점은 자신이 곧 부모이다
		if (pos == parent[pos])
			break;

		pos = parent[pos];
	}

	std::reverse(_path.begin(), _path.end());
```