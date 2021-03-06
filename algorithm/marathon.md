# 직사각형 별찍기

         import java.util.Scanner;

         class Solution {
             public static void main(String[] args) {
                 Scanner sc = new Scanner(System.in);
                 int a = sc.nextInt();
                 int b = sc.nextInt();

                 for (int i = 0; i < b; i++) {
                     for (int j = 0; j < a; j++) {
                         System.out.print("*");
                     }System.out.println();
                 }
             }
         }
         
* Scanner 클래스의 특징

1. 기본적인 데이터 타입들을 Scanner 의 메소드를 사용하여 입력받을 수 있다.
ex) 100을 입력하고자 할 때, String(문자열)로 입력받고 싶으면 next() 나 nextLine() 을, int(정수)로 입력받고 싶다면 nextInt() 를 사용하여 입력받으면 알아서 해당 타입으로 입력된다.
2. Scanner 을 사용할 시 util 패키지를 경로의 Scanner 클래스를 호출해야 한다.
ex) import java.util.Scanner
3. 공백(띄어쓰기) 또는 개행(줄 바꿈)을 기준으로 읽는다.
ex) Scanner 의 입력 메소드들은 대부분 공백과 개행(' ', '\t', '\r', '\n' 등등..)을 기준으로 읽는다. 이 덕분에 사용자의 편의에 따라 쉽게 입력을 받을 수 있다.
4. 객체생성 시 Scanner in = new Scanner(System.in)`클래스_이름  객체_이름 = new 클래스_이름()`
>주의할 것은 Scanner 을 생성할 때 System.in 이 들어간다는 점이다.
System.in 은 사용자로부터 입력을 받기 위한 입력 스트림이다.
그렇기 때문에 Scanner 뿐만 아니라 다른 입력 방식들도 사용자로부터 입력을 받기 위해서는 System.in 이 들어간다.

* Scanner 종류

         in.nextByte()		// byte 형 입력 및 리턴
         in.nextShort()		// short 형 입력 및 리턴
         in.nextInt()		         // int 형 입력 및 리턴
         in.nextLong()		// long 형 입력 및 리턴
         in.nextFloat()		// float 형 입력 및 리턴
         in.nextDouble()		// double 형 입력 및 리턴
         in.nextBoolean()	        // boolean 형 입력 및 리턴
         in.next()			// String 형 입력 및 리턴(공백을 기준으로 한 단어를 읽음)
         in.nextLine()	        // String 형 입력 및 리턴 (개행을 기준으로 한 줄을 읽음)        
>char 형(문자)타입으로 받는 메소드는 따로 없다. String으로 받은 뒤, charAt() 메소드로 문자로 반환해야한다.

 next() 와 nextLine() 의 차이 

일단 next() 는 '한 단어' 그러니까 공백을 기준으로 문장 한 개만 읽어 들인다.
nextLine() 은 위와 반대로 '한 줄' 즉, 한 줄에 입력된 여러 문장들을 읽는다.

# 짝수와 홀수

         class Solution {
             public String solution(int num) {
                 return num % 2==0 ? "Even": "Odd";         
             }
         }
         
# 가운데 문자 가져오기

         class Solution {
             public String solution(String s) {
                 return s.length() % 2 ==0 ? s.substring(s.length()/2-1,s.length()/2+1):
                 s.substring(s.length()/2,s.length()/2+1);
             }
         }
다른 방법

         class StringExercise{
             String getMiddle(String word){

                 return word.substring((word.length()-1) / 2, word.length()/2 + 1);    
             }
          }   
* substring(int1,int2)
 int1부터 int2까지 문자열 리턴
 int1만 입력 시 int1 이후로 리턴
 > 범위가 정확히 일치하지 않더라도 시행

# 두 정수 사이의 합

         class Solution {
             public long solution(int a, int b) {
                 long answer = 0;

                 if (a<b) {
                     for (int i = a; i <= b; i++){
                         answer += i;
                     }
                 } else if (a>b) {
                     for (int i = b; i <= a; i++) {
                         answer += i;
                 }
             } else {
                     answer = a;
                 }
                 return answer;
             }
         }
         
다른 방법

         class Solution {

             public long solution(int a, int b) {
                 return sumAtoB(Math.min(a, b), Math.max(b, a));
             }

             private long sumAtoB(long a, long b) {
                 return (b - a + 1) * (a + b) / 2;
             }
         }
> 등차수열의 합 사용

# 문자열을 정수로 바꾸기

         class Solution {
             public int solution(String s) {
             return Integer.parseInt(s);
             }
         }
* parseInt() `parsebyte(),parseLong()... `
  
 String타입의 숫자를 Int타입으로 변환        

# 없는 숫자 더하기

         class Solution {
             public int solution(int[] numbers) {
                 int answer = 10*9/2;

                 for (int i : numbers ) {
                     answer -= i;
                 } 

                 return answer;
             }
         }

# 음양 더하기

         class Solution {
             public int solution(int[] absolutes, boolean[] signs) {
                 int answer =0;

                 for (int i = 0; i < signs.length; i++) {
                     if (signs[i]) {
                         answer += absolutes[i];
                     } else {
                         answer -= absolutes[i];
                     }
                 }
                 return answer;
             }
         }
* 정규 

         class Solution {
             public int solution(int[] absolutes, boolean[] signs) {
                 int answer = 0;
                 for (int i=0; i<signs.length; i++)
                     answer += absolutes[i] * (signs[i]? 1: -1);
                 return answer;
             }
         }
         
