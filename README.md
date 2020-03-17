# PythonDataStructure
study Data Structure with python

# I) 기본 자료형

 ## 1. 정적 배열 (static array)
 
  - 크기가 고정돼 있다.
  - 같은 타입의 데이터만 담을 수 있다.
  - 접근 : O(1)
  - 탐색 : O(n)
  
 ## 2. 동적 배열 (dynamic  array)
 
  - 정적 배열로 만들어진 자료 구조
  - 정적 배열의 크기를 상황에 맞게 조절한다.
  - 추가 연산 :
   - 정적 배열에 남는 공간이 있을때 O(1)
   - 정적 배열에 남는 공간이 없을때 O(n)
  - 삽입 연산 :
   - 정적 배열에 남는 공간이 있을때 O(n)
   - 정적 배열에 난는 공간이 없을때 O(n)
   
 |        | static array | dynamic array |
 | ------ | ------------ | ------------- |
 | Access | O(1) | O(1) |
 | Search | O(n) | O(n) |
 | Insert | N/A | O(n) or O(1) |
 | Delete | N/A | O(n) or O(1) |
 
