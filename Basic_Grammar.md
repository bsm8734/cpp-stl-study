# 기본
### 입출력  
  `#include <iostream>`: `cin, cout` 표준 입출력 함수를 사용하기 위한 헤더  
  `using namespace std;`: `std::` 생략하기 위해서 사용
  `#define _CRT_SECURE_NO_WARNINGS`: scanf 보안 경고로 인한 컴파일 에러 방지

### 포인터
  - & : 실제로 잡혀있는 메모리 위치를 가리킴
    + 참조자, reference, 레퍼런스
    + 변수에 별명을 붙이고, 별명을 통해서 변수의 메모리 공간에 접근 가능
    + 변수에 대해서만 선언이 가능하고, 선언과 동시에 누군가를 참조해야만 함
    + 참조의 대상을 바꾸는 것이 불가능하며, NULL로 초기화하는 것이 불가능
  - \* : 포인터

  ```c
    int *ptr; // 선언
    int *ptr1 = nullptr; // 초기화
    int* ptr = NULL;

    int num = 10;
    int *ptr = &num;
    cout << *ptr << '\n'; // 10
    cout << ptr << '\n';  // 값의 주소
    cout << &ptr << '\n'; // 포인터의 주소

    // int* ptr = 10; // 오류, 값을 포인터에 담을 수 없음
    int num = 10;
    int* ptr = &num;
    cout << *ptr << '\n'; // 10
    cout << ptr << '\n';  // 값의 주소
    cout << &ptr << '\n'; // 포인터의 주소

    char s1[] = "HelloMWorld";
    // char* ptr = strchr(s1, 'W');
    if (ptr != NULL) {
      cout << *ptr << endl;	  // W
      cout << ptr << endl;	   // World
      cout << &ptr << endl;	  // 주소
      // printf("%c, %s\n", *ptr, ptr); // W, World
    }
    cout << strchr(s1, 'M');
    // 주의: ptr은 쓰레기 값으로 초기화되며, 그 위치에 값을 넣는 것은 위험함
    int *ptr;
    *ptr = 100;
  ```

  - [포인터 변수의 크기]는 [포인터 변수가 가리키는 변수의 데이터형]과는 관계없이 __4Byte__로 동일  
  - 단순히 "주소가 가리키는 값이 int형 변수다" 라는 것을 알려주기 위함  
  - 포인터 역참조  
    자료형 없이 *ptr 호출하면 주소를 역으로 참조하여 그 주소가 가지고 있는 실제 값을 가져옴

  - swap 구현 예제
  ```c
    // 포인터로 구현
    void swap(int *n1, int *n2) {
      int tmp;
      tmp = *n1;
      *n1 = *n2;
      *n2 = tmp;
    }

    // reference로 구현
    void swap(int &n1, int &n2) { // 주소공간에 별명을 통해 직접 접근
      int tmp;
      tmp = n1;
      n1 = n2;
      n2 = tmp;
    }

    // main()
    int arr[2] = {10, 20};
    swap(arr[0], arr[1]);
    // arr[2] = {20, 10}
  ```

### 자료형
  - 형변환
    ```c
      // =========================== string & numbers ========================= //
      // int to string
      string str = to_string(num);

      // string to int
      int num = stoi(str);
    ```
    ```c
      // =========================== string Tips! ========================= //
      // string with others
      stoi(str) // string to int
      stol(str) // string to long int

      // 다른 파라미터 없이 사용하면 소수아래자리에 0을 채워, (점 포함) 8 글자 출력
      stof(str) // stirng to float
      stod(str) // string to double

      string str_d = "2.11";
      cout << stod(str_d) << '\n'; // 2.110000

      // 받고자하는 형식이 아닌 문자 나오면 바로 자름
      string str = "33 3Hello00World";
      int num = stoi(str);
      cout << num << '\n'; // 33

      /* 원하는 형식으로 진수 설정 가능 */
      //string binary(2) -> int
      cout << stoi("1110", nullptr, 2) << endl; // 14

      //string oct(8) -> int
      cout << stoi("014", nullptr, 8) << endl; // 12

      //string hex(16) -> int
      cout << stoi("0x14", nullptr, 16) << endl; // 20
    ```
    ```c
      // ================================ char* =============================== //
      // char* to int
      int num = atoi(cStr);

      // char* to string
      string str = cStr;

      // string to char*
      char* cStr = str.c_str();
    ```

  - typedef
    ```c
      #include <string.h>    // strcpy 함수가 선언된 헤더 파일

      typedef 자료형 별칭;
      typedef long long int ll;

      typedef struct _Student {   // 구조체 이름: _Student
        int age;
        string name;
      } Student;                  // 구조체 별칭: Student

      Student s1;                  // 구조체 별칭 Student으로 변수 선언
      strcpy(s1.name, "홍길동");   // . 으로 구조체 멤버에 접근하여 값 할당
      s1.age = 30;
    ```

  - 표현가능 범위
    + 1byte = 8bit (*2의 8제곱 표현가능*) `char`
    + 4byte = 4x8bit = 32bit (*2의 32제곱 표현가능*) `int, long`
    + 8byte = 8x8bit = 64bit (*2의 64제곱 표현가능*) `long long`, `long long int`

    > K = 2^10 = 10^3  
    M = 2^20 = 10^6  
    G = 2^30 = 10^9  