# 평균 구하기

         class Solution {
             public double solution(int[] arr) {
                 double answer = 0;
                 double sum = 0;

                 for (int i = 0; i < arr.length; i++) {
                     sum += arr[i];
                     answer = sum/arr.length;
                 }
                 return answer;
             }
         }

# 핸드폰 번호 가리기

         class Solution {
             public String solution(String phone_number) {
                 String answer = "";

                 for (int i =0; i < phone_number.length()-4; i++) {
                     answer += "*";
                 }
                 answer += phone_number.substring(phone_number.length()-4);
                 return answer;
             }
         }
* 다른 방법

         class Solution {
           public String solution(String phone_number) {
              char[] ch = phone_number.toCharArray();
              for(int i = 0; i < ch.length - 4; i ++){
                  ch[i] = '*';
              }
              return String.valueOf(ch);
           }
         }
* `String`.toCharArray

 String(문자열)을 char형 배열로 바꾼다.
 
 # 행렬의 덧셈
 
         class Solution {
             public int[][] solution(int[][] arr1, int[][] arr2) {
                 int[][] answer = {};

                 for(int i=0; i<arr1.length; i++){
                     for(int j=0; j<arr1[0].length; j++){
                         answer[i][j] = arr[i][j] + arr2[i][j];
                     }
                 }
                 return answer;
             }
         }

# x만큼 간격이 있는 n개의 숫자

         class Solution {
             public long[] solution(int x, int n) {
                 long[] answer = new long[n];
                 long add = x;

                 for (int i = 0; i < n; i++) {
                     answer[i] = add;
                     add += x;
                 }

                 return answer;
             }
         }
answer이 Long이므로 x도 Long으로 변환

# 부족한 금액 계산하기

         class Solution {
             public long solution(int price, int money, int count) {
                 long answer = 0;
                 long sum = 0;

                 for (int i = 1; i <= count; i++) {
                     sum += price * i;
                     if (money <= sum) {
                         answer = sum - money;
                     } else {
                         answer = 0;
                     }
                 }

                 return answer;
             }
         }
         
* 다른 방법

         class Solution {
             public long solution(long price, long money, long count) {
                 return Math.max(price * (count * (count + 1) / 2) - money, 0);
             }
         }
         
# 2016년

         import java.time.*;
         class Solution {
           public String solution(int a, int b) {
               return LocalDate.of(2016, a, b).getDayOfWeek().toString().substring(0,3);
           }
         }
         
* LocalDate.of(입력날짜)**날짜 정보**만 출력 객체 생성 시 LocalDate targetDate = LocalDate.of(2019,11,12)`클래스_이름  객체_이름 = new 클래스_이름()`, [참고블로그](https://java119.tistory.com/52)
* LocalTime **시간 정보**
* LocaldateTime **날짜 시간 정보**
* `LocaDate.of()`.getDayOfWeek()해당 요일
* `객체`.plusyears(),minusyears()... 년,월, 일...더하기 빼기
* Localdate를 사용할 시 time 패키지를 경로의 Localdate 클래스를 호출해야 한다. ex) import java.time.LocalDate

* 다른방법

        class Solution {
           public String solution(int a, int b) {
               String answer = "";

               int[] c = {31,29,31,30,31,30,31,31,30,31,30,31};
               String[] MM ={"FRI","SAT","SUN","MON","TUE","WED","THU"};
               int Adate = 0;
               for(int i = 0 ; i< a-1; i++){
                   Adate += c[i];
               }
               Adate += b-1; // 1월 1일 시작     
               answer = MM[Adate %7];

               return answer;
           }
         }
         
# 나누어 떨어지는 숫자 배열

         import java.util.ArrayList;
         import java.util.Arrays;

         class Solution {
             public int[] solution(int[] arr, int divisor) {
                 int[] answer = {};


                 ArrayList<Integer> array = new ArrayList<Integer>();

                 for (int i = 0; i < arr.length; i++) {
                     if (arr[i] % divisor == 0) {
                         array.add(arr[i]);
                     }
                 }
                 if (array.isEmpty()) {
                     array.add(-1);
                 }

                 answer = new int[array.size()];
                 for (int i = 0; i < array.size(); i++) {
                     answer[i] = array.get(i);

                 }

                 Arrays.sort(answer);
                 return answer;
             }
         }
         
* ArrayList

ArrayList클래스는 패키지에서 찾을 수 있는 크기 조정 가능한 배열
내장 배열(List)와의 차이점은 배열(List)은 크기가 고정적이다(배열에 요소를 추가하거나 배열에서 제거하려면 새 배열을 만들어야 함). 
반면 ArrayList는 가변적으로 원할 때마다 추가 및 제거가능.

         import java.util.ArrayList; // import the ArrayList class

         ArrayList<String> cars = new ArrayList<String>(); // Create an ArrayList object
         
         
**생성구문**

         ArrayList<Integer> integers1 = new ArrayList<Integer>(); // 타입 지정
         ArrayList<Integer> integers2 = new ArrayList<>(); // 타입 생략 가능
         ArrayList<Integer> integers3 = new ArrayList<>(10); // 초기 용량(Capacity) 설정
         ArrayList<Integer> integers4 = new ArrayList<>(integers1); // 다른 Collection값으로 초기화
         ArrayList<Integer> integers5 = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5)); // Arrays.asList()
         
