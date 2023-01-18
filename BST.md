# BST

#### 트리란 무엇인가?

* 트리란 각각의 노드가 서로 부모 - 자식 관계를 가지는 형태의 자료구조를 의미한다.

* 연결 리스트와 다르게, 트리에는 "PATH"가 여러가지 있을 수 있다.

* 단일 연결 리스트는 트리의 일종으로 볼 수 있다. (한쪽으로만 치우친)

* 트리 관련 용어 정리

  | 용어    | 뜻                     |
  | ------- | ---------------------- |
  | Root    | 최상위의 노드          |
  | Child   | 자식 노드              |
  | Parent  | 부모 노드              |
  | Sibling | 형제 노드, 부모를 공유 |
  | Leaf    | 자식 노드가 없는 노드  |
  | Edge    | 노드 간의 관계         |



#### 트리는 어디서 사용되나?

* HTML, DOM
* Networking Routing: 음..그렇다고 한다
* Abstract Syntax Tree(추상 구문 트리): 소스코드를 문법에 맞게 노드들로 쪼개서 만든 트리!
* AI
* 디렉토리, 파일
* JSON



#### 이진 트리는 뭐지?

각각의 노드가 최대 2개의 자식 노드를 가질 수 있다.



#### 이진 탐색 트리(Binary Search Tree, BST)는 뭐지?

* 이진 트리에 Sorting을 가미한 것
* 왼쪽 자식 노드는 부모노드보다 작음
* 오른쪽 자식 노드는 부모노드보다 큼

![이진탐색트리(Binary Search Tree) · ratsgo's blog](https://i.imgur.com/po0R4GB.png)



#### 구현

```javascript
class Node {
    constructor (value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }
}

class BinarySearchTree {
    constructor() {
        this.root = null;
    }

    insert(value) {
        const newNode = new Node(value);
        if (!this.root) {
            this.root = newNode
            return this;
        };

        let current = this.root;

        while(true) {
            if (newNode.value === current.value) return undefined;
            
            if (newNode.value > current.value) {
                if (current.right) {
                    current = current.right;
                    continue;
                }
                current.right = newNode;
                break;
            }
            if (newNode.value < current.value) {
                if (current.left) {
                    current = current.left;
                    continue;
                }
                current.left = newNode;
                break;
            }
        }

        return this;
    }

    find(value) {
        if (!this.root) return false;
        let current = this.root;
        let found = false;
        while (current && !found) {
            if (value < current.value) {
                current = current.left;
            } else if (value > current.value) {
                current = current.right;
            } else {
                found = true;
            }
        }
        if (!found) return undefined;
        return current;
    }
}
```



#### 빅오

Logarithm이 기억난다면 쉽게 이해할 수 있다..!

* Insertion: O(logN)
* Searching: O(logN)

<strong>한쪽 노드만 있는 형태라면, 유효한 BST이지만 O(N)</strong>

=> 즉, 온전히 두 개의 자식 노드가 있는 형태를 가정했을 때만 O(logN) 효율이 나온다.

