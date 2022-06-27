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
         
* LocalDate.of(입력날짜), getDayOfWeek()해당 요일

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
