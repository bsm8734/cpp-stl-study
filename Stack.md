# Stack
  - 한쪽에서만 자료를 넣고 뺄 수 있는 자료구조
  - LIFO (Last-in First-out)
  - 어댑터 컨테이너
    + vector, deque, list container에 붙어서(기반으로) 사용이 가능
    + 내부적으로는 vector, deque, list container의 구조로 구현이 되어있되,
    stack이라는 포장지로 잘 감싸서 stack과 같이 작동하도록 멤버 함수 등을 지원해 주는 것
    + default: deque container 기반으로 작동
  - 활용: 문자열 뒤집기, 괄호(짝)검사, 후위표기식 계산, 중위표기식을 후위표기식으로 변환, DFS, 뒤로가기, Call Stack


  ```c
  #include <stack>

  stack<int> st;

  st.push(2);
  st.pop();

  st.push(1); st.push(2); st.push(3);
  st.top();   // 3
  st.size();  // 3

  while(!st.empty()) {  // st 안의 모든 원소를 제거
    st.pop();
  }
  // st.clear() 존재하지 않음
  // 스택이 비었는데 pop하려하면 에러 발생
  ```

> stack은 세로로 길고(위에서 접근), queue는 가로로 길기(옆/앞에서 접근) 때문에 가장 우선원소에 접근하는 함수명이 다르다  
이 외에 다른 함수는 대부분 비슷  
`stack.top()` vs. `q.front()`
