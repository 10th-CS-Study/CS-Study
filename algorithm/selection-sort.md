# ._.) 선택 정렬 (Selection Sort)을 마스터해봅시당

*Assembled by GimunLee (2019-10-29)*

### ***"`최솟값`을 찾아서 맨 앞 요소와 교환하기"*** 를 반복하는 간단하고 직관적인 알고리즘

<br>

## 목차
1. [선택 정렬 (Selection Sort)이란?]() 
2. [자바로 구현해보기]()
3. [시간 복잡도와 공간 복잡도]()
4. [선택 정렬의 장단점]()

<br>

## 🖥 선택 정렬 (Selection Sort)이란?

Selection Sort는 Bubble Sort과 유사한 알고리즘으로, **해당 순서에 원소를 넣을 위치(원소를 어디에 넣을지)는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘**입니다.

Selection Sort와 Insertion Sort를 헷갈려하시는 분들이 종종 있는데, Selection Sort는 배열에서 **해당 자리를 선택하고 그 자리에 오는 값을 찾는 것**이라고 생각하시면 편합니다.

<br>

### 📌 선택 정렬 과정

1. 주어진 배열 중에 `최소값`을 찾습니다.
2. 그 값을 맨 앞의 값과 `교체(Swap)`합니다. (pass)
3. 교체한 값을 제외한 나머지 배열로 1~2번을 반복 수행합니다.

<br>

## 🖥 자바로 구현해보기
```
입력 : [64, 25, 12, 22, 11]
출력 : [11, 12, 22, 25, 64]
```

```java
import java.util.Arrays;

public class SelectionSort {

	static void selectionSort(int[] arr) {
	    int minIdx, temp; // 최솟값 담을 minIdx, 요소 교체를 위한 temp 변수
	    for (int i = 0; i < arr.length-1; i++) {        // 1.
	        minIdx = i;
	        for (int j = i + 1; j < arr.length; j++) {  // 2.
	            if (arr[j] < arr[minIdx]) {           // 3.
	                minIdx = j;
	            }
	        }
	        // 4. swap(arr[minIdx], arr[i])
	        temp = arr[minIdx];
	        arr[minIdx] = arr[i];
	        arr[i] = temp;
	  }
	  System.out.println(Arrays.toString(arr));
	}
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		selectionSort(new int[] {64, 25, 12, 22, 11}); 
	}

}
```

1. 우선, 위치(index)를 **선택**해줍니다.
2. i+1번째 원소부터 선택한 위치(index)의 값과 비교를 시작합니다.
3. 오름차순이므로 현재 선택한 자리에 있는 값보다 순회하고 있는 값이 작다면, 위치(index)를 갱신해줍니다.
4. '2'번 반복문이 끝난 뒤에는 indexMin에 '1'번에서 선택한 위치(index)에 들어가야하는 값의 위치(index)를 갖고 있으므로 서로 교환(swap)해줍니다.

<br>

### 📌 GIF로 이해하는 Selection Sort

<img src="./resources/selection-sort-001.gif">

<br><br>

## 🖥 시간 복잡도와 공간 복잡도
### 📍 시간 복잡도

```
시간 복잡도: O(n^2)

best: O(n^2)
average: O(n^2)
worst: O(n^2)
```

데이터의 개수가 n개라고 했을 때, 

- 첫 번째 회전에서의 비교횟수 : 1 ~ (n-1) => n-1

- 두 번째 회전에서의 비교횟수 : 2 ~ (n-1) => n-2

  ...

- ```(n-1) + (n-2) + .... + 2 + 1 => n(n-1)/2```

비교하는 것이 상수 시간에 이루어진다는 가정 아래, n개의 주어진 배열을 정렬하는데 O(n^2) 만큼의 시간이 걸립니다. 최선, 평균, 최악의 경우 시간복잡도는 **O(n^2)** 으로 동일합니다.

<br/>

### 📍 공간복잡도

