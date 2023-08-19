# Linked List (연결 리스트)

### *각 노드가 데이터와 포인터를 가지고 한 줄로 연결되어 있는 방식으로 데이터를 저장하는 자료구조*

<br>

## 목차
1. [Linked List란?](#linked-list란)
2. [왜 Linked List를 사용하나?](#왜-linked-list를-사용하나) 
3. [장점](#장점)
4. [단점](#단점)
5. [JAVA로 연결리스트 구현해보기](#java로-연결리스트-구현해보기)

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

##  JAVA로 연결리스트 구현해보기

### 노드 구현은 아래와 같이 데이터와 다음 노드에 대한 참조로 나타낼 수 있다

```java
// List를 구성하는 Node 클래스
public class Node {
    Node next;
    String data;
    public Node(String data) {
        this.data = data;
    }
	public String getData() {
		return data;
	}
	@Override
	public String toString() {
		return "Node [next=" + next + ", data=" + data + "]";
	}
}
```

### 기능 구현

```java
	public class LinkedList {
    
	Node head;
  	Node tail;
    int size = 0;
    
    public void addFirst(String data){
    	Node newNode = new Node(data); //노드 생성
        
        newNode.next = head; //새로운 노드의 다음 노드로 헤드를 지정
        
        head = newNode; //head를 새로운 노드로 지정 
        size++; 
        
        if(head.next == null)
        	tail = head;
    }
    
    public void addLast(String data) { // Node 마지막에 삽입
        Node newNode = new Node(data); //노드 생성
    
    	if(size == 0) //리스트의 노드가 없는 경우, 첫번째 노드로 추가하는 메소드 사용 
    		addFirst(data); 
    	else {
    		tail.next = newNode; //마지막 노드의 다음 노드로 생성한 노드를 지정
        	tail = newNode; //마지막 노드를 갱신 
        	size++; 
    	}
    }
    
    
    public Object removeFirst() {
    	Node temp = head; //첫번째 노드를 head로 지정
        head = temp.next; //head의 값을 두번째 노드로 변경
        
        Object returnData = temp.data; //데이터 삭제 전 리턴할 값을 임시 변수에 담아둔다.
        temp = null;
        size--;
        return returnData;
    }
    
    public Object indexremove(int k) {
    	if(k == 0)
        	return removeFirst();
        
        Node temp = node(k-1); //k-1번째 node를 temp의 값으로 지정 
        
        Node todoDeleted = temp.next; 
        //삭제할 노드를 todoDeleted에 기록
        // 삭제 노드를 지금 제거하면 삭제 앞 노드와 삭제 뒤 노드를 연결할 수 없다. 
        
        temp.next = temp.next.next; 
        //삭제 앞 노드의 다음 노드로 삭제 뒤 노드를 지정한다. 
        
        Object returnData = todoDeleted.data; 
        //삭제된 데이터를 리턴하기 위해서 returnData에 저장한다. 
        
        if(todoDeleted == tail)
        	tail = temp;
       	
        todoDeleted = null;
        size--;
        return returnData;
    }
    
    public void removeValue(String data) {
        if(head == null) {
            return;
        }
        if(head.data.equals(data)) {
            head = head.next;
            return;
        }
        Node current = head;
        while(current.next != null) {
            if(current.next.data.equals(data)) {
                current.next = current.next.next;
                return;
            }
            current = current.next;
        }
    }
    
    public int indexOf(Object data){
    	Node temp = head; //탐색 대상이 되는 노드를 temp로 지정한다. 
        int index = 0; //탐색 대상의 엘리먼트 
        
        while(temp.data != data) { //탐색 값과 탐색 대상의 값을 비교
        	temp = temp.next;
            index++;
            
            if(temp == null) //더 이상 탐색할 대상이 없다는 것
            	return -1;
        }
        
        return index;
    }
    
    Node node(int index) {
    	Node x = head;
        for(int i = 0; i < index; i++)        
        	x = x.next;
        return x;
     }
    
    public int size() {
    	return size;
    }
    
    public void printList() {
        Node tempNode = this.head;    // tempNode에 head가 가리키는 첫번째 노드를 할당
        
        // tempNode가 null이 아닐 때까지 반복하여 출력
        while(tempNode != null) {
            System.out.print(tempNode.getData() + " ");
            tempNode = tempNode.next;    // temp 노드에 다음 노드(tempNode.next) 할당.
        }
        System.out.println();
    }
}


```

<br>

##### [참고 자료]

- [https://gyoogle.dev/blog/computer-science/data-structure/Linked%20List.html](https://gyoogle.dev/blog/computer-science/data-structure/Linked%20List.html)
- [https://monsieursongsong.tistory.com/8](https://monsieursongsong.tistory.com/8)
- [https://velog.io/@frombozztoang/Java-Linked-List-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0](https://velog.io/@frombozztoang/Java-Linked-List-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0)