**메소드**

         `Array`.add(Object) // ArrayList의 마지막에 데이터를 추가.
         `Array`.add(int index, Object) //ArrayList의 index에 데이터를 추가.
         `Array`.set(int index, Object) // index 위치 값 변경
         `Array`.remove(Object) // Object를 파라미터로 넘기는 경우 해당 ArrayList의 Object와 같은 값을 삭제.
         `Array`.remove(int index) : ArrayList의 index에 해당하는 값을 삭제.
         `Array`.size() // ArrayList의 크기.
         `Array`.get(int Index) // ArrayList 출력.
         `Array`.contains // 값이 있는지 여부만 파악.
         `Array`.ndexOf // 값의 위치Index를 찾아주고 값이 없다면 -1을 출력.
         import java.util.Arrays  // Import the Arrays class
          Arrays.sort(`Array`) // 정렬
          
 * Iterator 
 
-ArrayList 및 HashSet과 같은 컬렉션을 반복하는데 사용할 수 있는 개체
 
-컬렉션 프레임워크에서 저장된 요소를 읽어오는 방법을 표준화하기 위한 역할(인터페이스)

-Collection의 하위 컬렉션들이 소유 -> Iterator 타입의 객체를 반환하는 메소드를 이미 구현

-List, Set계열에 구현(Map은 없음)

-주로 읽기 전용으로 사용한다.
 
 **구성**
 
          Iterator<Integer> it = numbers.iterator();
 
          public interface Iterator {
          boolean hasNext(); //읽어 올 요소가 남아있는지 확인하는 메소드. 있으면 true, 없으면 false를 반환
          Object next(); // 읽어 올 요소가 남아있는지 확인하는 메소드. 있으면 true, 없으면 false를 반환
          void remove(); //  next()로 읽어 온 요소를 삭제. next() 를 호출한 다음에 remove() 를 호출해야 한다
          }
          
 **List에 데이터를 담고 반복**
 
          1. for 문

         for( int i =0; i<list.length; i++){

         출력문( list.get(i) );

         }



         2. for-each문(향상된 for문)

         for( String str : list ){

         출력문( str );

         }



         3. Iterator 반복자

         Iterator<String> iter = list.iterator();

         while(iter.hasNext()){ //얘는 true, false 반환, 있으면 true, 없으면 false 

                  System.out.println(iter.next());

         }
         
# 내적

         class Solution {
             public int solution(int[] a, int[] b) {
                 int answer = 0;

                 for (int i = 0; i < a.length; i++) {
                     answer += a[i]*b[i];
                 }
                 return answer;
             }
         }

# 문자열 내 p와 y의 개수

         class Solution {
             boolean solution(String s) {

                 int count = 0;
                 s = s.toLowerCase();

                 for (int i = 0; i < s.length(); i++) {
                     if (s.charAt(i) == 'p') count++;
                     if (s.charAt(i) == 'y') count--;
                 }

                 System.out.println("Hello Java");

                  return count == 0;
             }
         }

* 정규 표현식

         class Solution {
             boolean solution(String s) {
                 s = s.toUpperCase();

                 return s.chars().filter( e -> 'P'== e).count() == s.chars().filter( e -> 'Y'== e).count();
             }
         }

상시 사용 가능 공부하기

# 문자열 다루기 기본

         class Solution {
             public boolean solution(String s) {
                 boolean answer = true;

                 if (s.length() != 4 && s.length() != 6) return false;
                 for (int i = 0; i < s.length(); i++) {
                     if (s.charAt(i) > 0 || s.charAt(i) < 9) return true;
                     }
                 return answer;
             }
         }
         
* 논리 연산자

&&(and), ||(or), !(not) => a != b => !a.equals(b)

* 다른 풀이

         class Solution {
           public boolean solution(String s) {
               if(s.length() == 4 || s.length() == 6){
                   try{
                       int x = Integer.parseInt(s);
                       return true;
                   } catch(NumberFormatException e){
                       return false;
                   }
               }
               else return false;
           }
         }

* NumberFormatException

문자를 숫자로 변경시도하다가 에러가 발생하는 경우, try catch 사용하여 해결

* 정규표현식

         import java.util.*;

         class Solution {
           public boolean solution(String s) {
                 if (s.length() == 4 || s.length() == 6) return s.matches("(^[0-9]*$)");
                 return false;
           }
         }
         
         class Solution {
           public boolean solution(String s) {
             return (s.length() != 4 && s.length() != 6) || (s.split("[0-9]").length > 0) ? false:true;
           }
         }
![정규표현식 문법](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fq0afr%2Fbtq1bfbtrXL%2Fd8M2EshAkkHiAZeEBNswzK%2Fimg.png)
![정규표현식 문법](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Ft37Zg%2Fbtq09yiJ8mu%2FeIaCNKqj1kDfjT8vJjY0ek%2Fimg.png)
 
 **자주사용하는 정규표현식**
 
