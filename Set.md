# Set
  - 연관컨테이너
  - 노드 기반 컨테이너
  - 균형 이진트리로 구현
  - **key**라 불리는 원소들의 집합으로 이루어진 컨테이너 (원소 = key)
  - key값은 중복이 허용되지 않음
  - 삽입시 자동 정렬
  - default: 오름차순 정렬(less)
  - 중위 순회를 통하여 순서대로 출력 (iterator가 자동으로 inorder traversal 순서로 순회)
  - 사용
    1. 삽입과 동시에 정렬이 필요한 경우
    2. 중복을 제거한 원소의 집합이 필요한 경우
    3. 현재 원소가 중복된 값인지 확인이 필요한 경우

### Multiset
  - 연관 컨테이너
  - key값이 중복 가능 (일반 set과의 차이점)
  - 연산자, 생성자, 멤버 변수는 동일

### 선언
  ```c
  // set
  #include <set>

  set<int> s;               // 오름차순
  set<int, greater<>> s;    // 내림차순
  set<pair<int, string>> s;
  set<int> s(pred); // pred를 통하여 정렬기준을 세울 수 있음
  set<int> s2(s1);  // s1을 복사하여 s2 생성
  ```
  ```c
  // multiset
  #include <set>

  multiset<int> ms;
  multiset<vector<int>> ms;

  ```

### 함수
  ```c
  // ============================== 삽입 ==================================
  s.insert(k);
  // 원소 k를 삽입
  // 삽입시에 자동으로 정렬된 위치에 삽입
  // 삽입이 성공 실패에 대한 여부는 리턴값 (pair<iterator, bool>) 으로 나옴
  //  pair<iterator, bool>에서 pair.first는 삽입한 원소를 가리키는 반복자 이고, pair.second는 성공(true), 실패(false)를 나타냄
  set<string>::iterator iter;
  std::pair<iter, bool> ret = s.insert("a");

  s.insert(iter, k);
  // iter가 가리키는 위치 부터 k를 삽입할 위치를 탐색하여 삽입

  // ============================== 삭제 ==================================
  s.erase(iter);
  // iter가 가리키는 원소를 제거
  // 제거 한다음 제거 한 원소 다음 원소를 가리키는 반복자를 리턴

  // 둘다 같음
  s.erase(s.find("a"));
  s.erase("a");

  s.erase(start, end);
  // [start, end) 범위의 원소를 모두 제거

  s.erase(s.find(30), s.find(70)); // [30,70) 사이의 key를 가지는 원소 모두 제거
  // ============================== ETC ==================================
  s.find(k);
  // 원소 k를 가리키는 반복자를 반환
  // 원소 k가 없다면 s.end() 와 같은 반복자를 반환

  s.count(k);
  // 원소 k 의 갯수를 반환
  // 0 or 1의 값을 반환 (set은 중복 key를 비허용)
  // (단, multiset은 키값이 중복이 가능하므로 0/1이 아닌 다른 수 가능)

  s2.swap(s1);
  // s1과 s2를 바꿈

  s.clear();  // 모든 원소를 제거
  s.empty();  // set s가 비어있는지 확인


  s.value_comp();
  s.key_comp();
  // 정렬 기준 조건자를 반환합니다.
  // set 컨테이너에서는 두개의 함수 반환형이 같음

  s.size(); // 사이즈(원소의 갯수)를 반환
  s.max_size(); // 최대 사이즈(남은 메모리 크기)를 반환
  ```

##### key_comp 예제
  - `set.key_comp(x);`: x배열과 정렬상태(오름차순 등)가 같으면:true, 다르면:false
  - `set.value_comp(x);`: key_comp(x)랑 똑같음

  ```c
  set<int> Set = { 1,3,5,7,9,11 };

  set<int>::key_compare Key_Comp = Set.key_comp();

  // 서로 방향이 같은 경우
  if (Key_Comp(2, 3))
      cout << "same(2,3)" << endl; // same
  else
      cout << "Not same(2,3)" << endl;

  // 서로 방향이 다른 경우
  if (Key_Comp(3, 2))
      cout << "same(3,2)" << endl;
  else
      cout << "Not same(3,2)" << endl; // not same
  ```

