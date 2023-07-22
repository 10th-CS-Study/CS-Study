# 거품 정렬 (Bubble Sort)

_Assembled by GimunLee (2019-10-29)_

<br>

## 목표

- Bubble Sort에 대해 설명할 수 있다.
- Bubble Sort 과정에 대해 설명할 수 있다.
- Bubble Sort을 구현할 수 있다.
- Bubble Sort의 시간복잡도와 공간복잡도를 계산할 수 있다.

<br>

## 요약

Bubble Sort는 Selection Sort와 유사한 알고리즘으로 **`서로 인접한 두 원소의 대소를 비교하고, 조건에 맞지 않다면 자리를 교환하며 정렬하는 알고리즘`** 입니다.

조건문의 부등호 방향에 따라 내림차순으로 정렬할 수도, 오름차순으로 정렬할 수도 있습니다.

정렬 과정에서 원소의 이동이 거품이 수면으로 올라오는 듯한 모습을 보여 Bubble Sort라고 불립니다.

<br>

## 과정

1. 1회전에 1번째 원소와 2번째 원소를, 2번째 원소와 3번째 원소를, 3번째 원소와 4번째 원소를, … 이런 식으로 (N - 1)번째 원소와 N번째 원소를 비교하여 조건에 맞지 않는다면 서로 교환합니다.
2. 1회전을 수행하고 나면 가장 큰 원소가 맨 뒤로 이동하므로 2회전에서는 N번째 원소는 정렬에서 제외되고, 2회전을 수행하고 나면 끝에서 (N - 1)번째 원소까지는 정렬에서 제외됩니다. 이렇게 정렬을 1회전 수행할 때마다 정렬에서 제외되는 데이터가 하나씩 늘어납니다.

<br>

## Java 코드

```java
package study;

import java.util.*;

public class Main {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt(); // 정렬을 진행할 배열의 크기를 받음
		int temp = 0; // 교환이 수행될 때 쓰이는 변수
		int[] arr = new int[n];

		for (int i = 0; i < n; i++) {
			arr[i] = sc.nextInt();
		}

		for (int j = 0; j < (n - 1); j++) {
//		outer 루프는 inner 루프의 범위를 점점 줄이기 위함
//		inner 루프에서 두 개씩 잡아서 비교하기 때문에 (n - 1)번 비교만 해도 n번째 원소까지 비교할 수 있음
			for (int k = 0; k < (n - 1 - j); k++) {
//				inner 루프에서 (n - 1), (n - 2), ... 1번 비교가 수행됨
//				시간 복잡도는 (n - 1) + (n - 2) + ... + 1 = (n - 1)*n/2로 O(n^2)이 됨
				if (!(arr[k] <= arr[k + 1])) {
//				비교해서 왼쪽에 있는 수보다 오른쪽에 있는 수가 크지 않을 때 교환이 수행됨 (오름차순)
//				부등호 방향을 반대로 한다면 내림차순으로 정렬됨
					temp = arr[k];
					arr[k] = arr[k + 1];
					arr[k + 1] = temp;
				}
//				for (int a : arr) {
//					System.out.printf("%d ", a);
//				}
//				System.out.println("");
			}
			for (int a : arr) {
				System.out.printf("%d ", a);
			}
			System.out.println("");
//			예제
//			10
//			9 1 4 6 11 10 3 15 2 13
		}
	}
}
```

```java
예제 1
10
9 1 4 6 11 10 3 15 2 13 (입력)
1 4 6 9 10 3 11 2 13 15 (1회전) - 9번 비교
1 4 6 9 3 10 2 11 13 15 (2회전) - 8번 비교
1 4 6 3 9 2 10 11 13 15 (3회전) - 7번 비교
1 4 3 6 2 9 10 11 13 15 (4회전) - 6번 비교
1 3 4 2 6 9 10 11 13 15 (5회전) - 5번 비교
1 3 2 4 6 9 10 11 13 15 (6회전) - 4번 비교
1 2 3 4 6 9 10 11 13 15 (7회전) - 3번 비교
1 2 3 4 6 9 10 11 13 15 (8회전) - 2번 비교
1 2 3 4 6 9 10 11 13 15 (9회전) - 1번 비교

예제 2
10
1 2 3 4 5 6 7 8 9 10 (입력)
1 2 3 4 5 6 7 8 9 10 (1회전) - 9번 비교
1 2 3 4 5 6 7 8 9 10 (2회전) - 8번 비교
1 2 3 4 5 6 7 8 9 10 (3회전) - 7번 비교
1 2 3 4 5 6 7 8 9 10 (4회전) - 6번 비교
1 2 3 4 5 6 7 8 9 10 (5회전) - 5번 비교
1 2 3 4 5 6 7 8 9 10 (6회전) - 4번 비교
1 2 3 4 5 6 7 8 9 10 (7회전) - 3번 비교
1 2 3 4 5 6 7 8 9 10 (8회전) - 2번 비교
1 2 3 4 5 6 7 8 9 10 (9회전) - 1번 비교
```