![자주사용](https://velog.velcdn.com/images%2Fsongs4805%2Fpost%2F261bdd15-7efd-49b0-b08b-20351a26a9d1%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-09-04%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.03.00.png)

# 서울에서 김서방 찾기

         class Solution {
             public String solution(String[] seoul) {
                 String answer = "";

                 for (int i = 0; i < seoul.length; i++) {
                     if (seoul[i].equals("Kim") ) {
                         answer = "김서방은 " + i + "에 있다";
                     }
                 }
                 return answer;
             }
         }
         
* ==와 equals 차이

 == 연산자는 비교하고자 하는 두개의 대상의 **주소값**을 비교, String클래스의 equals 메소드는 비교하고자 하는 두개의 대상의 **값 자체**를 비교
문자열을 비교하려면 equals라는 메서드를 활용하여 두개의 값을 비교해주어야 한다.

# 수박수박수박수박수박수?

         class Solution {
             public String solution(int n) {
                 String answer = "";

                 for (int i = 0; i < n; i++) {
                     if (i % 2 ==0) {
                         answer += '수';
                     } else { answer += '박';
                     }
                 }
                 return answer;
             }
         }
         
# 완주하지 못한 선수

         import java.util.HashMap;

         class Solution {
             public String solution(String[] participant, String[] completion) {
                 String answer ="";
                 HashMap<String, Integer> map = new HashMap<>(); // 해쉬맵 선언 key는 String형태, value는 integer형태
                 for(String par : participant) map.put(par, map.getOrDefault(par, 0) + 1); // for each문을 통해 hashmap에 participant 하나씩 꺼내 map에 넣어 값에+1, 동명이인을 판단하기 위해 map.getOrDefault(par, 0)사용, 동명이인이 있다면 participant의 value를 가져져와 더한다.
                 for(String par : completion) map.put(par, map.get(par) -1 ); // for each문을 통해 hashmap에 participant 하나씩 꺼내 map에 넣어 값에-1
                 for(String key : map.keySet()) {                                                  
                  if(map.get(key) != 0) { // value값이 0이 아닌 값을 출력
                           answer = key;
                           System.out.println(answer);
                           break;
                  }
                 }
                 return answer;
             }
         }
         
* 다른 풀이

         import java.util.*;
         class Solution {
             public String solution(String[] participant, String[] completion) {
                 Arrays.sort(participant); // 선 정렬
                 Arrays.sort(completion);
                 int i;
                 for ( i=0; i<completion.length; i++){ // 정렬로 같아진 순서로 비교

                     if (!participant[i].equals(completion[i])){
                         return participant[i]; // 일치하지 않는 participant 출력
                     }
                 }
                 return participant[i]; // 끝까지 돌았다면 마지막 participant 
             }
         }

 
 * 해쉬맵

   - 해시맵은 이름 그대로 해싱(Hashing) <sup> 반복비교를 하지않고 키값을 사용하여 바로 값에 접근 </sup> 된 맵(Map).<sup> 키(Key)와 값(Value) 두 쌍으로 데이터를 보관하는 자료구조</sup> 키는 고유값, 값은 중복가능
   -  배열과 연결이 결합된 형태.
   -  hashing 기법을 사용하기 때문에 많은 양의 데이터가 저장될때 유용, 검색에 최고성능을 보인다.
   -  추가/삭제/검색/접근성이 모두 뛰어나다.
   -  순서가 유지되지 않는다. (순서유지가 필요하다면 LinkedHashMap을 사용한다.)


 * 메소드


         import java.util.HashMap; // HashMap을 사용할 시 util 패키지를 경로의 HashMap 클래스를 호출
         
         HashMap<String,String> map = new HashMap<String,String>(); // HashMap선언
         
         map.put(key,value); //값 추가
         
         map.remove(1); //key값 1 제거
         
         map.clear(); //모든 값 제거

         출력

         System.out.println(map); //전체 출력 : {1=사과, 2=바나나, 3=포도}

         System.out.println(map.get(1));//key값 1의 value얻기

         for(Integer i : map.keySet()){ // keySet() 메서드는 key의 값만 출력, 모든 키를 순회
             System.out.println("[Key]:" + i + " [Value]:" + map.get(i))

         for (Entry<Integer, String> entry : map.entrySet()) { //entrySet() 메서드는 key와 value의 값 모두 출력
              System.out.println("[Key]:" + entry.getKey() + " [Value]:" + entry.getValue());

# 이상한 문자 만들기

         class Solution {
             public String solution(String s) {
                 String answer = ""; // 입력값에 ""가 붙어있어 제거
                 s = s.toLowerCase();
                 String[] str = s.split("");
                 int uper = 0;


                 for (int i = 0; i < str.length; i++) {
                     if (str[i].equals(" ")) {
                         uper = 0; 
                     } else if (uper % 2 == 0) {
                         str[i] = str[i].toUpperCase();
                         uper++;
                     } else {
                         uper++; // uper로 홀짝 구별 빈칸인 경우 0으로 처리하여 다음 문자 짝수 판정
                     }
                     answer += str[i];
                 }
                 return answer;
             }
         }

# 자릿수 더하기

         import java.util.*;

         public class Solution {
             public int solution(int n) {
                 int answer = 0;

                 while (n > 0){
                     answer += n % 10; // 
                     n/=10;
                 }
                 // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
                 System.out.println("Hello Java");
                 return answer;
             }
         }
         
* 다른 풀이

         public class Solution {
             public int solution(int n) {
                 int answer = 0;
                 String s = Integer.toString(n); //int n을 String으로 변환

                 for(int i=0; i<s.length(); i++){
                     answer += Integer.parseInt(s.substring(i, i+1));
                 }
                 return answer;
             }
         }
         
# 자연수 뒤집어 배열로 만들기
         
         class Solution {
             public int[] solution(long n) {
                 String s = String.valueOf(n);
                 StringBuilder sb = new StringBuilder(s); // reverse메소드를 쓰기위해 Stringbuilder 사용
                 sb = sb.reverse();
                 String[] stringarr =sb.toString().split("");
                 int[] answer = new int[sb.length()];
                 for (int i = 0; i < sb.length(); i ++) {
                     answer[i] = Integer.parseInt(stringarr[i]);
                 }
                 return answer;
             }
         }
         
* point

class Solution {
  public int[] solution(long n) {
 
        String a = "" + n; // 문자열 + 숫자 = 문자열을 이용하여 쉽게 long → String으로 할당가능,  String.split("")사용하여 String을 String[]으로 변환가능
        
        int[] answer = new int[a.length()];
        
        int cnt = 0;
        
        while (n > 0) {
 
            // 1) 12345 % 10 = 5
            // 2) 1234 % 10 = 4
            // 3) 123 % 10 = 3
            // 4) 12 % 10 = 2
            // 5) 1 % 10 = 1
            answer[cnt] = (int) (n % 10);
 
            // 12345 = 1234
            // 1234 = 123
            // 123 = 12
            // 12 = 1
            // 1 = 0 ( 0.1 ) // 소수점 시 0이 되는 것을 이용
            n /= 10;
 
            cnt++;
        }      
        return answer;
  }
}
https://retrieverj.tistory.com/42

* String, Stringbuilder, StringBuffer

String은 불변 concat, + 사용 시 기존 값을 버리고 새로 할당해서 느려짐
**but** StringBuffer와 StringBuilder는 유동적으로 사용한다

* StringBuffer, StringBuilder의 차이는?

StringBuffer는 공통 메소드 동기화로 인해 멀티 스레드 환경에서만 사용

그 외에는 StringBuilder를 사용하면 됨

* StringBuffer, StringBuilder의 주요 메소드 

sb.append(값) - StringBuffer, StringBuilder 뒤에 값을 붙인다

sb.insert(인덱스, 값) - 특정 인덱스부터 값을 삽입한다

sb.delete(인덱스, 인덱스) - 특정 인덱스부터 인덱스까지 값을 삭제한다

sb.indexOf(값) - 값이 어느 인덱스에 들어있는지 확인한다

sb.substring(인덱스, 인덱스) - 인덱스부터 인덱스까지 값을 잘라온다

sb.length() - 길이 확인

sb.replace(인덱스, 인덱스, 값) - 인덱스부터 인덱스까지 값으로 변경

sb.reverse() - 글자 순서를 뒤집는다

# 콜라츠 추측

         class Solution {
             public int solution(long num) { // 오버플로우로 int를 long으로 변경
                 int answer = 0;

                 while (num != 1) {
                     if (num % 2 == 0) {
                         num /= 2;
                     } else {
                         num = num*3 + 1;
                     }
                     answer++;

                     if (answer > 500) return -1;
                 }
                 return answer;
             }
         }
         
# 정수 내림차순으로 정렬하기

         import java.util.Arrays;
         import java.util.Collections;

         class Solution {
             public long solution(long n) {

                 String[] s = String.valueOf(n).split("");
                 Arrays.sort(s, Collections.reverseOrder()); //primitive arrays은 Arrays.sort()를 통한 내림차순을 할 수 없다. Object of Array를 사용하면 Collections.reverseOrder()사용 가능
                 StringBuilder sb = new StringBuilder();
                 for (String str : s) sb.append(str);

                 return Long.parseLong(sb.toString());
             }
         }

오름차순 정렬

= Arrays.sort()

내림차순 정렬

= Arrays.sort(arr, Collection.reverseOrder());

# 정수 제곱근 판별

         class Solution {
             public long solution(long n) {
                 long answer = 0;
                 long sqrt = (long) Math.sqrt(n); // 형변환을 통해 long으로 변화시켜 넣음

                 if (Math.pow(sqrt,2)==n) return (long) Math.pow(sqrt+1,2); // solution이 long값이라 long으로 형변환
                 return -1;
             }
         }

* Math.sqrt(n^2)=5, Math.pow(n,2)=n^2

# 제일 작은 수 제거하기
         import java.util.ArrayList;
         import java.util.Arrays;

         class Solution {
             public int[] solution(int[] arr) {

                 if (arr.length <= 1) {
                     int[] answer = {-1};
                     return answer;
                 }
                 int[] answer = new int[arr.length - 1]; // arr.length -1 가장 작은 수 제거한 배열 수
                 int min = arr[0];
                 for (int i = 1; i < arr.length; i++) {
                     min = Math.min(min, arr[i]); // arr[0]인 min과 비교하여 가장 작은 수 출력
                 }
                 int index = 0;
                 for (int i = 0; i < arr.length; i++) {
                     if (arr[i] == min) {
                         continue;
                     }
                     answer[index++] = arr[i]; // 가장 작은 수를 찾을 때까지 배열의 길이 증가
                 }
                 return answer;
             }
         }
         
       
# 하샤드 수

         class Solution {
             public boolean solution(int x) {
                 boolean answer = true;
                 int sum = 0;
                 int num = x; // if문에서 사용하기 위해 x값을 저장

                 while (x > 0) {
                     sum += x % 10;
                     x /= 10;
                 }

                 if (num % sum == 0) {
                     answer = true;
                 } else {
                     answer = false;
                 }
                 return answer;
             }
         }
         
# 3진법 뒤집기

         import java.util.*;
         class Solution {
             public int solution(int n) {
                 int answer = 0;
                 ArrayList<Integer> list = new ArrayList<>();
                 // 10진법 -> 3진법
                 while(n != 0) {
                     list.add(n%3);
                     n /= 3;
                 } 
                 // 3진법 -> 10진법
                 int tmp = 1;
                 for(int i=list.size()-1;i>=0;i--) { 
                     answer += list.get(i)*tmp;
                     tmp *= 3;
                 }
                 return answer;
             }
         } 
         
* 다른 풀이

         import java.util.*;
         class Solution {
             public int solution(int n) {
                 int answer = 0;
                 String ans = "";
                 while(n != 0) {
                     ans += n%3; // String을 사용하여 숫자 배열 ex) String "1234", Array {"1","2","3","4"}
                     n /= 3;
                 }
                 return Integer.parseInt(ans, 3); // int 10진법으로 변환
             }
         }
         
> 진법 변환
        
         N진법 -> 10진법
         Integer.parseInt(i, N);
         10진법 -> N진법
         Integer.toBinaryString(number); // 2진법
         Integer.toOctalString(number); // 8진법
         Integer.toHexString(number); // 16진법

# 최소직사각형

         class Solution {
             public int solution(int[][] sizes) {
                 int answer = 0;
                 int maxW = 0;
                 int maxH = 0;
                     for (int i = 0; i < sizes.length; i++) {
                        if (sizes[i][0] < sizes[i][1]) {
                            int tmp = sizes[i][0];
                            sizes[i][0] = sizes[i][1];
                            sizes[i][1] = tmp;
                        }
                        if (maxW < sizes[i][0]) maxW = sizes[i][0];
                        if (maxH < sizes[i][1]) maxH = sizes[i][1]; // 정규표현식 maxw = Math.max(maxw, sizes[i][0] > sizes[i][1] ? sizes[i][0] : sizes[i][1]);
                                                                                  maxh = Math.max(maxh, sizes[i][0] > sizes[i][1] ? sizes[i][1] : sizes[i][0]);

                     }
                     answer = maxH * maxW;
                 return answer;
             }
         }
         
* point

두 값을 swsp 
int tmp = array[i][0];
array[i][0] = array[i][1]; // tmp 임시로 이동할 파일이 지워지지 않게 보관
array[i][1] = tmp;

최대값 구하는 법

if (maxW < sizes[i][0]) maxW = sizes[i][0];

# 2번. 자연수 뒤집어 더하기

          public String solution(int n) {
                 String answer = "";
                 String s = String.valueOf(n); // int n을 String으로 변환
                 int[] rn = new int[s.length()]; // 배열 rn의 크기 부여
                 int sum = 0;
                 int cnt = 0;

                 while (n != 0) { // 자리수 역순으로 구하기
                     rn[cnt] = n % 10;
                     n /= 10;
                     cnt++; // cnt를 사용하여 rn에 순차적으로 스태킹
                 }

                 for (int i = 0; i < rn.length; i++) {
                     sum += rn[i];
                 }

                 StringBuilder sb = new StringBuilder(); // StringBuilder는 일시적 저장소?
                 for (int i = 0; i < rn.length; i++) {
                     sb.append(rn[i]);
                     if (i != rn.length - 1) {
                         sb.append("+"); // sb에 일시적으로 저장
                     } else {
                         sb.append("="); 
                         sb.append(sum);
                     }
                 }


                 answer = sb.toString(); // toString()을 사용하여 저장해논 값을 출력

                 return answer;
             }
         // 출력 값
             public static void main(String[] args) {
                 Main method = new Main();

                 System.out.println(method.solution(718253));
             }
         }
         
#  문자열 내 마음대로 정렬하기

         import java.util.ArrayList;
         import java.util.Collections;

         class Solution {
             public String[] solution(String[] strings, int n) {
                 String[] answer = new String[strings.length];

                 ArrayList<String> ary = new ArrayList<>();
                 for (int i = 0; i < strings.length; i++) {
                     ary.add(strings[i].charAt(n) + strings[i]); // charAt(n)을 이용해서 인덱스 n번째 문자로 정렬  
                 }
                 Collections.sort(ary); // Collections.sort(ary) ArrayList 정렬, Arrays.sort(ary) Array(배열) 정렬

                 for (int i = 0; i < strings.length; i++) {
                     answer[i] = ary.get(i).substring(1); // 배열 answer에 넣어주기 위해 목록액세스로 변환(get사용)
                 }
                 return answer;
             }
         }

# 3번. 같은 단어는 싫어

         public class Main {
             public String[] solution(String[] arr, int n) {
                 String[] answer = new String[arr.length];

                 ArrayList<String> ary = new ArrayList<>();
                 String sameStr = "";
                 for (int i = 0; i < arr.length; i++) {
                     if ( sameStr == arr[i]) {
                         sameStr = arr[i];
                         ary.add(arr[i].charAt(n) + arr[i]);
                     }
                     Collections.sort(ary);
                 }
                 for (int i = 0; i < arr.length; i++) {
                     answer[i] = ary.get(i).substring(1);
                 }

                     return answer;
                 }

                 public static void main(String[] args) {
                     Main method = new Main();
                     String[] arr = {"coke", "water", "glass", "dog", "dog", "yogurt", "vitamin"};
                     int n = 2;
                     System.out.println(Arrays.toString(method.solution(arr, n)));
                 }
             }

# 1번. 행렬 음양 더하기

import java.util.Arrays;

         public class Main {
             public int[][] solution(int[][] arr1, int[][] arr2, boolean[][] signs) {
                 int[][] answer = new int[arr1.length][arr1[0].length]; // arr1.length = 배열의 개수, arr1[0].length = index의 


                 for (int i = 0; i < arr1.length; i++) {
                     for (int j = 0; j < arr1[0].length; j++) {
                         if (signs[i][j]) {
                             answer[i][j] = arr1[i][j] + arr2[i][j];
                         } else {
                             answer[i][j] = -arr1[i][j] - arr2[i][j];
                         }
                     }
                 }
                 return answer;
             }

             public static void main(String[] args) {
                 Main method = new Main();
                 int[][] arr1 = {{5, 7, 1}, {2, 3, 5}};
                 int[][] arr2 = {{5, 1, 6}, {7, 5, 6}};
                 boolean[][] signs = {{true, true, false}, {false, true, false}};
                 System.out.println(Arrays.deepToString(method.solution(arr1, arr2, signs)));
             }
         }

* Array

value안에 index

# 두 개 뽑아서 더하기

         import java.util.ArrayList;
         import java.util.Collections;

             class Solution {
                 public int[] solution(int[] numbers) {


                     ArrayList<Integer> ary = new ArrayList<>();
                     for (int i = 0; i < numbers.length ; i++) {
                         for (int j = i + 1; j < numbers.length; j++) { // 두 수가 겹치지 않도록 j = i + 1
                             int sum = numbers[i] + numbers[j];
                             if (!ary.contains(sum)) ary.add(sum); // 같은 수가 있다면 넣지 않는다
                         }
                     }
                     Collections.sort(ary);
                     int[] answer = new int[ary.size()]; // ary를 뒤에 선언했기에 answer을 밑에서 선언해 준다.
                     for (int i = 0; i < ary.size(); i++) {
                         answer[i] = ary.get(i);
                     }
                     return answer;
                 }
             }

# 로또의 최고 순위와 최저 순위

         class Solution {
             public class solution {
                 public int[] solution(int[] lottos, int[] win_nums) {
                     int[] answer = new int[2];
                     int win = 0;
                     int lose = 0;

                     for (int i = 0; i < lottos.length; i++) {
                         if (lottos[i] == 0) {
                             win += 1;
                             lose += 1;
                         }
                         for (int j = 0; j < lottos.length; j++) {
                             if (lottos[i] == win_nums[j]) win += 1;
                         }
                     }
                     if (win == 6) {
                         answer[0] = 1;
                     } else if (win == 5) {
                         answer[0] = 2;
                     } else if (win == 4) {
                         answer[0] = 3;
                     } else if (win == 3) {
                         answer[0] = 4;
                     } else if (win == 2) {
                         answer[0] = 5;
                     } else {
                         answer[0] = 6;
                     }

                     win -= lose;

                     if (win == 6) {
                         answer[1] = 1;
                     } else if (win == 5) {
                         answer[1] = 2;
                     } else if (win == 4) {
                         answer[1] = 3;
                     } else if (win == 3) {
                         answer[1] = 4;
                     } else if (win == 2) {
                         answer[1] = 5;
                     } else {
                         answer[1] = 6;
                     }

                     return answer;
                 }
             }
         }
         
# 문자열 내림차순으로 배치하기

         import java.util.ArrayList;
         import java.util.Collections;

         class Solution {
             public String solution(String s) {
                 String answer = "";
                 String[] str = new String[s.length()];

                 ArrayList<String> ary = new ArrayList<>(); // 배열 길이가 변화되지 않기 때문에 ArrayList 불필요

                 str = s.split("");
                 for (int i =0; i < s.length(); i++) { // 따라서 추가하는 내용도 불필요
                     ary.add(str[i]);
                 }
                 ary.sort(Collections.reverseOrder());

                 for (int i =0; i < s.length(); i++) {
                     answer += ary.get(i);
                 }
                 return answer;
             }
         }

             // 출력문
             public static void main(String[] args) {
                 StringSort method = new StringSort();
                 String s = "Zbcdefg";
                 System.out.println(method.solution(s));
             }
         }


         
*Character.isUpperCAse(`char배열`) = true // 대문자인지 판단

* 다른 풀이1

         import java.util.*;


         class Solution {
             public String solution(String s) {
                 String answer="";

                 String arr[] = s.split("");

                 Arrays.sort(arr ,Collections.reverseOrder());

                 for(int i=0;i<arr.length;i++){

                     answer += arr[i];
                 }

                 return answer;
             }
         }

* 다른 풀이2

         public String solution(String s) { 
         char[] array = s.toCharArray();
         Arrays.sort(array);
         return new StringBuilder(new String(array)).reverse().toString(); // 선 정렬 후 StringBuilder를 사용하여 뒤집고 String으로 변환하여 출력
         }

# 모의고사

         import java.util.ArrayList;
         import java.util.Arrays;


         class Mock {
             public int[] solution(int[] answers) {
                 int[] num1 = {1,2,3,4,5}, num2 = {2,1,2,3,2,4,2,5}, num3 = {3,3,1,1,2,2,4,4,5,5}; // 규칙을 찾아 넣으면 너무 복잡해져서 하드코딩으로 작업
                 int[] cnt = new int[3]; / 

                 for (int i = 0; i < answers.length; i++) { 
                     if (answers[i] == num1[i%num1.length]) cnt[0]++; // i%length를 통해 반복되는 num를 구현
                     if (answers[i] == num2[i%num2.length]) cnt[1]++;
                     if (answers[i] == num3[i%num3.length]) cnt[2]++; // cnt[]를 통해 해당위치로 고정하여 차후 정렬할 필요X
                 }

                 int max = Math.max(Math.max(cnt[0],cnt[1]), cnt[2]); 
                 ArrayList<Integer> ary = new ArrayList<>(); // 배열의 크기가 변하므로 ArrayList를 사용
                 if (max == cnt[0]) ary.add(1);
                 if (max == cnt[1]) ary.add(2);
                 if (max == cnt[2]) ary.add(3);

                 int[] answer = new int[ary.size()];

                 for (int i = 0; i < answer.length; i++) {
                     answer[i] = ary.get(i);

                 }

                 return answer;
             }
             public static void main(String[] args) {
                 Mock method = new Mock();
                 int[] a = {1,3,2,4,2};
                 System.out.println(Arrays.toString(method.solution(a)));
             }
         }

# 소수 만들기

         import java.util.ArrayList;

         public class Solution {

             public int solution(int[] nums) {
                 int answer = 0;
                 int sum = 0;

                 // 합을 저장할 저장공간 선언
                 ArrayList<Integer> ary = new ArrayList<Integer>();
                 // for문을 이용하여 배열의 합을 구한다.
                 for (int i = 0; i < nums.length; i++) {
                     for (int j = i + 1; j < nums.length; j++) {
                         for (int l = j + 1; l < nums.length; l++) {
                             sum = (nums[i] + nums[j] + nums[l]);
                             if (!ary.contains(sum)) ary.add(sum); // 중복확인
                         }
                     }
                 }

                 // 저장된 합이 소수인지 판별한다.
                 for (int j = 0; j < ary.size(); j++) {
                     int i = ary.get(j);
                     int count = 2; 
                     answer++;
                     while (count < i) {
                         // 저장된 값이 count로 나눴을 때 나머지가 0이라면 소수가 아니기 때문에 answer의 값을 더하지 않는다.
                         if (i % count == 0) {
                             answer--;
                             break;
                         }
                         count++;
                     }
                 }
                 return answer;
             }
           }

# 숫자 문자열과 영단어

* 문자열이 숫자인지 확인하는 방법

  - regex(정규표현식)를 인수로 사용하고true 또는false 부울 값을 반환하는String 클래스의matched()메서드를 사용할 수 있습니다.

         public class SimpleTesting {

             public static void main(String[] args) {
                 String str = "123";
                 boolean isNumeric =  str.matches("[+-]?\\d*(\\.\\d+)?");
                 System.out.println(isNumeric);
                 str = "121xy";
                 isNumeric =  str.matches("[+-]?\\d*(\\.\\d+)?");
                 System.out.println(isNumeric);
                 str = "0x234";
                 isNumeric =  str.matches("[+-]?\\d*(\\.\\d+)?");
                 System.out.println(isNumeric);
             }
         }
     
  - Character클래스의 isDigit()메서드를 사용하여 루프의 각 문자를 확인할 수 있습니다. true또는 false값을 반환합니다.

         public class SimpleTesting {

             public static void main(String[] args) {
                 String str = "1123";
                 boolean isNumeric = true;
                 for (int i = 0; i < str.length(); i++) {
                     if (!Character.isDigit(str.charAt(i))) {
                         isNumeric = false;
                     }
                 }
                 System.out.println(isNumeric);
             }
         }
         
  - Apache를 사용하는 경우StringUtils 클래스의isNumeric()메서드를 사용할 수 있습니다.이 메서드는 숫자 시퀀스가 포함 된 경우true를 반환합니다.


         import org.apache.commons.lang3.StringUtils;

         public class SimpleTesting {

             public static void main(String[] args) {
                 String str = "1123";
                 boolean isNumeric = StringUtils.isNumeric(str);
                 System.out.println(isNumeric);
                 str = "123xyz";
                 isNumeric = StringUtils.isNumeric(str);
                 System.out.println(isNumeric);
             }
         }

  - Double 클래스의parseDouble()메서드를 사용하여 문자열을 double로 변환하고 double 유형 값을 반환 할 수 있습니다. 구문 분석 할 수없는 경우 예외가 발생합니다.

             public class SimpleTesting {

             public static void main(String[] args) {
                 String str = "1123";
                 try {
                 Double.parseDouble(str);
                 System.out.println("It is numerical string");
                 }catch(NumberFormatException e) {
                     System.out.println("It is not numerical string");
                 }
             }
         }
         
   - Java 8 이상 버전

         public class SimpleTesting {

             public static void main(String[] args) {
                 String str = "1123";
                 boolean isNumeric = str.chars().allMatch( Character::isDigit );
                 System.out.println(isNumeric);
                 str = "ab234";
                 isNumeric = str.chars().allMatch( Character::isDigit );
                 System.out.println(isNumeric);
             }
         }
         
  
  * 문제풀이


         public class ChangeNum {
             public int solution(String s) {
                 int answer = 0;
                 String[] num = {"zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine"};

                 for (int i = 0; i < 10; i++) {
                     s = s.replace(num[i],Integer.toString(i)); // 따로 확인할 필요없이 replace를 통해 숫자를 체크하고 변경
                 }
                 answer = Integer.parseInt(s);

                 return answer;
             }
         }

* 여러모로 다양하게 사용되는 replace 

# 시저 암호

             class Solution {
                 public String solution(String s, int n) {
                     String answer = "";

                     for (int i =0; i < s.length(); i++) {
                         char chr = s.charAt(i);

                         if (Character.isLowerCase(chr)) {
                             chr = (char) ((chr - 'a' + n) % 26 + 'a'); // 아스키 코드로 계산하여 chr에 첫문자 a를 빼주어 n을 더해 구함
                         } else if (Character.isUpperCase(chr)) {
                             chr = (char) ((chr - 'A' + n) % 26 + 'A'); // % 26을 통해 z이후는 다시 a부터 
                         }
                         answer += chr;
                     }
                     return answer;
                 }
             }
             
* char는 숫자(아스키 코드)로 저장

# 신규 아이디 추천

         class Solution {
             public String solution(String new_id) {
                 String answer = new_id.toLowerCase(); // 1단계

                 answer = answer.replaceAll("[^-_.a-z0-9]", ""); // 2단계 조건은 그냥 연달아 적으면 됨
                 answer = answer.replaceAll("[.]{2,}", "."); // 3단계
                 answer = answer.replaceAll("^[.]|[.]$", "");    // 4단계

                 if (answer.equals("")) {    // 5단계
                     answer += "a";
                 }

                 if (answer.length() >= 16) {     // 6단계
                     answer = answer.substring(0, 15);
                     answer = answer.replaceAll("[.]$","");
                 }

                 if (answer.length() <= 2) {  // 7단계
                     while (answer.length() < 3) {
                         answer += answer.charAt(answer.length()-1);
                     }
                 }

                 return answer;
             }
         }