### 반복자
  ```c
  // ============================== 반복문 ==================================
  // 반복자 선언
  set<int>::iterator iter, start, end;

  // 반복자를 리턴(참조)
  iter = s.begin();   //  맨 첫번째 원소를 가리키는 반복자를 리턴(참조)
  iter = s.end();     // 맨 마지막 원소(의 다음)를 가리키는 원소의 끝부분을 알 때 사용

  //존재 하는 원소 찾기
  iter = s.find(30);
  if(iter != s.end()){
      cout << *iter << " : 존재 " << '\n'; // 30 : 존재
  } else {
      cout << "존재하지 않음 " << '\n';
  }

  iter = s.begin();
  cout << *iter <<'\n'; // s의 첫 원소
  iter = s.end();
  cout << *iter <<'\n'; // NULL

  s.rbegin();
  s.rend();
  // begin(), end() 와 반대로 작동하는 멤버함수들
  // 역으로 출력하고 싶을때 사용
  for(iter = s.rbegin(); iter != s.rend(); iter++){
      cout << * iter << '\n';
  }

  // =========================== 구간 반복자 ==================================
  s.upper_bound(k); // 원소 k가 끝나는 구간의 반복자
  s.lower_bound(k); // 원소 k가 시작하는 구간의 반복자

  set<int>::iterator l, u;
  for(int i = 0; i < 10; i++) s.insert(i*10); // s={0,10,20,30,40,50,60,70,80,90}

  l = s.lower_bound(12); // [20,
  u = s.upper_bound(78); //     80) --> erase

  s.erase(l, u);  // s={0,10,   80,90}

  s.equal_range(k); // k=15 라면 15의 {lower_bound(k), upper_bound(k)}를 반환
  // 원소 k가 시작하는 구간과 끝나는 구간의 반복자 pair 객체를 반환
  // upper_bound(k), lower_bound(k) 가 합쳐진 멤버함수

  // equal_range 활용
  multiset<int>::iterator iter;
  for(iter = ms.begin(); iter != ms.end(); iter++){
      cout << *iter << " " ;
  }
  cout << endl;

  //pair<iter, iter> 를 통해 key 11 의 equal_range 를 받습니다.
  pair<multiset<int>::iterator, multiset<int>::iterator> equal_pair = ms.equal_range(11);


  for(iter = equal_pair.first ; iter != equal_pair.second; iter++){
      cout << *iter << " " ;
  }
  cout << endl;
  ```

### 클래스, 구조체 활용법
  - 클래스, 구조체를 map, set의 key값으로 만드는 방법
    map, set을 생각해보면 균형 이진트리로 구현되어 있는 연관 컨테이너이다.  
    트리는 key를 통해 정렬하고 원소를 찾을 수 있어야 하므로 key값은 대소비교가 가능해야한다. 클래스를 <, > 기호를 통해 대소비교 할 수 있게 하기 위해서는 operator <를 재정의 해주면 된다.

##### 클래스, 구조체에서 **operator <**를 재정의하는 방법
  - 클래스, 구조체 내부에 아래와 같이 정의 및 선언
  - 리턴타입: bool
  - 매개변수로는 현재 클래스와 동일한 클래스 타입으로 const & 형태로 받음
  - 재정의 하지않으면 컴파일 에러
  ```c
  bool operator<(const 클래스명& 변수명) const
  {
    //비교구문을 통해 true, false를 반환
  }
  ```
  - 예제
  ```c
  #include<iostream>
  #include<map>        // map
  #include<utility>    // make_pair
  using namespace std;

  class Human
  {
  private:
      int age;
      int height;
  public:
      // 나이가 적은지 확인하고,
      // 나이가 같다면 키가 작은지 확인
      Human(int _age, int _height) : age(_age), height(_height){}
      bool operator<(const Human& rhs) const
      {
          if (age != rhs.age)
              return age < rhs.age;
          // else
          return height < rhs.height;
      }
  };

  int main(void)
  {
      std::map<Human, int> m; // map 선언

      // map의 key 값이될 클래스 배열
      Human hArr[] = { Human(30, 180), Human(30, 170), Human(30, 160),
                       Human(22, 110), Human(22, 100), Human(42, 168),
                       Human(51, 170) };

      int num = 0;                            // map의 value가 될 아무거나 값
      for (Human human : hArr)
      {
          m.insert(make_pair(human, num));    // 클래스가 map의 키 값으로 잘 들어감
          num++;
      }

      if (m.find(Human(30, 160)) != m.end()) {    // map의 키 값 검색

          cout << "map에 Human(30, 160)이 있음" << endl; // 출력
      }
      else
      {
          cout << "map에 Human(30, 160)은 없음" << endl;
      }
      return 0;
  }
  ```
