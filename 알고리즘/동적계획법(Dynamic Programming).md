# 동적 계획법(DP, Dynamic Programming)
## 동적 계획법이란?
> Richad Bellman이 고안한 알고리즘으로, 문제를 각각 작은 문제로 나누고 그 결과를 큰 문제를 해결할 때 사용하는 방식
- 배낭문제, 피보나치 등

## 조건
- 최적 부분 구조 : 문제의 최적해가 부분 문제의 최적해를 포함하는 구조
	- 큰 문제의 최적해가 부분 문제의 최적해들로써 구성되어있어야 함
- 부분 문제 반복 : 재귀를 통해 문제를 해결할 때 같은 부분 문제를 계속 반복하여 해결해야하는 경우
	- 분할정복은 작은 문제 내 반복이 일어나지 않음
	- 예) 병합정렬(merge sort), 퀵정렬(quick sort)

## 구현 방식
### 1. Bottom-up 방식(반복)
- 아래서부터 계산 수행하고 누적하여 큰 문제 해결
- Tabulation: 반복문을 통해 dp[0]부터 채워나가는 "table filling" 후, 배열(table)에 저장된 값에 접근(재활용) 함
```java
public int fibo(int n) {
	int[] dp = new int[n+1];
    dp[0] = 0; 
	dp[1] = 1;
    
    for (int i=2; i<=n; i++) {
    	dp[i] = dp[i-1] + dp[i-2]; 
    }
    
    return dp[n];
}
```
### 2. Top-down 방식(재귀)
- 위에서부터 큰 문제를 해결하기 위해 작은 문제들의 상태로 내려가 이를 통해 큰 문제를 해결하는 방식
- Memoization: 구현 결과를 메모리 공간에 저장해주고 다시 호출될 경우 이 값을 가져옴
- 메모리 공간을 차지하기 때문에, 연속적이지 않은 값이 필요한 경우 key:value 형식의 자료형으로 저장하는 것이 효율적임

```java
static int[] dp;

public void getFibo(int n) {
	dp = new int[n];
	System.out.println(fibo(n));
}

public int fibo(int n) {
	if (n == 0) return 0;
    if (n == 1) return 1;
    if (dp[n] != 0) return dp[n];
    dp[n] = fibo(n-1) + fibo(n-2);
    return dp[n];
}
```
## 분할정복과 비교
- 공통점
	- 큰 문제를 작은 단위로 분할
- 차이점
	- DP
		- 부분 문제 반복이 발생하여, 상위문제 해결 시 재활용 됨
		- Memoization 기법 사용
	- 분할정복
		- 부분 문제가 반복되지 않음
		- Memoization 사용 X

---
## 번외
## Merge sort
- John von Neumann이 고안
### 과정
1. 리스트의 길이가 0 또는 1이면 정렬된 것으로 간주
2. 리스트 길이가 2이상인 경우 리스트를 절반으로 나누어 비슷한 크기의 두 부분 리스트로 분할
3. 각 부분 리스트를 재귀
4. 두 부분 리스트를 다시 하나의 정렬 리스트로 병합
<img src = "https://gmlwjd9405.github.io/images/algorithm-merge-sort/merge-sort-concepts.png">  
<img src = "https://gmlwjd9405.github.io/images/algorithm-merge-sort/merge-sort.png">

### 장단점
- 단점
	- 임시 배열이 필요
	- 레코드의 크기가 큰 경우 이동 횟수가 많아져 시간 복잡도 증가
- 장점
	- 데이터 분포에 영향을 받지 않음(O(nlong2n)으로 동일)
	- LinkedList로 구현할 경우, 임시배열 불필요
	- 크기가 큰 레코드를 정렬할 경우 LinkedList를 사용하면, 정렬 방법 중에 가장 효율적임
<img src="https://gmlwjd9405.github.io/images/algorithm-merge-sort/sort-time-complexity.png">

## Quick sort
- https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html

## 빠른 거듭제곱 알고리즘
- 행렬 A의 n거듭제곱 구하기
- A * A * A * ... * A는 시간 복잡도 O(n)
- n이 짝수일 경우, A^n = (A^2)^(n/2)
- n이 홀수일 경우, A^n = A*A^(n-1)
- n이 0이면 종료
- 시간복잡도 향상 : O(logN)
- 2^5 구하기
	```
	n = 5
	res = 1

	2^5 = 2 * 2^4  (n이 홀수일 때 밑을 하나 꺼내서 n을 짝수로 만든다) -> n = 4
	res = res * 2; (꺼낸 수를 결과값에 저장한다) res = 2

	2^4 = (2^2)^2 = 4^2 (n이 짝수일 때 밑을 제곱하고 n을 2로 나눈다) -> n = 2

	4^2 = 16^1 (n이 짝수일때 밑을 제곱하고 n을 2로 나눈다) -> n = 1

	16^1 = 16 * 16^0 = 16 (n이 홀수일 때 밑을 하나 꺼내서 n을 짝수로 만든다) -> n = 0

	res = res * 16; (꺼낸 수를 결과값에 저장한다) res = 32

	n == 0이면 종료
	```
---

## 참고자료
- https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html

