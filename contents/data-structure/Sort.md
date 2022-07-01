# 정렬 알고리즘

## 정렬 알고리즘이란?

n개의 숫자가 입력으로 주어졌을 때, 이를 사용자가 지정한 기준에 맞게 정렬하여 출력하는 알고리즘

<br>

## 정렬 알고리즘의 종류(기본 7가지)

### 선택 정렬(Selection Sort)

> 주어진 배열에서 최솟값을 찾고 배열의 가장 앞의 값과 위치를 바꾸면서 정렬하는 방식   
→ 배열의 최솟값을 찾아 `선택`하여 정렬하기 때문에 선택 정렬이라고 불림

<details>
  <summary> 알고리즘(ADL) </summary>
  <div markdown="0">

 ![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Selection_ADL.png)

  </div>
</details>

<details>
  <summary> 수행 과정(png) </summary>
  <div markdown="0">

 ![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Selection_Process.png)

  </div>
</details>

<details>
  <summary> 수행 과정(gif) </summary>
  <div markdown="0">

 ![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Selection.gif)

  </div>
</details>

- 장점
    - 구현이 간단하다.
    - 데이터를 하나씩 비교하기 때문에 정밀한 비교가 가능하다.
    - 비교하는 횟수에 비해 교환하는 횟수가 적다.
- 단점
    - 데이터를 하나씩 비교하기 때문에 시간이 오래걸린다.
    - 정렬된 상태에서 새로운 데이터가 추가되면 효율이 좋지 않다.
- 시간 복잡도
    - 평균: O(n^2)
    - 최선: O(n^2)
    - 최악: O(n^2)

---

### 버블 정렬(Bubble Sort)

> 서로 인접한 원소를 비교하여 앞의 값의 크기가 작도록 자리를 바꾸면서 정렬하는 방식   
→ 정렬 방식이 마치 물속에서 올라오는 `물방울`과 같기 때문에 버블 정렬이라고 불림

<details>
  <summary> 알고리즘(ADL) </summary>
  <div markdown="0">

 ![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Bubble_ADL.png) 

  </div>
</details>

<details>
  <summary> 수행 과정(png) </summary>
  <div markdown="0">

  ![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Bubble_Process.png)

  </div>
</details>

<details>
  <summary> 수행 과정(gif) </summary>
  <div markdown="0">

 ![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Bubble.gif)

  </div>
</details>

- 장점
    - 구현이 간단하다.
    - 데이터를 하나씩 비교하기 때문에 정밀한 비교가 가능하다.
- 단점
    - 데이터를 하나씩 비교하기 때문에 시간이 오래걸린다.
    - 순서에 맞지 않은 요소를 인접한 요소와 교환한다.
    - 큰 수가 앞에 있을수록 뒤로 이동하기 위해 많은 교환이 이루어진다.
    - 특정 요소가 최종 정렬 위치에 있어도 교환되는 일이 발생한다.
- 시간 복잡도
    - 평균: O(n^2)
    - 최선: O(n^2)
    - 최악: O(n^2)

---

### 삽입 정렬(Insertion Sort)

> 현재 위치의 원소를 정렬된 상태의 앞부분과 비교하여 적절한 위치에 삽입하면서 정렬하는 방식   
→ 원소를 배열의 적절한 위치로 `삽입`하기 때문에 삽입 정렬이라고 불림

<details>
  <summary> 알고리즘(ADL) </summary>
  <div markdown="0">

![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Insertion_ADL.png)

  </div>
</details>

<details>
  <summary> 수행 과정(png) </summary>
  <div markdown="0">

![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Insertion_Process.png)

  </div>
</details>

<details>
  <summary> 수행 과정(gif) </summary>
  <div markdown="0">

 ![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Insertion.gif)

  </div>
</details>

- 장점
    - 입력으로 들어오는 배열의 원소가 정렬되어 있을수록 속도가 빠르다.
    - 이미 정렬된 값은 교환이 일어나지 않는다.
- 단점
    - 삽입을 구현해야 하므로 속도가 자료구조의 영항을 많이 받는다. (삽입 후 앞 부분을 뒤로 이동시켜야 한다.)
    - 입력으로 들어오는 배열이 역순에 가까울수록 효율이 매우 떨어진다.
- 시간 복잡도
    - 평균: O(n^2)
    - 최선: O(n)
    - 최악: O(n^2)

---

### 합병 정렬(Merge Sort)

> 배열을 작은 단위로 쪼개어 정렬한 결과를 합치면서 전체를 정렬하는 방식   
→ 쪼갠 후 `합병`하면서 정렬하기 때문에 합병 정렬이라고 불림

<details>
  <summary> 알고리즘(ADL) </summary>
  <div markdown="0">