주어진 배열 안에서 교환(swap)을 통해, 정렬이 수행되므로 **O(n)** 입니다.

<br><br>

## 🖥 선택 정렬의 장단점
### 🎯 장점

- Bubble sort와 마찬가지로 알고리즘이 단순합니다.
- 정렬을 위한 비교 횟수는 많지만, Bubble Sort에 비해 실제로 교환하는 횟수는 적기 때문에 많은 교환이 일어나야 하는 자료상태에서 비교적 효율적입니다.
- Bubble Sort와 마찬가지로 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않습니다. => 제자리 정렬(in-place sorting)

<br>

### 🎯 단점

- 시간복잡도가 O(n^2)으로, 비효율적입니다.
- **불안정 정렬(Unstable Sort)** 입니다.

<br>

### 🤷🏻‍♀️ 불안정 정렬(Unstable Sort)이 뭐죠?

#### 불안정 정렬 (Unstable Sort)
불안정 정렬(Unstable Sort)은 정렬 알고리즘의 한 종류로, 동일한 키(key) 값을 가지는 원소들의 상대적인 순서가 정렬 전과 정렬 후에도 유지되지 않을 수 있는 정렬 방식을 말합니다. 즉, ***정렬되기 전과 후의 같은 값들의 순서가 보장되지 않을 수 있습니다.***

예를 들어, 주어진 배열이 [5, 2, 3, 5, 1]이라고 가정해봅시다. 이 배열을 불안정 정렬로 정렬하면 결과가 [1, 2, 3, 5, 5]가 될 수 있습니다. 이때, 원래 배열에서 같은 값인 5가 두 개 있었습니다. 그러나 정렬 후에는 두 5의 순서가 변경되었습니다. 이처럼 불안정 정렬은 같은 값들의 순서가 변할 수 있습니다.

#### 안정 정렬 (Stable Sort)
반면에 안정 정렬(Stable Sort)은 동일한 키 값을 가지는 원소들의 상대적인 순서가 정렬 전과 정렬 후에도 유지되는 정렬 방식입니다. 위의 예시에서, 안정 정렬로 정렬을 수행하면 원래 배열에서 순서가 먼저인 5와 순서가 나중인 5의 상대적인 순서가 정렬 후에도 유지됩니다.

### 불안정 정렬 vs 안정 정렬 : 어떤 것이 더 좋을까
불안정 정렬과 안정 정렬 중 어떤 것을 선택할지는 사용하는 상황과 데이터의 특성에 따라 다르게 결정됩니다. 불안정 정렬은 안정 정렬보다 일반적으로 조금 더 빠르고 메모리를 덜 사용하는 경향이 있습니다.

따라서 원소들의 순서가 중요하지 않거나 같은 값들의 상대적인 순서가 중요하지 않은 경우에는 불안정 정렬을 사용하는 것이 효율적일 수 있습니다. 하지만 같은 값들의 상대적인 순서가 중요하거나 원래 데이터의 순서를 유지해야 하는 경우에는 안정 정렬을 선택해야 합니다.

<br>

## 🖥 결론

Bubble Sort와 유사하지만, 조금 더 빠른 Selection Sort에 대해 알아보았습니다. 기술 면접이나 시험(n번째 회전에 정렬 상태)에서도 종종 나오는 정렬이니 알아두시면 좋을 것 같습니다.

<br>

## Reference & Additional Resources

- https://jinhyy.tistory.com/9 
- [https://medium.com/@joongwon/%EC%A0%95%EB%A0%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B8%B0%EC%B4%88-805391cb088e](https://medium.com/@joongwon/정렬-알고리즘-기초-805391cb088e) 
- https://gmlwjd9405.github.io/2018/05/06/algorithm-selection-sort.html 
- [https://ko.wikipedia.org/wiki/%EC%84%A0%ED%83%9D_%EC%A0%95%EB%A0%AC](https://ko.wikipedia.org/wiki/선택_정렬) 
