# Map
  - 연관컨테이너
  - 노드 기반 컨테이너
  - 균형 이진트리로 구현
  - **key와 value**가 쌍으로 저장 (pair 객체 형태로 저장됨)
  - Unique Key: key는 고유한 값이므로 중복이 불가능
  - 삽입되면서 key를 기준으로 자동으로 정렬됨 (default: less/오름차순)
  - 필요한 만큼 동적할당

### Multimap
  - key 중복을 허용함
  - key 값이 같더라도, 나중에 삽입되는 값이 뒤쪽에 삽입 (In-order 상 뒤쪽)

  ```c
  #include <map>
  multimap<string, int> mm1;    // 선언
  multimap<int, int> mm2(mm1);  // mm1을 복사한 multimap mm2를 생성
  ```

### 선언
  - map 에 삽입을 하기 위한 insert는 pair 객체를 인자로 받아야함
  - key 값과 value는 쌍을 이루기 때문
  - `m[key] = val;` 을 통해서 원소(key, value)를 추가/수정이 가능

  ```c
  #include <map>

  map<int, int> m1;     // 오름차순
  map<string, int> m2;

  map<int> m(pred); // pred를 통해 정렬기준(오름,내림)을 세웁니다.
  map<int> m2(m1);

  m1.insert(pair<int, int>(10, 20));
  m2.insert(pair<string, int>("Hello", 22));
  ```

### 멤버함수들
  ```c
  // =========================== 삽입, 삭제 ==================================
  m.insert(k);     //k는 pair 객체
  m.insert(iter, k);

  m.erase(start, end);


  // =========================== 찾기, 교환 ==================================
  m.find(k);
  m2.swap(m1);

  // find 예제
  std::map<int, int>::iterator it;
  it = myMap.find(3);
  // 만약 존재한다면 iterator는 3을 return
  // 존재하지 않는다면 it는 m.end() 리턴
  // 만약 원하는 key값을 가지는 원소가 존재하는지 안하는지를 알고 싶다면
  if( myMap.find(key) == myMap.end()) cout << "found!";


  // ============================== bound ====================================
  // set의 bound 관련 함수와 동일하게 작동 (key를 기준으로 삼는 것도 동일)  
  m.upper_bound(k);
  // key 값에 해당되는 맨 마지막 원소의 "다음" 을 가리키는 반복자를 반환
  // 폐구간 " ) " 으로 사용
  m.lower_bound(k);
  // key 값에 해당하는 맨 첫번째 원소를 가리키는 반복자를 반환
  // 개구간 " [ " 으로 사용됨

  m.equal_range(k);
  // key 값에 해당하는 원소의 "범위" 를 pair 객체로 반환
  // pair 객체의 first 는 key 값에 해당하는 원소의 첫번째 반복자를 반환. (lower_bound)
  // pair 객체의 second 는 key 값에 해당하는 원소의 마지막 원소의 "다음" 반복자를 반환 (upper_bound)
  // [ first, second )


  // =============================== comp ==================================
  // 정렬 기준 조건자를 반환
  // set의 comp 관련 함수와 동일하게 작동
  m.value_comp();
  m.key_comp();

  // comp 예제
  map<int, string>::key_compare KComp = m.key_comp();
  if (KComp(3, 5))  cout << "same" << endl;
  else  cout << "Not same" << endl;


  // =============================== 크기 ==================================
  m.size();
  m.clear();
  m.count(k);
  m.empty();
  m.max_size();


  // ============================== 반복자 ==================================
  m.begin();
  m.end();

  m.rbegin();
  m.rend();

  // 출력 예제
  void print(map<int, string> Target_Map) { // 함수
    for (auto i : Target_Map)
        cout << i.first << " " << i.second; // key, value
  }
  print(Map); // 호출
  ```

### 예제
  ```c
  // ============================== 선언 ==================================
  map<int, string> m;

  // ============================== 삽입 ==================================
  // 방법 1
  m.insert(pair<int, string>(30, "world "));
  m.insert(pair<int, string>(12, "hello "));
  // 방법2
  m[12] = "hello ";
  m[30] = "world ";

  // ============================== 반복자 =================================
  map<int, string>::iterator iter;

  //접근방법 1 // "12 hello 30 world "
  for(iter = m.begin(); iter != m.end(); iter++){
     cout << iter->first << " " << iter->second;
  }

  //접근방법 2 // "12 hello 30 world "
  for(iter = m.begin(); iter != m.end(); iter++){
     cout << (*iter).first << " " << (*iter).second;
  }
  ```

##### 클래스, 구조체에서 **operator <**를 재정의하는 방법
  - Set.md 참고
