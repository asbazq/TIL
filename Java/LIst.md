# List

## List의 특징

1. 크기를 자유롭게 설정 가능

    - 배열은 처음 크기를 설정하고 나서부터는 크기 설정이 불가능하지만 리스트는 삽입과 삭제로 원하는대로 크기를 변경할 수 있다

2. 배열은 직접 액세스(Direct access), 순차 액세스(Sequential Access) 모두 가능, List는 순차 액세스만 가능

   - 직접 액세스(Direct Access)는 배열의 값으로 바로 접근하는 것을 말하고 순차 액세스는(Sequential Access)는 처음부터 시작해 배열의 특정 값까지 접근하는 것을 말한다

   - 직접 액세스가 훨씬 더 빠르게 접근할 수 있기 때문에 배열 안에 값을 넣거나 가져올 때는 Array가 List보다 더 빠르다

   - List는 삽입, 삭제를 통해 크기를 자유롭게 변경 가능하고(List는 동적으로 크기를 변경 가능) 순차 액세스만 가능하기 때문에 배열보다는 좀 느리다

   - 배열(Array)은 크기를 변경 불가
 
 ## List 선언
 
 ArrayList<데이터형> 리스트명 = new ArrayList<데이터형>();
 
 ArrayList와 LinkedList 두 유형으로 선언이 가능한데 ArrayList는 대량의 데이터 검색에 LinkedList는 대량의 데이터 삽입, 삭제에 유리
 
 ## 주요 메소드
 
 - List 추가
 
리스트명.add("값")


- List 삭제 

리스트명.remove("값");

리스트명.remove(인덱스)

 
- List 값 변경

리스트명.set(인덱스, "바꿀값");

 
- List 크기 확인

리스트명.size();

 
- List에 특정 값 들었는지 확인

리스트명.contains("값");

 
- List가 비었는지 확인

리스트명.isEmpty();

 
- List 안에 List, Set, 배열 전체 더하기

리스트명.addAll(다른컬렉션명(List, Set..));

-배열도 합쳐줄 수 있음

리스트명.addAll(Arrays.asList(배열명)); -- 배열의 경우

출처 : https://wakestand.tistory.com/107