![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Merge_ADL1.png)
    
![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Merge_ADL2.png)
    
  </div>
</details>

<details>
  <summary> 수행 과정(png) </summary>
  <div markdown="0">

![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Merge_Process.png)

  </div>
</details>

<details>
  <summary> 수행 과정(gif) </summary>
  <div markdown="0">

 ![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Merge.gif)

  </div>
</details>
    
- 장점
    - 항상 일정한 시간 복잡도를 가진다.
    - 안정적이며, 대부분의 경우에서 좋은 성능을 낸다.
- 단점
    - 추가 메모리 공간이 필요하다.
- 시간 복잡도
    - 평균: O(nlogn)
    - 최선: O(nlogn)
    - 최악: O(nlogn)

---

### 퀵 정렬(Quick Sort)

> 배열에서 하나의 피벗(pivot)을 정하여 이 피벗보다 작은 값은 왼쪽, 큰 값은 오른쪽에 위치시킨 후, 피벗 양쪽 배열에서 같은 과정을 반복하며 정렬하는 방식   
→ 평균적으로 `빠른 수행 속도`로 정렬하기 때문에 퀵 정렬이라고 불림

<details>
  <summary> 알고리즘(ADL) </summary>
  <div markdown="0">

![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Quick_ADL1.png)
    
![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Quick_ADL2.png)
    
  </div>
</details>

<details>
  <summary> 수행 과정(png) </summary>
  <div markdown="0">

![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Quick_Process1.png)
    
![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Quick_Process2.png)  
    
![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Quick_Process3.png)  

  </div>
</details>

<details>
  <summary> 수행 과정(gif) </summary>
  <div markdown="0">

 ![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Quick.gif)  

  </div>
</details>
    
- 장점
    - 평균적으로 속도가 매우 빠르다.
- 단점
    - 피벗을 어떻게 설정하는 지에 따라 성능의 차이가 심하다.
    - 안정성이 좋지 않다.
- 시간 복잡도
    - 평균: O(nlogn)
    - 최선: O(nlogn)
    - 최악: O(n^2)

---

### 힙 정렬(Heap Sort)

> 완전 이진 트리인 힙을 이용하여 가장 큰 수를 root 노드로 이동시키며 하나씩 꺼내 배열의 뒤부터 저장하며 정렬하는 방식   
→ 완전 이진 트리의 일종인 `힙(Heap)`을 사용하여 정렬하기 때문에 힙 정렬이라고 불림

<details>
  <summary> 알고리즘(ADL) </summary>
  <div markdown="0">

![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Heap_ADL.png)
    
  </div>
</details>

<details>
  <summary> 수행 과정(png) </summary>
  <div markdown="0">

![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Heap_Process1.png)
    
![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Heap_Process2.png)

  </div>
</details>

<details>
  <summary> 수행 과정(gif) </summary>
  <div markdown="0">

 ![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Heap.gif)  

  </div>
</details>

- 장점
    - 항상 같은 시간 복잡도를 가지기 때문에 성능이 준수하다.
- 단점
    - 같은 시간 복잡도를 가지는 정렬 알고리즘과 비교하면 느린 편이다.
- 시간 복잡도
    - 평균: O(nlogn)
    - 최선: O(nlogn)
    - 최악: O(nlogn)

---

### 쉘 정렬(Shell Sort)

> 일정 간격(gap)으로 배열을 생성하여 각 배열끼리 삽입 정렬한 후, 더 적은 개수의 배열을 생성하여 앞 과정을 반복하며 정렬하는 방식   
→ 삽입정렬을 보완하는 방식으로 `Donald L. Shell`이라는 사람이 제안하여 쉘 정렬이라고 불림

<details>
  <summary> 알고리즘(ADL) </summary>
  <div markdown="0">

![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Shell_ADL.png)
    
  </div>
</details>

<details>
  <summary> 수행 과정(png) </summary>
  <div markdown="0">

![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Shell_Process1.png)
    
![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Shell_Process2.png)

  </div>
</details>

<details>
  <summary> 수행 과정(gif) </summary>
  <div markdown="0">

 ![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Shell.gif)  

  </div>
</details>

- 장점
    - 삽입 정렬의 문제점을 해결함으로써 성능이 좋다.
- 단점
    - 설정한 간격(gap)에 따라 성능의 차이가 심하다.
- 시간 복잡도
    - 평균: O(n^1.3~1.5)
    - 최선: O(n)
    - 최악: O(n^2)

---

## 정렬 속도 한 번에 보기(gif)

 ![](https://github.com/vhzkclq0705/CS-Study/blob/main/contents/data-structure/images/Sort/Speed.gif)  

## 면접 대비
- ?? 정렬에 대해 설명해 보세요.
