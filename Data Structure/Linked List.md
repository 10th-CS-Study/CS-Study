# Linked List (연결 리스트)

### *각 노드가 데이터와 포인터를 가지고 한 줄로 연결되어 있는 방식으로 데이터를 저장하는 자료구조*

<br>

## 목차
1. [Linked List란?](#linked-list란)
2. [왜 Linked List를 사용하나?](#왜-linked-list를-사용하나) 
3. [장점](#장점)
4. [단점](#단점)
5. [스택으로 구현한 연결리스트 (java)](#스택으로-구현한-연결리스트-java)

<br>

## Linked List란?

![img](https://www.geeksforgeeks.org/wp-content/uploads/gq/2013/03/Linkedlist.png)

연속적인 메모리 위치에 저장되지 않는 선형 데이터 구조

(포인터를 사용해서 연결된다)

각 노드는 `데이터 필드`와 `다음 노드에 대한 참조를 포함하는 노드`로 구성

<br>

## 왜 Linked List를 사용하나?

> 배열은 비슷한 유형의 선형 데이터를 저장하는데 사용할 수 있지만 제한 사항이 있음
>
> 1) 배열의 크기가 고정되어 있어 미리 요소의 수에 대해 할당을 받아야 함
>
> 2) 새로운 요소를 삽입하는 것은 비용이 많이 듬 (공간을 만들고, 기존 요소 전부 이동)

<br>

## 장점

> 1) 동적으로 메모리 사용 가능
>
> 2) 삽입/삭제 용이
>
> 3) 대용량 데이터 처리 적합

<br>

## 단점

> 1) 특정 위치 데이터 검색할 때 느림
>
> 2) 메모리를 추가적으로 사용해야 함


<br>

## 스택으로 구현한 연결리스트 (java)

### 노드 구현은 아래와 같이 데이터와 다음 노드에 대한 참조로 나타낼 수 있다

```java
public class Node<T> {
	private T data; // 해당 노드의 데이터를 저장
	private Node<T> link; // 해당 노드와 연결된 노드를 저장
	
	public Node(T data, Node<T> link) {
		super();
		this.data = data;
		this.link = link;
	}

	public Node(T data) {
		super();
		this.data = data;
	}

	public T getData() {
		return data;
	}

	public void setData(T data) {
		this.data = data;
	}


	public Node<T> getLink() {
		return link;
	}

	public void setLink(Node<T> link) {
		this.link = link;
	}

    @Override
	public String toString() {
		return "Node [data=" + data + ", link=" + link + "]";
	}
}
```


### 인터페이스 구현

```java
public interface IStack<E> {
	void push(E e);
	E pop();
	E Peek();
	int size();
	boolean isEmpty();
}
```

### 기능 구현

```java
import java.util.EmptyStackException;

public class LinkedListStack<E> implements IStack<E> {

	private Node<E> top = null;

	@Override
	public void push(E e) {
		top = new Node<>(e, top);
        // 기존 top을 다음 노드로 참조하고
        // 입력 받은 값을 data로 하는 새 노드 생성
        // 새로운 노드를 top으로
	}

	@Override
	public E pop() {
		if(isEmpty()) { // 비어있으면 Exception
			throw new EmptyStackException();
		}
        // 비어있지 않으면 
        // top위치와 연결되 있던 노드를 top으로
		Node<E> popNode = top;
		top = popNode.getLink();

		popNode.setLink(null);
		
		return popNode.getData();
	}

	@Override
	public E Peek() {
		if(isEmpty()) {
			throw new EmptyStackException();
		}
		return top.getData(); // top의 data 리턴
	}

	@Override
	public int size() {
		int size = 0;
         // 연결된 노드가 null이아니면
		for (Node<E> temp = top; temp != null; temp = temp.getLink()) { 
			++size; //사이즈 증가
		}
		return size;
	}

    
	@Override
	public boolean isEmpty() {
		return top==null;
	}
}
```

<br>

##### [참고 자료]

- [https://gyoogle.dev/blog/computer-science/data-structure/Linked%20List.html](https://gyoogle.dev/blog/computer-science/data-structure/Linked%20List.html)
- [https://monsieursongsong.tistory.com/8](https://monsieursongsong.tistory.com/8)