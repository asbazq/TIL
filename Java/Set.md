# Set

## Set

set은 중복값을 허용하지 않기 때문에 동일한 값은 하나만 들어가게 된다. 

또한 삽입 시 순서(인덱스)가 없기 때문에 배열(Array)이나 List 처럼 .get(인덱스)로 값을 가져올 수 없고 

Iterator를 통해 가져와야 하는데 set.iterator()로 set 값을 iterator에 담은 후 .next를 통해 하나씩 뽑아내는 식이다

> 사실 대부분의 경우에는 넣은 값의 hashCode값에 따라 순서가 정해져 나오게 된다

## HashSet

Set<E> 객체명 = new HashSet<E>(); // HashSet 생성자

  ## TreeSet
  
  중복된 데이터를 저장할 수 없고 입력한 순서대로 값을 저장하지 않는다. 
  TreeSet은 기본적으로 **오름차순으로 데이터를 정렬**

  ## LinkedHashSet
  LinkedHashSet도 중복된 데이터를 저장할 수 없다. 
  **입력된 순서대로 데이터를 관리**
  
  ## 주요 메소드
  
Set에 값 추가하기 set명.add("값");

Set 크기 확인하기 set명.size();

Set 내용 출력할 수 있게 Iterator 안에 담기 Iterator<데이터타입> iterator명 = set명.Iterator();

Iterator 안에 담은 set 출력하기 Iterator명.next();

or

while(iterator명.hasNext()) {

iterator명.next(); // 값 없을때까지 계속 출력

}
  
  ![set api](https://mblogthumb-phinf.pstatic.net/MjAxNzA0MjhfMjQ4/MDAxNDkzMzkwOTg3NDA4.87xH0xjzS8jOW8Y0OTA-liTaOUEQUrzkRBwE7N71O0Yg.zNyDW48QICuPvpTlE1UB6yTCIIyZ4E6CIZBDgLcvhY4g.PNG.heartflow89/image.png?type=w800)

  
  ## LinkedSet
  
  - 다른 Set들과 동일하게 중복은 허용하지 않으나 .add() 한 순서대로 값이 저장된다
  
  ## TreeSet
  
  - 오름차순으로 값을 정렬해 가지고 있으며 다른 set보다 대량의 데이터를 검색할 시 훨씬 빠르다
  
  ex) 
  
    import java.util.HashSet;
    import java.util.Iterator;

    public class SetTest {

    public static void main(String[] args) {
      HashSet<String> set = new HashSet<String>(); // set 선언

      set.add("a");
      set.add("b");
      set.add("b"); // set에 중복값 저장 불가 
      set.add("c"); // set에 값 담기

      System.out.println("set 크기 확인 : " + set.size());

      Iterator<String> iter = set.iterator(); // set을 Iterator 안에 담기
      while(iter.hasNext()) { // iterator에 다음 값이 있다면
        System.out.println("iterator : " + iter.next()); // iter에서 값 꺼내기
        }
      }
    }
