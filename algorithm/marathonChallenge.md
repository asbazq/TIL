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

# 소수 찾기

        class Solution {
            public int solution(int n) {
                int answer = 0;

                for (int i = 2; i <= n; i++) {
                    boolean flag = true;
                    for (int j = 2; j <= Math.sqrt(i); j++) { // Marh.sprt(i)를 사용하여 시간복잡도를 줄임
                        if (i % j == 0) { // 나누어진다면 소수가 아님
                            flag = false; // 해당 변수로 소수인지 아닌지 판단
                            break;
                        } 
                    }
                    if (flag) answer++;
                }
                return answer;
            }
        }
        
# 실패율

        import java.util.Arrays;
        import java.util.HashMap;
        import java.util.Map;

        public class FailRate {
            public int[] solution(int N, int[] stages) {
                int[] answer = new int[N];
                int[] cnt = new int[N]; // 스테이지에 도달했으나 아직 클리어하지 못한 플레이어의 수
                Map<Integer,Double> map = new HashMap<>(); // HashMap을 이용하여 key에는 스테이지 value에는 실패율
                int total = stages.length; // 스테이지에 도달한 플레이어 수

                for (int i = 0; i < stages.length; i++) {
                    int stage = stages[i]; // 스테이지에 도달했으나 아직 클리어하지 못한 플레이어의 수
                    if (stage == N + 1) continue; // 마지막 스테이지는 제외
                    cnt[stage - 1]++; // 배열은 0부터 시작이므로 -1
                }
                for (int i = 0; i < cnt.length; i++) { // 스테이지에 도달한 플레이어 수
                    if (total == 0) { // 플레이어가 0일 때
                        map.put(i,0d); // 0을 삽입
                        continue;
                    }
                    map.put(i, (double) cnt[i] / total); // 실패율
                    total -= cnt[i]; // 이전 층을 뺀 플레이어 수
                }
                for (int i = 0; i < N; i++) {
                    double max = -1; // value값이 0일 수도 있으니까 -1 대입
                    int maxkey = 0;

                    for (int key : map.keySet()) { // map의 키값
                        if (max < map.get(key)) {
                            max = map.get(key); // 최대 값 구함
                            maxkey = key;
                        }
                    }
                    answer[i] = maxkey + 1; // 실패율이 높은 순으로 , 배열은 0부터니까 +1
                    map.remove(maxkey); // maxkey를 지우고 다시 반복
                }
                    return answer;
            }
            public static void main(String[] args) {
                FailRate method = new FailRate();
                int a = 5;
                int[] b = {2, 1, 2, 6, 2, 4, 3, 3};
                System.out.println(Arrays.toString(method.solution(a, b)));
            }
        }

