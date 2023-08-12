# Tree

<br>

```
Node와 Edge로 이루어진 자료구조
Tree의 특성을 이해하자
```

<br>

<img src="https://www.geeksforgeeks.org/wp-content/uploads/binary-tree-to-DLL.png">

<br>

트리는 값을 가진 `노드(Node)`와 이 노드들을 연결해주는 `간선(Edge)`으로 이루어져있다.

그림 상 데이터 1을 가진 노드가 `루트(Root) 노드`다.

모든 노드들은 0개 이상의 자식(Child) 노드를 갖고 있으며 보통 부모-자식 관계로 부른다.
![image](https://github.com/10th-CS-Study/CS-Study/assets/50294908/c335e767-2496-4134-a0c4-5d4254d8bef9)
![image](https://github.com/10th-CS-Study/CS-Study/assets/50294908/01e7d5b9-15d2-4eb3-af45-c5ae05181bac)

<br>

아래처럼 가족 관계도를 그릴 때 트리 형식으로 나타내는 경우도 많이 봤을 것이다. 자료구조의 트리도 이 방식을 그대로 구현한 것이다.

<img src="https://post-phinf.pstatic.net/MjAxOTA4MjZfMTg1/MDAxNTY2Nzc0Mzk2OTMw.k2EDmhB2y4O1MVrL-XqOXibXkSOBtGX8r86emCgUk9Eg.8C_5nfeIvIDSiLO8FL-i4e28h-8DmbQRS4r2CqSJ6TUg.JPEG/2216_nephew.jpg?type=w1200" width="500">

<br>

트리는 몇 가지 특징이 있다.

- 트리에는 사이클이 존재할 수 없다. (만약 사이클이 만들어진다면, 그것은 트리가 아니고 그래프다)
- 모든 노드는 자료형으로 표현이 가능하다.
- 루트에서 한 노드로 가는 경로는 유일한 경로 뿐이다.
- 노드의 개수가 N개면, 간선은 N-1개를 가진다.

<br>

가장 중요한 것은, `그래프`와 `트리`의 차이가 무엇인가인데, 이는 사이클의 유무로 설명할 수 있다.

사이클이 존재하지 않는 `그래프`라 하여 무조건 `트리`인 것은 아니다 사이클이 존재하지 않는 그래프는 `Forest`라 지칭하며 트리의 경우 싸이클이 존재하지 않고 모든 노드가 간선으로 이어져 있어야 한다
![image](https://github.com/10th-CS-Study/CS-Study/assets/50294908/87375cbd-8340-49f9-afa1-bb3ad267bed7)

<br>

### 트리 순회 방식

트리를 순회하는 방식은 총 4가지가 있다. 위의 그림을 예시로 진행해보자

<br>

<img src="https://www.geeksforgeeks.org/wp-content/uploads/binary-tree-to-DLL.png">

<br>

1. #### 전위 순회(pre-order)

   각 루트(Root)를 순차적으로 먼저 방문하는 방식이다.

   (Root → 왼쪽 자식 → 오른쪽 자식)

   > 1 → 2 → 4 → 8 → 9 → 5 → 10 → 11 → 3 → 6 → 13 → 7 → 14

   <br>

2. #### 중위 순회(in-order)

   왼쪽 하위 트리를 방문 후 루트(Root)를 방문하는 방식이다.

   (왼쪽 자식 → Root → 오른쪽 자식)

   > 8 → 4 → 9 → 2 → 10 → 5 → 11 → 1 → 6 → 13 → 3 →14 → 7

   <br>

3. #### 후위 순회(post-order)

   왼쪽 하위 트리부터 하위를 모두 방문 후 루트(Root)를 방문하는 방식이다.

   (왼쪽 자식 → 오른쪽 자식 → Root)

   > 8 → 9 → 4 → 10 → 11 → 5 → 2 → 13 → 6 → 14 → 7 → 3 → 1

   <br>

4. #### 레벨 순회(level-order)

   루트(Root)부터 계층 별로 방문하는 방식이다.

   (루트 노드부터, 마지막 노드까지 순회하되, 왼쪽부터 오른쪽순으로 순회함. --> bfs기반의 탐색(순회)방법)

   > 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9 → 10 → 11 → 13 → 14
 
<br>

<br>

### Code

```java
public class Tree<T> {
    private Node<T> root;

    public Tree(T rootData) {
        root = new Node<T>();
        root.data = rootData;
        root.children = new ArrayList<Node<T>>();
    }

    public static class Node<T> {
        private T data;
        private Node<T> parent;
        private List<Node<T>> children;
    }
}
```

<br>

<br>

#### [참고 자료]

- [링크](https://www.geeksforgeeks.org/binary-tree-data-structure/)



## 트라이(Trie)

> 문자열에서 검색을 빠르게 도와주는 자료구조

```
정수형에서 이진탐색트리를 이용하면 시간복잡도 O(logN)
하지만 문자열에서 적용했을 때, 문자열 최대 길이가 M이면 O(M*logN)이 된다.

트라이를 활용하면? → O(M)으로 문자열 검색이 가능함!
```

<br>

<img src="https://t1.daumcdn.net/cfile/tistory/24354E335833A7CF17">

> 예시 그림에서 주어지는 배열의 총 문자열 개수는 8개인데, 트라이를 활용한 트리에서도 마지막 끝나는 노드마다 '네모' 모양으로 구성된 것을 확인하면 총 8개다.

<br>

해당 자료구조를 풀어보기 위해 좋은 문제 : [백준 5052(전화번호 목록)](<https://www.acmicpc.net/problem/5052>)

##### 문제에서 Trie를 java로 구현한 코드

```java
static class Trie {
    boolean end;
    boolean pass;
    Trie[] child;

    Trie() {
        end = false;
        pass = false;
        child = new Trie[10];
    }

    public boolean insert(String str, int idx) {

        //끝나는 단어 있으면 false 종료
        if(end) return false;

        //idx가 str만큼 왔을때
        if(idx == str.length()) {
            end = true;
            if(pass) return false; // 더 지나가는 단어 있으면 false 종료
            else return true;
        }
        //아직 안왔을 때
        else {
            int next = str.charAt(idx) - '0';
            if(child[next] == null) {
                child[next] = new Trie();
                pass = true;
            }
            return child[next].insert(str, idx+1);
        }

    }
}
```
