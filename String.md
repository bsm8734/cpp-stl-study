# 문자열
`#include <string>`: 기본 제공하는 자료형이 아닌 string 객체를 사용하기 위한 헤더

### 선언
  ```c
  string str1 = "Hello";
  string str2("Hello");

  string str3;
  str3.assign("12345678");

  // 동적할당
  string *pstr = new string("Hello");
  delete pstr;
  ```

### append
  ```c
  string str1 = "hello";
  string str2 = " worldworldworld";

  // 전부 붙이기
  str1.append(str2); // "hello worldworldworld"

  // str2(param1)의 시작위치(param2)부터 원하는갯수(param3)만큼 붙이기
  str1.append(str2, 0, 6); // "hello world"

  // 원하는갯수(param1)만큼 원하는 문자를 붙이기(param2)
  str1.append(5, '.'); // "hello....."
  ```

### size & length
  ```c
  str.size();
  str.length();
  ```

### compare
  ```c
  // =========================== string 타입 문자열 ========================= //
  string str1 = "aaa";
  string str2 = "aab";

  // <, >, == : 앞에서부터 아스키코드 기준 비교
  if(str1 == str2) // True, False
    cout << "True" << '\n';

  int ret = str1.compare(str2); // 같으면 0, 다르면 -1/1 : return (str1-str2)


  // =========================== C 타입 문자열 ========================= //
  // 맨 뒤에 '\n' 존재하는 문자열에서만 사용 가능
  // c_str의 경우, == 연산자 사용시, 주소값을 비교하게됨
  char s1[10] = "aaa";
  char s2[10] = "aab";

  int ret1 = strcmp(s1, s2); // 같으면 0, 다르면 -1/1 : return (s1-s2)
  int ret2 = strncmp(s3, s1, 2); // 원하는갯수(param3) 만큼 같은지 확인 : return (s1-s2)
  ```

### find
  ```c
  string str1 = "hello world ! I love you lovelove";
  string str2 = "love";

  str1.find(str2); // 16
  str1.find("nothing"); // string::npos

  // 원하는 문자열(param1)을 지정한 위치(param2) 이후부터 찾기
  int pos = str1.find(str2);  // 16
  str.find(str2, pos + 1);    // 25

  // 거꾸로 탐색
  str1.rfind("love"); // 29

  // ============================== Example ============================ //
  // 같은 문자열이 여러번 나타날때 유용
  size_t pos;
  string str = "hello world ! I love you lovelove";
  pos = tr.find("love");

  while(pos != string::pos){
    // cout << pos << " "; // "love"의 위치출력
    pos = str.find("love", pos + 1);
  }

  // =========================== C 타입 문자열 ========================= //
  char s1[] = "HelloMWorld";
  char* ptr = strchr(s1, 'W');
  if (ptr != NULL) {
    cout << *ptr << endl;	// W
    cout << ptr << endl;	// World
    cout << &ptr << endl;	// 주소
  }

  char s1[] = "HelloMWorld";
  cout << strchr(s1, 'W') << '\n'; // World
  ```
  > 리턴값 strchr() 함수는 string의 문자로 변환되는 c의 첫 번째 표시에 대한 포인터를 리턴. 함수는 지정된 문자를 찾지 못하면 NULL을 리턴.
  > 따라서 strchr은 value가 아닌 주소값 포인터이므로 * 포인터로 지정가능

### substr
  ```c
  // 원하는 위치만큼 sub-string 부분문자열을 만들 수 있음
  string str1 = "good morning Mr Brown";
  string str2;
  str2 = str1.substr(5, 7); // "morning"
  str2 = str1.substr(5);    // "morning Mr Brown"
  str2 = str1.substr(str1.find("Mr")); // "Mr Brown"
  ```
  - `str1.substr(5)` : index가 5번째인 값부터 끝까지 문자열을 반환
  - `str1.substr(5,1)` : index가 5번째인 값부터 1 길이의 문자열을 반환

### replace
  ```c
  strgin str = "hello my world";

  // param1 이상, param2 미만의 sub-string을 param3으로 대체
  str.replace(str.find("my"), 2, "your"); // hello your world // [6, (6+2))
  str.replace(str.begin()+6, str.begin()+8, "hello"); // hello hello world // [6, 8)

  str.replace(6, 3, "HELLO WORLD", 0, 3); // 6, 0: 각각의 시작위치 // 3: 길이
  str.replace(6, 3, "HELLO WORLD", 2);    // "HELLO WORLD"의 처음 2글자로 대체

  ```
  - `str1.replace(5, 2, str2)` : str1의 5번째인 자리부터 2개의 문자열을 str2문자열 전체로 대체

### swap, reverse
  ```c
  swap(str1, str2)                  // str1와 str2의 참조를 서로 바꾸어줌 // str1<=>str2
  reverse(str.begin(), str.end());  // 문자열 역순 반환
  // #include <algorithm> 필요
  // 양방향 반복자를 사용하므로 vector, string, list등의 양방향 반복자를 사용할 수 있는 컨테이너에서는 어디서든 reverse 함수 사용 가능
  ```

### erase
  ```c
  str.assign("12345678");

  // 시작위치(param1)부터 지정한갯수(param2)만큼 삭제
  str.erase(0, 4);  // 5678
  str.erase(4, 4);  // 1234
  str.erase(4, 1);  // 1234678 // ind=4 위치, value=5 삭제

  // 시작위치(param1)~끝까지 삭제
  str.erase(4);     // 1234
  str.erase();      // 전체삭제
  ```

### empty & clear
  ```c
  // 문자열에 내용이 있으면 문자열 초기화
  if (str.empty() == 0)
    str.clear();
  ```

> 접근: at(), operator[], front(), back(), push_back(), pop_back(), begin(), end()  
크기: size(), length(), capacity(), resize(), shrink_to_fit(), reserve(), clear(), empty()  
형변환, 비교, 찾기: c_str(), compare(), copy(), find()  
수정: swap(), operator+,  replace(), substr()  
