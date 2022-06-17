# 가상메모리

## 가상메모리란
> 물리적 메모리 크기의 한계를 극복하기 위해 나온 기술   
> 프로세스를 실행할 때 필요한 부분만 메모리에 로드하고 나머지는 디스크에 두는 것
> * ex) segmentation, paging




## Demanding Paging(요구 페이징)
> 필요한 페이지만 메모리에 올리는 것



<img src="./images/Virtual_Memory/demand_paging1.png" width="700"/>  

### demand paging의 page table은 다음과 같은 요소를 가지고 있다.
> frame number, vaild bit
> * vaild-invaild bit: 메모리에 페이지가 올리와 있는 여부 -> 1: page가 메모리에 있음, 0: 메모리에 없고 디스크에 존재함



### ***`만약 페이지가 메모리에 없다면?`***




<img src="./images/Virtual_Memory/demand_paging.png" width="700"/>  


### 주소변환 과정
> * 1. TLB에서 page가 있는지 확인한다.
> * 2. TLB hit인 경우 주소변환을 하고 TLB miss인 경우 page table을 확인한다.
> * 3. page table의 valid-invalid bit가 1이라면 TLB에 page table을 load한다. 0이라면 page fault 발생
> * 4. page fault가 발생하면 MMU가 운영체제에 Trap을 발생시키고 커널모드로 들어가 ISR에 의해 page fault handler가 작동된다.
> * 5. 유효하지 않은 참조인 경우 프로세스를 종료시키고 그렇지 않다면 빈 page frame에 load한다. 빈 page frame이 없다면 victim page 를 
> 선택하여 대체한다
>   * victim page: backing store(disk)로 page out 되는 page
> * 6. 운영체제는 참조된 page를 디스크에서 메모리로 로드(I/O)하고, disk I/O가 끝날 때까지 해당 프로세스는 운영체제에게 CPU를 빼앗긴다.
> * 7. disk I/O가 끝나면 page table이 업데이트 되고 vaild-invaild bit가 1로 바뀐다.
> 해당 프로세스는 ready queue에 들어간다.
> * 8. 프로세스에 cpu가 할당되면 다시 실행한다.


## Page Replacement Algorithm
* 메모리에 올라와있는 page를 관리하는 알고리즘   
> page in: backing store에서 메모리에 load 시키는 것   
> page out: 메모리에서 backing store로 out 시키는 것
> * page out되는 page를 victim page로 부름 


### ***`수정되지 않은 page를 고르는 것이 중요하다.`***
* 수정된 page는 backing store로 page out될 때 write 연산을 해야되기 때문이다.


### 1. OPT(Optimal Algorithm)
가장 먼 미래에 참조되는 page를 대체하는 방법으로 `항상 최적의 결과를 갖는다.`
> 다만 미래의 참조를 모두 알고 있어야 하므로 실제로 사용하기는 어렵고 다른 알고리즘의 성능에 의한 upper bound를 제공하는 역할을 한다.

<img src="./images/Virtual_Memory/OPT.png" width="700"/>  

### 2. FIFO(First In First Out)
먼저 들어온 page부터 page out 시키는 방법이다. 
> 미래를 모르는 경우에도 사용할 수 있고 모든 page가 frame에 평등하게 존재한다.

<img src="./images/Virtual_Memory/FIFO.png" width="700"/>  

`balady's anomaly 존재`
 * 일반적으로 frame이 증가하면 page fault가 감소하지만 특정 구간에서 늘어나는 현상이 발생

 <img src="./images/Virtual_Memory/belady's_anomaly.png" width="700"/>  


### 3. LRU(Least Recently Used)
참조한지 가장 오래된 page를 page out 시키는 방법
> optimal에 근접한 방법이며 belady's anomaly가 존재하지 않는다.   
> 구현하기 어렵고 접근빈도를 고려하지 않는다.   
> 연결 리스트로 구현하면 O(1)만에 page를 찾고 삽입할 수 있다. 제일 최근에 찹조된 page를 가장 앞으로 옮기는 방식으로 연결 리스트를 구현하면 replace가 일어날 때 가장 뒤에 있는 page를 바꿔주면 된다.


<img src="./images/Virtual_Memory/LRU.png" width="700"/>  


### 4. LFU(Least Frequently Used)
참조 횟수가 가장 적은 page를 page out 시키는 방법
> page를 참조하는 빈도는 고려하지만 최근에 사용된 page는 반영하지 못한다.   
> 연결 리스트를 이용해서 구현하면 replace 될 page를 찾는데 O(n)의 시간이 걸리고 heap을 이용하면 O(logn)의 시간이 걸린다.
> * heap: 완전 이진 트리의 일종으로 우선순위 큐 형태의 자료구조이다.


### 5. Second Chance(Clock)








<img src="./images/Virtual_Memory/Clock.png" width="700"/>  