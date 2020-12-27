# Vector
`#include <vector>`: vector를 사용하기 위한 헤더

### 선언
  ```c
  vector<int> v;          // 비어있는 vector v를 생성

  vector<int> v(n);       // default 값(0)으로 초기화 된 n개의 원소를 가지는 vector v를 생성
  vector<int> v(n, val);  // val로 초기화된 n개의 원소를 가지는 vector v를 생성
  vector<int> v1(5, 2);   // 2, 2, 2, 2, 2

  vector<int> v2(v1);     // v2는 v1 vector를 복사해서 생성
  ```

### 원소 할당, 접근
  ```c
  // ============================== 할당 ============================ //
  v.assign(5, 2); // 2의 값으로 5개의 원소 할당
  // v.reserve(n);   // n개의 원소를 저장할 위치를 예약(미리 동적할당)

  // ========================== 삽입, 삭제 ========================== //
  v.push_back(7); // 마지막 원소 뒤에 원소 7을 삽입
  v.pop_back();   // 마지막 원소를 제거

  v.insert(2, 3, 4); // 2번째 위치에 3개의 4값을 삽입 (뒤 원소들은 뒤로 밀림)
  v.insert(2, 3); // v[2] = 3 와 같음
  // 2번째 위치에 3의 값을 삽입
  // 삽입한 곳의 iterator를 반환

  v.erase(iter);
  // iter 가 가리키는 원소를 제거
  // size만 줄어들고 capacity(할당된 메모리)는 그대로 남음

  // ============================== 크기 ============================ //
  v.size(); // 원소의 갯수를 리턴
  // v.capacity();  // 할당된 공간의 크기를 리턴
  // v.resize(n);   // 크기를 n으로 변경 (더 커졌을 경우 default값인 0으로 초기화)

  // ============================== 접근 ============================ //
  v.at(idx); // idx번째 원소를 리턴
  v[idx]; // idx 번째 원소를 리턴 // 범위를 점검X, 속도가 v.at(idx)보다 빠름

  v.front(); // 첫번째 원소를 리턴
  v.back(); // 마지막 원소를 리턴

  /* iterator */
  v.begin();  // 첫번째 원소를 가리 // (iterator와 사용)
  v.end();    // 마지막의 "다음"을 가리킴 (iterator와 사용)
  v.rbegin(); // reverse begin을 가리킴 (거꾸로 해서 첫번째 원소를 가리킴, iterator와 사용)
  v.rend();   // reverse end 을 가리킴 (거꾸로 해서 마지막의 다음을 가리킴, iterator와 사용)

  // =========================== 제거, 비었는지 ========================= //
  v.empty() //  vector가 비었으면 리턴 true
  // 비어있다의 기준은 size가 0이라는 것이지, capacity와는 상관이 없음

  v.clear();
  // 모든 원소를 제거합니다.
  // 원소만 제거하고 메모리는 남아있음
  // size만 줄어들고 capacity는 그대로 남아있음

  // =============================== ETC ============================= //
  // swap
  v2.swap(v1);    // v1과 v2의 원소와 capacity 바꿈 (모든걸 스왑해줌)

  // copy
  copy(v1.begin(), v1.end(), v2.begin()); // src: v1  // dst: v2

  if (v1 == v2) // v1과 v2의 원소가 모두 같은가?
  if (v1 != v2) // v1과 v2의 원소 중 하나라도 다른 것이 있는가?
  ```

### iterator 사용
  ```c
  vector<int>::iterator iter;
  for(iter = v.begin(); iter != v.end() ; iter++){
      cout << *iter << " ";
  }
  ```

### copy
  - for문이 copy보다 느림
  ```c
  // 1차원 벡터 복사
  copy(v1.begin(), v1.end(), v2.begin()); // src: v1  // dst: v2

  // 다차원 벡터 복사
  v2.resize(v1.size(), vector<int>(v1.size()));
  copy(v1.begin(), v1.end(), v2.begin());
  ```

  - <details>
    <summary>배열 복사</summary>
    <div markdown="1">

    ```c
    /* 1차원 배열 복사 */
    copy(arr1, arr1 + ARR_SIZE, arr2);
    // param1: 배열의 시작부분
    // param2: 배열의 끝부분
    // param3: 복사할 배열의 시작부분을 각각 포인터로 넘겨준다.

    /* 2차원 배열 복사 */
    copy(&arr1[0][0], &arr1[0][0] + ARR_SIZE * ARR_SIZE, &arr2[0][0]);
    ```

    </div>
    </details>  

### swap
  ```C
  v2.swap(v1);    // v1과 v2의 원소와 capacity 바꿈 (모든걸 스왑해줌)
  ```