### pair
  ```c
  // 선언
  pair<int, int> p1;
  pair<int, string> p2 = make_pair(1, "bsm");

  // 접근
  cout << p2.first << ' ' << p2.second << '\n';   // 1 bsm

  // 활용
  vector<pair<int, string> > v;

  v.push_back({1, "hello"});    
  v.push_back(pair<int, string>(3, "world"));

  vector<pair<int, string> >::iterator iter;
  for(iter = v.begin(); iter != v.end(); iter++){
      cout << "[" << iter->first << "," << iter->second << "]" << endl;
  }

  ```

### cmath 헤더
  ```c
    #include <cmath>

    // 원하는 개수만큼의 소수점 출력
    cout<< fixed;
    cout.precision(1); // 소수점 1자리까지 표현 (반올림)

    cout.setf(ios::fixed);    // 설정 (= cout << fixed;)
    cout.unsetf(ios::fixed);  // 해제

    // 반올림: round 함수
    round(3.2); // 3
    round(3.7); // 4
    round(-3.2); // -3
    round(-3.7); // -4

    // 올림,내림: ceil, floor 함수
    ceil(4.2);  // 5
    floor(4.2); // 4

    // 버림: trunk 함수
    trunk(3.2); // 3
    trunk(3.7); // 3
    trunk(-3.2); // -3

    trunk(-3.7); // -3
    floor(-3.7); // -4
  ```

### algorithm 헤더
  - min, max
    ```c
      min(a, b) // 더 작은 값 반환
      max(a, b) // 더 큰 값 반환

      minmax(10, 20);  // 어떤 것이 min인지 max인지 구분하여 pair형태로 반환
      minmax({10, 20, 30, 40, 50}); // {최소, 최대} return {10, 50}
    ```

    <details>
    <summary>min, max 재정의하여 클래스 비교 하기</summary>
    <div markdown="2">

    ```c
      // min, max를 사용하여 클래스를 비교 가능
      class Animal {
        private:
            int age;
            int legs;
        public:
            Animal(int _age, int _legs) : age(_age), legs(_legs) {};    //생성자

            //나이가 적은지 확인하고,
            //나이가 같다면 다리개수가 적은지 판단.
            bool operator<(const Animal& _animal) const
            {
                if (age != _animal.age)
                    return age < _animal.age;
                return legs < _animal.legs;
            }

            // cout 출력을 위한 "<<" 재정의.
            friend ostream& operator<<(ostream& _os, const Animal& _animal);
      };
      // cout 출력을 위한 "<<" 재정의.
      ostream& operator<<(ostream& _os, const Animal& _animal) {
          _os << _animal.age << '/' << _animal.legs;
          return _os;
      }

      Animal cat1(10, 4);
      Animal cat2(20, 4);
      cout << min(cat1, cat2) << '\n'; // 10/4
      cout << max(cat1, cat2) << '\n'; // 20/4
    ```
    </div>
    </details>

    <details>
    <summary>반복문을 사용하여 쉽게 min, max값 구하기</summary>
    <div markdown="2">

    ```c
      //min, max를 비교하기 위해 맨 앞 요소 저장.
      int smallest = v[0];
      int largest = v[0];

      for (int i = 1; i < len; ++i)
      {
          smallest = min(smallest, v[i]);   //작은 값을 다시 smallest에 대입
          largest = max(largest, v[i]);     //큰 값을 다시 largest에 대입
      }
    ```
    </div>
    </details>  

### 반복문
  ```c
  // 범위기반 반복문: 배열, vector
  int arr[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
  for (int elem : arr)
    cout << elem << " ";

  for (auto elem : arr) {
    elem += 100; // 기존 데이터가 변경되지않음 // 이 줄은 실행되지않는 것과 같음
    cout << elem << " ";
  }
  for(int& elem : arr) {
    elem += 1;    // 기존 arr 데이터가 변경됨 // reference로 접근  
    cout << elem << endl;
  }

  // iterator -> string, vector, list 가능 (반복자 존재) // queue, stack (X)
  for(vector<int>::iterator iter = v.begin(); iter != v.end(); ++iter){
    *iter += 10; // 값 변경 // 포인터이므로 주소에 접근하여 값을 가져오거나 쓸 수 있음
    cout << *iter << '\n';
  }

  // auto 사용법
  // vector<string>::iterator = v.begin(); 와 같음
  auto it = v.begin();
  for (; it != v.end(); ++it)
  {
      cout << *it << '\n';
  }
  ```
