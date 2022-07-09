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
