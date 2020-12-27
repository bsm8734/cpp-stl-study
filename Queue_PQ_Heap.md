# Queue, PQ, Heap

### Queue
  - FIFO: First-In, First-out (선입선출)
    + rear(end)에 데이터를 삽입하고 front에서 데이터를 빼는 자료구조
  - 어댑터 컨테이너
    + deque, list 컨테이너에 붙어서(기반하여) 사용 가능 (vector container 불가능)
    + vector container가 불가능한 이유: queue 자료구조 특성상 뒤에서 삽입하고 앞에서 빼야하는데(FIFO) vector는 앞에서 빼는 동작을 지원해 주지 않기 때문
    + 내부적으로 deque, list container 로 구현이 되어있지만 queue 구조로 동작하도록 멤버 함수를 제공해주는 것
    + default: deque container 기반
  - 큐의 종류
    1. 선형 큐
    2. 환형 큐
    3. 우선순위 큐([Priority Queue](Priority-Queue))
  - 함수
  ```c
  #include <queue>

  queue<int> q;
  // 내부 컨테이너 구조를 바꾸는 생성자 형식
  // queue<int, list<int>> q;  // 헷갈리니까 그냥 위에꺼 쓰기!
  // queue<string, list<string>> q;

  q.push(1);
  q.pop();

  q.push(1); q.push(2); q.push(3);

  q.front();  // 1
  q.back();   // 3

  q.size();   // 3

  while(!q.empty()){ // q 안의 모든 원소를 제거
    q.pop();
  }
  // q.clear() 존재하지 않음
  // 큐가 비었는데 pop하려하면 에러 발생
  ```

### Priority Queue
- 최대, 최소 값을 빠르게 찾기 위해서 사용
- 활용: 프림 알고리즘, 다익스트라 알고리즘, 허프만 코드
- **Heap**으로 구현 가능
> Heap
  + 완전이진트리의 일종
  + Heap Tree는 중복을 허용 (이진탐색트리에서는 중복 비허용)
  + 우선순위 큐를 구현하는 방법 중에 가장 효율적
  + 삽입, 삭제 모두 O(logn)
  + 배열을 사용하여 구현 (index 0번은 쉬운 계산을 위해 사용하지 않음)
  + 특정 위치의 노드번호는 새로운 노드가 추가되어도 변하지 않음

- 부모, 자식 관계
  + 부모의 인덱스 = n
  + 왼쪽자식의 인덱스 = 2n
  + 오른쪽자식의 인덱스 = 2n+1

  > *부모의 인덱스(n) = 자식의 인덱스(2n, 2n+1) / 2*

- **삽입** 시, 맨 마지막 노드에 삽입하고 상위 노드와 값을 비교하여 위치를 변경해감
- **삭제** 시, 최상위 루트 노드를 삭제하고, 그 자리에 최하단 마지막 노드를 가져옴  
   이후 하위 노드와 값을 비교하여 위치를 변경해감
- 삽입, 삭제가 이루어질 때마다 위치 업데이트 실시  
  최대로 노드 위치 업데이트 해봤자 *트리의 높이 이하* 만큼의 업데이트 진행

- **종류**
  - max heap: 내림차순 *(default)*  
    root 노드에는 (우선순위가) 가장 큰 값이 들어있음   // -,4,3,2,1
  - min heap: 오름차순  
    root 노드에는 (우선순위가) 가장 작은 값이 들어있음 // -,1,2,3,4

```c
// ============================== 선언 =================================
#include <queue>

priority_queue<int> pq;     // default: max heap (내림차순)
priority_queue<int, vector<int>, greater<int>> pq; // min heap (오름차순)

//사용자 지정 비교함수 사용
priority_queue<int, vector<int>, compare> pq;
```
```c
// ============ comp structure와 operator overloading ==================
struct compare {
    bool operator()(const int& a, const int& b) {
        // method 1
        return a > b;  // 오름차순

        // method 2
        if(a > b) return true; // 오름차순
        else return false;
    }
};

struct compare {
    bool operator()(int a, int b) {
        return l > r;  // 오름차순
    }
};
```
> **compare 함수의 return 값이 의미하는 것**  
 `return true;`  : b의 우선순위를 더 높게 만들기  
 `return false;` : a의 우선순위를 더 높게 만들기  

```c
// =================== 함수 ======================
pq.size();
pq.push();
pq.pop();
pq.top();
pq.empty()
```
