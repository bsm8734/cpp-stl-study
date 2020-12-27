# Deque
  - 양쪽에서 삽입 삭제 가능
  - 크기가 가변적
  - 앞, 뒤에서 삽입/삭제 가능
  - 중간에 데이터 삽입/삭제가 용이하지 않음
  - 랜덤접근(인덱스로 접근) 가능 *(= 리스트처럼 탐색하지 않아도 된다)*
  - 많은 데이터 혹은 검색량이 많은 경우, *map, set, hash_map* 사용하는 것이 좋음

### 생성
  ```c
  #include <deque>

  deque<int> dq;             // dq는 빈 컨테이너
  deque<int> dq(n);          // dq는 default 값으로 초기화 된 n개의 원소를 가짐
  deque<int> dq(n, val);     // dq는 val로 초기화 된 n개의 원소를 가짐
  deque<int> dq(dq2);        // dq는 dq2의 복사본
  deque<int> dq(begin, end); // dq는 반복자 구간 [begin, end)로 초기화 된 원소를 가짐
  ```

### 함수
  ```c
  // ============================== 할당, 접근 =================================
  dq.assign(10, "Hello");   // 특정원소로 덱을 채움, param2가 주어지지 않으면 default형으로 채워짐
  dq.assign(4, 3);          // 3의 값으로 4개의 원소 할당 // 3,3,3,3

  dq.at(idx);   // idx번째 원소를 반환, 유효범위를 점검, dq[idx]보다 속도가 느림
  dq[idx];      // idx 번째 원소를 참조

  dq.front();   // 첫 번째 원소를 참조
  dq.back();    // 맨 마지막 원소를 참조

  // ============================== 삽입, 삭제 =================================
  dq.push_front(3); // dq의 첫 번째 원소 앞에 원소 3을 삽입
  dq.pop_front();   // dq의 첫 번째 원소를 제거

  dq.push_back(5);    // dq의 마지막 원소 뒤에 원소 5를 삽입
  dq.pop_back();      // 마지막 원소를 제거

  dq.insert(1, 2, 3);
  // 1번째 위치에 2개의 3값을 삽입
  // 삽입 시에 앞뒤 원소의 개수를 판단하여 적은 쪽으로 미루어서 삽입
  // 만약 앞의 원소의 개수가 적을 경우, 앞쪽으로 블록을 만들어서 원소를 옮기고 삽입
  // 만약 뒤의 원소의 개수가 적을 경우, 뒤쪽으로 블록을 만들어서 원소를 옮기고 삽입

  dq.insert(3, 4);
  // 3번째 위치에 4의 값을 삽입
  // 삽입한 곳의 iterator를 반환

  // ============================== 크기 =================================
  dq.size();    // 원소의 개수를 리턴

  dq.resize(n);
  // 크기를 n 으로 변경
  // 만약 크기가 더 커졌을 경우 비어있는 원소를 default값인 0으로 초기화
  dq.resize(n,2);
  // 크기를 n 으로 변경
  // 만약 크기가 더 커졌을 경우 빈 원소를 2로 초기화

  // capacity 함수는 없음

  // ============================== ETC =================================
  dq2.swap(dq1); // dq1과 dq2를 바꿈 (swap)

  dq.empty()    // dq가 비었으면 true를 반환
  dq.clear();   // 모든 원소를 제거

  dq.erase(iter);
  // iter가 가리키는 원소를 제거
  // 제거 한 후 앞 뒤의 원소의 개수를 판단하여 적은쪽의 원소를 당겨서 채움
  // 제거한 곳의 iterator 를 반환
  ```

### iterator

<details>
<summary>반복자 종류 (begin, end)</summary>
<div markdown="1">

```c
dq.begin();
// 첫번째 원소를 가리킴 (iterator와 사용)
// ex) deque<int>::iterator iter = dq.begin();

dq.end();
// 마지막의 "다음"을 가리킴 (iterator와 사용)
// ex) deque<int>::iterator iter = dq.end();

dq.rbegin();
// reverse begin을 가리킴
// 맨 마지막원소를 마치 첫 번째 원소처럼 가리킴 (역으로)
// iterator와 사용
// ex) deque<int>::iterator iter = dq.rbegin();

dq.rend();
//  reverse end 을 가리킴
// 맨 첫번째 원소의 "앞"을 마지막 원소의 "다음" 처럼 가리킴
// iterator와 사용
// ex) deque<int>::iterator iter = dq.rend();
```

</div>
</details>  

```c
// ============================== 정방향 출력 =================================
deque<int>::iterator iter;

for(iter = dq.begin(); iter != dq.end() ; iter++){
  cout << *iter << '\n';
}

// ============================== 역방향 출력 =================================
deque<int>::reverse_iterator r_iter;

for(r_iter = dq.rbegin(); r_iter != dq.rend() ; r_iter++) {
   cout << *r_iter << '\n';
}
```