예제 2와 같은 최선의 상황에서도 (10 - 1)회전까지 수행됩니다.

<br>

## GIF로 이해하는 Bubble Sort

<img src="./resources/bubble-sort-001.gif">
<br>
<img src="./resources/bubble-sort-wiki.gif">

<br>

## 시간복잡도

시간복잡도를 계산하면, `(n - 1) + (n - 2) + (n - 3) + .... + 2 + 1 => n(n-1)/2`이므로, **O(n^2)** 입니다. 또한, Bubble Sort는 정렬이 되어 있든 말든 2개의 원소를 비교하기 때문에 최선, 평균, 최악의 경우 모두 시간복잡도가 **O(n^2)** 으로 동일합니다.

<br>

## 공간복잡도

주어진 n 크기의 배열 안에서 교환을 통해, 정렬이 수행되므로 **O(n)** 입니다.

<br>

## 장점

- 구현이 매우 간단하고, 소스코드가 직관적입니다.
- 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는 제자리 정렬(in-place sorting)입니다.
- 중복된 값을 입력 순서와 동일하게 정렬하는 안정 정렬(Stable Sort) 입니다.

<br>

## 단점

- 시간복잡도가 최악, 최선, 평균 모두 O(n^2)으로, 굉장히 비효율적입니다.

<br>

## 결론

Bubble Sort는 정렬 알고리즘 중에 가장 직관적인 교육용으로 많이 사용되는 정렬입니다.

Bubble Sort에 대해 알아보았습니다.

<br>

## 부록: 개선된 Bubble Sort

```java
package study;

import java.util.*;

public class Main {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt(); // 정렬을 진행할 배열의 크기를 받음
		int temp = 0; // 교환이 수행될 때 쓰이는 변수
		int[] arr = new int[n];
		int ex;

		for (int i = 0; i < n; i++) {
			arr[i] = sc.nextInt();
		}

		for (int j = 0; j < (n - 1); j++) {
			ex = 0;
//			교환이 되었는지 판단하기 위한 변수
			for (int k = 0; k < (n - 1 - j); k++) {
				if (!(arr[k] <= arr[k + 1])) {
					temp = arr[k];
					arr[k] = arr[k + 1];
					arr[k + 1] = temp;
					ex++;
				}
//				for (int a : arr) {
//					System.out.printf("%d ", a);
//				}
//				System.out.println("");
			}
			for (int a : arr) {
				System.out.printf("%d ", a);
			}
			System.out.println("");
//			예제 1
//			10
//			9 1 4 6 11 10 3 15 2 13
//			예제 2
//			1
//			1 2 3 4 5 6 7 8 9 10
			if (ex == 0) {
				break;
			}
		}
	}
}
```

```java
예제 1
10
9 1 4 6 11 10 3 15 2 13
1 4 6 9 10 3 11 2 13 15 (1회전) - 9번 비교
1 4 6 9 3 10 2 11 13 15 (2회전) - 8번 비교
1 4 6 3 9 2 10 11 13 15 (3회전) - 7번 비교
1 4 3 6 2 9 10 11 13 15 (4회전) - 6번 비교
1 3 4 2 6 9 10 11 13 15 (5회전) - 5번 비교
1 3 2 4 6 9 10 11 13 15 (6회전) - 4번 비교
1 2 3 4 6 9 10 11 13 15 (7회전) - 3번 비교
1 2 3 4 6 9 10 11 13 15 (8회전) - 2번 비교

예제 2
10
1 2 3 4 5 6 7 8 9 10
1 2 3 4 5 6 7 8 9 10 (1회전) - 9번 비교
```

외에도 양방향 Bubble Sort 등 다양한 개선 방법이 있습니다.

<br>

## 참조

- https://zeddios.tistory.com/20
- https://jinhyy.tistory.com/9
- https://gmlwjd9405.github.io/2018/05/06/algorithm-bubble-sort.html
- https://velog.io/@msriver/알고리즘-버블정렬-개선하기
