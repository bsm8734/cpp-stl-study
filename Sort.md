# 정렬
방법: 2개(sort 함수 사용, 인덱스로 접근하여 배열 활용)

### sort 함수
  - 퀵소트 사용: O(nlogn)
  - 언제 사용?
    - 입력 형식이 복잡한 형식일 때 유용
    - 값의 수가 적을 때 유용
    - 정렬 조건을 까다롭게 정의해야하는 경우 유용 (compare 함수 정의해서 해결가능)

  ```c
    #include <algorithm>          // sort 함수 사용을 위해 필요

    sort(arr, arr+10);            // [arr, arr+10) default(오름차순) 정렬
    sort(v.begin(), v.end());                    // default: 오름차순
    sort(v.begin(), v.end(), greater<int>());    //내림차순
    sort(v.begin(), v.end(), less<int>());       //오름차순

    sort(v.begin(), v.end(), compare);           //사용자 정의 함수 사용
  ```
  ```c
    // compare 함수 정의
    bool compare(int a, int b){
      if (a < b) return true; // 오름차순 정렬
      else return false;
    }
  ```
  > **compare 함수에서 return 값이 의미하는 것**  
  파라미터 순서가 *(int a, int b)*인 경우,   
  `return a<b;`   *오름차순*  
  `return true;`  *a와 b의 위치를 그대로 두기*  
  `return false;` *a와 b의 위치를 바꾸어야 원하는 sort 완성가능*  

  <details>
  <summary>연산자 오버로딩(operator overloading, '<') 활용한 sort</summary>
  <div markdown="1">

    ```c
      class Student{
        public:
          string name;
          int age;
          Student(string name, int age):name(name),age(age){}

          // 연산자 오버로딩
          bool operator<(Student s) const{  
              if(this->name == s.name){
                  return this->age < s.age;
              }else{
                  return this->name < s.name;
              }
          }
      };

      // 출력형식 지정
      void Print(vector<Student> &v){
        for(int i=0; i<5; i++){
            cout << v[i].name << ", " << v[i].age << '\n';
        }
        cout << endl;
      }

      // 정렬 호출
      sort(v.begin(), v.end());   // [begin, end) 연산자 오버로딩 이용한 정렬

      Print(v);                   // 정렬 후 출력
    ```

  </div>
  </details>  

### 배열 활용
  - 언제 사용?
    - 정렬하고자하는 값이 단순한 값일 경우(int, char)
    - 값의 범위가 작을 때 유용
    - 메모리 제한이 빡셀때 유용
  - 방법
    1. 주어진 범위만큼 배열을 선언
    2. **받은 값을 인덱스 삼아** 배열에 ++
    3. for문으로 앞에서부터 배열을 탐색하면 정렬된 것처럼 사용할 수 있음

### Example
  <details>
  <summary>정렬된 경우, 최빈원소(가장 많이 나타나는 원소) 찾기</summary>
  <div markdown="1">

  ```c
    vector<int> v(n);
    for(auto& i : v)
      cin >> i;

    sort(v.begin(), v.end());

    int res = v[0];
    int res_cnt = 1, tmp = 1;
    for(int i = 1; i < n; i++){
      if(v[i] == v[i-1]) tmp++;     // 이전 원소와 같으면 tmp++
      else tmp = 1;                 // 이전 원소와 다르면 1로 초기화

      if (res_cnt < tmp) {          // 매번! 조건 확인 후에
        res_cnt = tmp;              // 원소 하나 확인 후, 바로 바로 max값 갱신
        res = v[i];
      }
    }
  ```
  </div>
  </details>  

  <details>
  <summary>버블소트 구현</summary>
  <div markdown="1">

  ```c
  //reference를 이용한 call-by-reference
  void Swap(int &num1, int &num2){
      int tmp;
      tmp = num1; //변수 사용하듯 사용하면 됩니다.
      num1 = num2;
      num2 = tmp;
  }

  // BubbleSort
  // int *(&arr) : 배열을 reference를 통해서 call by reference 하는 법(= 포인터를 참조자로 참조하는법)
  void BubbleSort(int *(&arr),int len){
      for(int i=0; i<len-1; i++){
          for(int j=1; j<len -i; j++){
              if(arr[j] > arr[j-1]){ //내림차순
                  Swap(arr[j], arr[j-1]);
              }
          }
      }
  }

  void Solution(string & str){
      int len = (int)str.length();
      int * arr = new int[len];

      // string으로 받은 문자열의 인자를 int type의 배열에 하나씩 넣어줌
      for(int i=0; i<len; i++) {
          arr[i] = str[i] -'0';
      }

      BubbleSort(arr, len);

      for(int i=0; i<len; i++){
          cout << arr[i];
      }

      delete []arr;
  }


  int main(void){

      string str;

      cin>>str;
      Solution(str);

      return 0;
  }
  ```

  </div>
  </details>    
