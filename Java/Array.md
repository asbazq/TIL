# Array

배열은 크기가 정해진 데이터의 공간입니다. 한 번 정해지면 바꿀 수 없어요

배열은 인덱스를 부여받고 인덱스를 통해 즉시 접근이 가능합니다.(O(1)) 

배열은 원소를 중간에 삽입/삭제 하려면 모든 원소를 다 옮겨야 합니다.

최악의 경우 배열의 길이 N 만큼을 옮겨야 하므로 O(N)의 시간 복잡도를 가집니다.

소를 새로 추가하려면, 새로운 공간을 할당해야 하므로 매우 비효율적인 자료구조입니다.


# ArrayList

배열과의 차이점은 배열이 크기가 고정인 반면 ArrayList는 크기가 가변적으로 변합니다.

내부적으로 저장이 가능한 메모리 용량(Capacity)이 있으며 현재 사용 중인 공간의 크기(Size)가 있습니다.

만약 현재 가용량(Capacity) 이상을 저장하려고 할 때 더 큰 공간의 메모리를 새롭게 할당합니다.

ArrayList는 한 덩어리의 큰 배열을 사용하는 방식입니다.

 > 추가, 삭제, 변경, 유무확인(contains,indexOf), 출력(for-each 반복문, get(), iterator, listIterator의 경우 생성 시 ArrayList의 크기를 입력해주고 역방향 가능)
 
 ArrayList를 생성할 때 Set이나 다른 ArrayList를 전달하면 해당 Collections의 값들로 초기화됩니다.

마지막으로 가변 인자를 전달받는 Arrays.asList()를 사용하면 기본 값들로 생성 가능합니다.

# LinkedList

ArrayList는 배열을 사용해서 List를 구현한 클래스입니다.

ArrayList와 다르게 LinkedList는 각각의 노드를 연결하는 방식을 사용합니다.

LinkedList를 화물열차라고 했을 때 화물칸은 노드, 연결고리는 포인트

LinkedList는 양방향 연결 리스트(Doubly Linked List)로 구현되어 있습니다.

각각의 데이터가 노드(Node)로 구성되어 연결이 되는 구조입니다.

각각의 노드는 데이터와 함께 next(다음 노드)와 prev(이전 노드) 값을 내부적으로 가지고 있습니다.

일반적으로 LinkedList의 장점은 데이터를 추가하거나 삭제하는 것이 원활하다는 점입니다.

 > ArrayList와 기능 동일

그래서 주로 ArrayList는 검색이 많은 경우에 사용하고 LinkedList는 잦은 삽입/삭제 시 사용합니다.

일반적으로 new LinkedList<>()와 같이 타입을 생략한 형태로 초기화를 진행합니다.

Set이나 다른 ArrayList 등을 전달해서 해당 값으로 초기화하는 것도 가능합니다.

Arrays.asList로 한 번에 여러 개의 값을 입력하면서 초기화시키는 방법도 존재합니다. 

> LinkedList<Integer> integers4 = new LinkedList<>(Arrays.asList(1, 2, 3, 4, 5)); // Arrays.asList()

ArrayList와 다른 점은 가용량이 의미가 없기 때문에 가용량을 받는 생성자가 존재하지 않는다는 점입니다.
  
  ### Array와 LinkedList의 차이
  
  ||Array|LinkedList|
  |:--:|:--:|:--:|
  |특정 원소 조회|O(1)|O(N)|
  |중간에 삽입 삭제|O(N)|O(1)|
  |데이터 추가|데이터 추가 시 모든 공간이 다 차버렸다면 새로운 메모리 공간을 할당받아야 한다 |모든 공간이 다 찼어도 맨 뒤의 노드만 동적으로 추가하면 된다.|
  |정리|데이터에 접근하는 경우가 빈번하다면 Array를 사용하자|삽입과 삭제가 빈번하다면 LinkedList를 사용하는 것이 더 좋다.|
