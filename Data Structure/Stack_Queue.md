## 스택(Stack)

입력과 출력이 한 곳(방향)으로 제한

##### LIFO (Last In First Out, 후입선출) : 가장 나중에 들어온 것이 가장 먼저 나옴

<br>

**_언제 사용?_**

함수의 콜스택, 문자열 역순 출력, 연산자 후위표기법

<br>

##### 주요 기능

데이터 최상위에 넣음 : push()

데이터 최상위 값 뺌 : pop()

비어있는지 확인 : isEmpty()

<br>

##### Node

```java
public class Node<T> {
	private T data;
	private Node<T> link;
	@Override
	public String toString() {
		return "Node [data=" + data + ", link=" + link + "]";
	}
	public Node(T data, Node<T> link) {
		super();
		this.data = data;
		this.link = link;
	}
	public Node(T data) {
		super();
		this.data = data;
	}
	public Node() {
		super();
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
}
```

##### Stack 인터페이스

```java
public interface MyStack<T> {
	void push(T e);
	T pop();
	T peek();
	int size();
	boolean isEmpty();
}

```

##### Stack 구현

```java
package study12;

import java.util.*;

public class LinkedListStack<T> implements MyStack<T> {
	private Node<T> top = null;

	@Override
	public void push(T e) {
//		인자로 들어온 e 값으로 새로운 노드를 생성하고 link 변수가 top 노드를 가리키게 함
//		첫 노드를 생성했다면 그 노드의 link는 top이 가리켰던 null임
//		마지막에는 이렇게 생성한 노드를 top이 가리키게 함
		top = new Node<>(e, top);
	}

	@Override
	public T pop() {
//		스택이 비어있는 경우에는 예외를 던지도록 설정
		if (isEmpty()) {
			throw new NoSuchElementException();
		}
//		제일 위에 있는 노드를 삭제해야 함
		Node<T> popNode = top;
//		삭제할 노드의 데이터를 반환하기 위한 변수 data 선언
		T data = popNode.getData();
//		top이 삭제할 노드의 link 노드를 가리키게 함
		top = popNode.getLink();
//		popNode와 link 노드의 연결을 끊음
//		사실상 제일 위에 있는 노드가 삭제된 효과
		popNode.setData(null);
		popNode.setLink(null);
//		일반적으로 객체 자체를 반환하는 것이 아니라 객체에 저장된 데이터를 반환함
		return data;
	}

	@Override
	public T peek() {
		if (isEmpty()) {
			throw new NoSuchElementException();
		}
//		top이 가리키고 있던 노드가 peek할 노드임
		return top.getData();
	}

	@Override
	public int size() {
		int size = 0;
//		top을 시작으로 link를 타고 들어가면서 크기를 셈
//		타고 들어간 것이 null이면 마지막이라는 뜻임
		for (Node<T> temp = top; temp != null; temp = temp.getLink()) {
			size++;
		}
		return size;
	}

	@Override
	public boolean isEmpty() {
//		top이 어떤 노드도 가리키고 있지 않다면(null) false 반환
		return top == null;
	}
}

```

##### Stack 테스트

```java
public class LinkedListStackTest {
	public static void main(String[] args) {
		MyStack<Integer> stack = new LinkedListStack<>();
		System.out.println("empty? : " + stack.isEmpty());
		System.out.println("push");
		stack.push(1);
		System.out.println("push");
		stack.push(2);
		System.out.println("push");
		stack.push(3);
		System.out.println("push");
		stack.push(4);
		System.out.println("push");
		stack.push(5);
		System.out.println("peek : " + stack.peek());
		System.out.println("size : " + stack.size());
		System.out.println("pop : " + stack.pop());
		System.out.println("size : " + stack.size());
		System.out.println("peek : " + stack.peek());
		System.out.println("empty? : " + stack.isEmpty());
	}
}

//empty? : true
//push
//push
//push
//push
//push
//peek : 5
//size : 5
//pop : 5
//size : 4
//peek : 4
//empty? : false
```

<br>

<br>

<br>

## 큐(Queue)

입력과 출력을 한 쪽 끝(head, tail)으로 제한

##### FIFO (First In First Out, 선입선출) : 가장 먼저 들어온 것이 가장 먼저 나옴

<br>

**_언제 사용?_**

버퍼, 마구 입력된 것을 처리하지 못하고 있는 상황, BFS

<br>

##### 주요 기능

데이터 맨 뒤에 넣음 : enQueue()

데이터 맨 앞에서 뺌 : deQueue()

비어있는지 확인 : isEmpty()

<br>

##### Queue 인터페이스

```java
public interface MyQueue<T> {
	void offer(T e);
	T poll();
	T peek();
	int size();
	boolean isEmpty();
}
```

##### Queue 구현

```java
package study12;

import java.util.*;

public class LinkedListQueue<T> implements MyQueue<T> {
	private Node<T> head = null;
	private Node<T> tail = null;

	@Override
	public void offer(T e) {
//		추가할 노드 생성
		Node<T> offerNode = new Node<>(e);
//		큐가 비어있었을 경우 head가 추가한 노드를 가리키도록 함
		if (isEmpty()) {
			head = offerNode;
		}
//		큐가 비어있지 않았을 경우 tail의 link로 추가할 노드를 할당함
		else {
			tail.setLink(offerNode);
		}
//		마지막에는 tail이 추가한 노드를 가리키도록 함
		tail = offerNode;
	}

	@Override
	public T poll() {
		if (isEmpty()) {
			throw new NoSuchElementException();
		}
//		큐의 크기가 1이었을 경우 미리 tail에 null을 할당함
//		아래에서 삭제 노드의 data와 link를 null로 할당하긴 하지만 필드가 null인 것과 객체가 null인 건 다르다고 생각했음
		if (size() == 1) {
			tail = null;
		}
//		삭제할 노드 선언
		Node<T> pollNode = head;
//		삭제할 노드의 데이터를 반환하기 위한 변수 data 선언
		T data = pollNode.getData();
//		head는 삭제할 노드의 link 노드를 가리키게 함
		head = pollNode.getLink();
//		노드의 데이터를 삭제하고 연결을 끊음
		pollNode.setData(null);
		pollNode.setLink(null);
		return data;
	}

	@Override
	public T peek() {
		if (isEmpty()) {
			throw new NoSuchElementException();
		}
		return head.getData();
	}

	@Override
	public int size() {
		int size = 0;
		for (Node<T> temp = head; temp != null; temp = temp.getLink()) {
			size++;
		}
		return size;
	}

	@Override
	public boolean isEmpty() {
		return head == null;
	}
}
```

##### Queue 테스트

```java
public class LinkedListQueueTest {
	public static void main(String[] args) {
		MyQueue<Integer> queue = new LinkedListQueue<>();
		System.out.println("empty? : " + queue.isEmpty());
		System.out.println("offer");
		queue.offer(1);
		System.out.println("offer");
		queue.offer(2);
		System.out.println("offer");
		queue.offer(3);
		System.out.println("offer");
		queue.offer(4);
		System.out.println("offer");
		queue.offer(5);
		System.out.println("peek : " + queue.peek());
		System.out.println("size : " + queue.size());
		System.out.println("poll : " + queue.poll());
		System.out.println("size : " + queue.size());
		System.out.println("peek : " + queue.peek());
		System.out.println("empty? : " + queue.isEmpty());
	}
}

//empty? : true
//offer
//offer
//offer
//offer
//offer
//peek : 1
//size : 5
//poll : 1
//size : 4
//peek : 2
//empty? : false
```
