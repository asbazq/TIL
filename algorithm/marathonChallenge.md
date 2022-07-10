# 약수의 개수와 덧셈

class Solution {
    public int solution(int left, int right) {
        int answer = 0;

        for (int i = left; i <= right; i++ ) {
            int cnt = 0; // 다음 숫자로 넘어갈 때 count초기화

            for (int j = 1; j <= i; j++) {
                if (i%j==0) cnt++; // 약수 개수
            }
            if (cnt % 2 == 0) answer += i; // 약수의 개수 짝,홀 확인
            else answer -= i;
        }
            return answer;
    }
}

# 약수의 합

      class Solution {
          public int solution(int n) {
              int answer = 0;
               for (int i = 1; i <= n; i++) { // 약수이므로 1부터 int n까지
                  if (n % i == 0) answer += i;  // 약수 구하는 식
              }
              return answer;
          }
      }

# 예산

        import java.util.Arrays;

        class Solution {
         public int solution(int[] d, int budget) {
                int answer = 0;
                Arrays.sort(d); // 정렬하여 작은 수 먼저

                for (int i = 0; i < d.length; i++) {
                    budget -= d[i]; // 예산에서 빼줌
                    if (budget < 0) break;
                    answer++;
                }
                return answer;
            }
        }
        
# 최대공약수와 최소공배수
        
            public int[] solution(int n, int m) {
            int[] answer = new int[2];
            int big = Math.max(n, m);
            int small = Math.min(n, m);

            answer[0] = gcd(big, small);
            answer[1] = big * small / answer[0];

            return answer;
        }

        static int gcd(int a, int b) {
            if (a % b == 0) {
                return b;
            }
            return gcd(b, a % b);
        }
    }
    
* 유클리드 호제법 사용

![image](https://user-images.githubusercontent.com/107836678/178115562-18f86fc3-7288-4f60-b2c6-6d1553ce92d2.png)

# K번째수

        import java.util.ArrayList;
        import java.util.Arrays;
        import java.util.Collections;

        public class Solution {
            public int[] solution(int[] array, int[][] commands) {
                int[] answer = new int[commands.length];

                ArrayList<Integer> ary = new ArrayList<>();
                for (int i = 0; i < commands.length; i++) {
                    for (int j = commands[i][0]; j <= commands[i][1]; j++) { 
                        ary.add(array[j-1]); // n번째 숫자는 배열[n-1]이기 때문에 -1
                        Collections.sort(ary);
                    }
                    answer[i] = ary.get(commands[i][2] - 1); // n번째 숫자는 배열[n-1]이기 때문에 -1
                    ary.clear();
                }

                return answer;
            }
        }


* 다른 풀이

        import java.util.*;
        class Solution {
            public int[] solution(int[] array, int[][] commands) {
                int[] answer = new int[commands.length];

                for (int i = 0; i < commands.length; i++) {
                    int[] temp = Arrays.copyOfRange(array, commands[i][0] - 1, commands[i][1]); 
                                           // 원본 배열, 복사할 시작인덱스, 복사할 끝인덱스

                    Arrays.sort(temp); // 배열 오름차순 정렬
                    answer[i] = temp[commands[i][2] - 1];
                }
                return answer;
            }
        }
        
* Arrays.copyOfRange(원본 배열, 복사할 시작인덱스, 복사할 끝인덱스)
