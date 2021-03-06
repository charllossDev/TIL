# Prime algorithm
소수: 약수가 1과 자기 자신밖에 없는 수

* N이 소수가 되려면, 2보다 크거나 같고, N-1 보다 작거나 같은 수와 나누어 떨어지면 안됨
* N의 소수 구하는 방법
  + 2부터 N-1 까지 수를 나눠서 확인
  * N/2 보다 작거나 같은 수로 나누어 떨어지면 안됨
  * **루트 N 보다 작거나 같은 자연수로 나누어 떨어지면 안됨**
    - `시간 복잡도 루트^N`
    ```java
    private int isPrime(int n) {
      if (n < 2) {
        return 0;
      }
      for (int i = 2; i*i <= n; i++) {
        if (n % i == 0)
          return 0;
      }
      return 1;
    }
    ```

## Multiple Prime Algorithm
M개의 수들 중 소수를 구하는 알고리즘

* 숫자 N의 소수를 판단하는 최단 시간 복잡도 -> 루트 N
* M 개의 숫자들의 소수를 판단하는 시간 복잡도 -> M * 루트 N
  + 찾아야 하는 M개의 숫자가 커질수록 복잡도가 상승
  + M = 1억인 경우, 시간복잡도: 루트 N * 10,000
  + 1,000,000 * 1,000 = 1,000,000,000 = 10억 = `10초`, 너무 오래걸린다
* 이를 해결하기 위해 에라토스테네스의 체를 사용

### Sieve of Eratosthenes
> 에라토스테네스 체

1부터 N까지 범위 안에 들어가는 모든 소수를 구하려면 에라토스테네스의 체를 사용한다.

1. 2부터 N까지 모든 수를 써놓는다.
2. 아직 지워지지 않은 수 중에서 가장 작은 수를 찾는다.
3. 그 수는 소수이다.
4. 이제 그 수의 배수를 모두 지운다.

* M = 100 까지 수 중 소수 구하는 에라토스테네스 체 알고리즘 코드
```java
  int point;
  int n = 100;
  int[] num = new int[n];
  boolean[] check = new boolean[n];

  for (int i = 2; i <= n ; i++) {
    if (check[i] == false) {
      num[point++] = i;
      for (int j = i*i; j <= n; j+=i) {
        check[j] = true;
      }
    }
  }
```  
