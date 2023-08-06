# ._.) 이진 탐색 (Binary Search)을 마스터해봅시당

### *데이터가 정렬돼 있는 배열에서 특정한 값을 찾아내는 알고리즘*

<br>

## 목차
1. [이진 탐색(Binary Search)이란?](#이진-탐색-binary-search이란) 
2. [진행 순서](#진행-순서)
3. [이진 탐색 예시](#이진-탐색-예시)
4. [Code](#code)

<br>

## 이진 탐색 (Binary Search)이란?

> 탐색 범위를 두 부분으로 분할하면서 찾는 방식

처음부터 끝까지 돌면서 탐색하는 것보다 훨~~~씬 빠른 장점을 지님

```
* 시간복잡도
전체 탐색 : O(N)
이진 탐색 : O(logN)
```

<br>

## 진행 순서

- 우선 정렬을 해야 함
- `left`와 `right`로 `mid` 값 설정
- `mid`와 내가 구하고자 하는 값과 비교
- 구할 값이 `mid`보다 높으면 : left = mid+1
  구할 값이 `mid`보다 낮으면 : right = mid - 1
- `left` > `right`가 될 때까지 계속 반복하기

<br>

## 이진 탐색 예시
오름차순으로 정렬된 배열이 있다.

```
{ 17, 28, 43, 67, 88, 92, 100 }
```

이 배열에서 이진 탐색을 이용하여 `43`의 값을 찾아보자.

<br/>

#### 첫 번째 시도
우선 가운데에 위치한 임의의 값 `67`을 선택한다.

선택한 값 67과 찾고자 하는 값 `43`를 비교한다.

`43` < `67` 이므로 43은 67의 `좌측`에 존재한다는 것을 알 수 있다.

<br/>

#### 두 번째 시도
67을 기준으로 좌측에 있는 배열 값들을 대상으로 다시 탐색을 진행한다.

```
{ 17, 28, 43 }
```

마찬가지로 가운데의 임의의 값 `28`을 선택한다.

`28` < `43` 이번에는 28이 43보다 작으므로 28 `우측`에 위치하는 것을 알 수 있다.

<br/>

#### 세 번째 시도
28의 우측을 기준으로 배열을 다시 설정해보면

```
{ 43 }
```

배열에 값이 하나만 남게 되고 값을 확인해보면,
`43` == `43` 원하는 값을 찾았다.

<br/>

## Code

#### 📌 반복문을 이용한 방법

```java
import java.util.Arrays;
import java.util.NoSuchElementException;

public class BinarySearch {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int arr[] = { 17, 28, 43, 67, 88, 92, 100 };
		
	    System.out.println(Arrays.toString(arr));
	    int target = 43;
	    System.out.println("찾을 값: " + target);
	    
		int targetIndex = binarySearch(arr, target);
		
		System.out.println("target 인덱스: " + targetIndex);
		System.out.println("target 값: " + arr[targetIndex]);
	}

	public static int binarySearch(int[] arr, int M) {
		
	    int	left = 0;
	    int right = arr.length - 1;
	    int mid = 0;

	    while (left <= right) {
	        mid = (left + right) / 2;
	        if (M == arr[mid]) {
	            return mid;
	        }else if (arr[mid] < M) {
	            left = mid + 1;
	        }else if (M < arr[mid]) {
	            right = mid - 1;
	        }
	    }
	    throw new NoSuchElementException("타겟 존재하지 않음");
	}
}

```

<br/>

#### 📌 재귀를 이용한 방법
```java
import java.util.Arrays;
import java.util.NoSuchElementException;

public class BinarySearch {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int arr[] = { 17, 28, 43, 67, 88, 92, 100 };
		
	    System.out.println(Arrays.toString(arr));
	    int target = 43;
	    System.out.println("찾을 값: " + target);
	    
	    int targetIndex = binarySearchRecur(arr, target, 0, arr.length-1);
		
		System.out.println("target 인덱스: " + targetIndex);
		System.out.println("target 값: " + arr[targetIndex]);
	}
	
	public static int binarySearchRecur(int arr[], int target, int left, int right) {
		
	    if (left > right)
	        return -1;

	    int mid = (left + right) / 2;
	    
	    if (arr[mid] == target)
	        return mid;
	    else if (arr[mid] > target)
	        return binarySearchRecur(arr, target, left, mid-1);
	    else
	        return binarySearchRecur(arr, target, mid+1, right);
	}
}
```

<br/>

## Reference & Additional Resources

- [https://gyoogle.dev/blog/algorithm/Binary%20Search.html](https://gyoogle.dev/blog/algorithm/Binary%20Search.html)
- [https://www.programiz.com/dsa/binary-search](https://www.programiz.com/dsa/binary-search)
- [https://cjh5414.github.io/binary-search/](https://cjh5414.github.io/binary-search/)