# Data Structure Notes

**Author:** Anowar Hossain
**Subject:** Data Structure

---

## 1. Introduction to Data Structures
Data structures are divided into two main categories:
* **Linear:** Array, Linked List, Stack, Queue.
* **Non-Linear:** Tree, Graph.

---

## 2. Stack
A stack is a list of elements in which an element may be inserted or deleted only at one end, called the **top** of the stack. Stack is known as **LIFO** (Last In First Out).

**Operations:**
* **Push():** Insert an element into the stack.
* **Pop():** Delete the element from the stack. Always deletion will be done from the top.
* **top():** View the element which is at the top of the stack.
* **display():** View all the elements in the stack.

**Conditions:**
* **Overflow:** `top == MAX_STACK - 1`
* **Underflow:** `top == -1`

### C/C++ Implementation of Stack
```cpp
void push(int x) {
    if (top == Max_stack - 1) {
        printf("Overflow");
    } else {
        top++;
        stack[top] = x;
    }
}

void pop() {
    if (top == -1) {
        printf("Underflow");
    } else {
        printf("%d", stack[top]);
        top--;
    }
}

void display() {
    if (top == -1) {
        printf("Stack is empty");
    } else {
        for (int i = 0; i <= top; i++) {
            printf("%d", stack[i]);
        }
        // For reverse way stack result:
        // for(int i = top; i >= 0; i--) { printf("%d", stack[i]); }
    }
}

void top() {
    if (top == -1) {
        printf("Stack is empty");
    } else {
        printf("%d", stack[top]);
    }
}
```

---

## 3. Queue
A queue is another special kind of list where items are inserted at one end called **Rear** and deleted at the other end called **front**. Another name for a queue is **FIFO** (First In First Out).

**Operations:**
* **enqueue():** Insert an element at the end of the queue.
* **dequeue():** Delete the first element of the queue.
* **display():** Display all the elements in the queue.

**Conditions:**
* **Overflow:** `rear == n - 1`
* **Underflow:** `front == -1 && rear == -1`

### C/C++ Implementation of Queue
```cpp
void enqueue(int x) {
    if (rear == n - 1) {
        printf("Overflow");
    } else if (front == -1 && rear == -1) {
        front = rear = 0;
        queue[rear] = x;
    } else {
        rear++;
        queue[rear] = x;
    }
}

void dequeue() {
    if (front == -1 && rear == -1) {
        printf("Underflow");
    } else if (front == rear) {
        printf("%d", queue[front]);
        front = rear = -1;
    } else {
        printf("%d", queue[front]);
        front++;
    }
}

void display() {
    if (front == -1 && rear == -1) {
        printf("Underflow");
    } else {
        for (int i = front; i <= rear; i++) {
            printf("%d", queue[i]);
        }
    }
}
```

---

## 4. Circular Queue
A circular queue is the extended version of a regular queue where the last element is connected to the first element. Thus forming a circle-like structure.

**Formulas for Circular Queue:**
* Next index: `(rear + 1) % N`
* **Overflow:** `((rear + 1) % N) == front`

### C/C++ Implementation of Circular Queue
```cpp
void enqueue(int x) {
    if (((rear + 1) % N) == front) {
        printf("Overflow");
    } else if (front == -1 && rear == -1) {
        front = rear = 0;
        queue[rear] = x;
    } else {
        rear = (rear + 1) % N;
        queue[rear] = x;
    }
}

void dequeue() {
    if (front == -1 && rear == -1) {
        printf("Underflow");
    } else if (front == rear) {
        printf("%d", queue[front]);
        front = rear = -1;
    } else {
        printf("%d", queue[front]);
        front = (front + 1) % N;
    }
}

void display() {
    int i = front;
    if (front == -1 && rear == -1) {
        printf("Underflow");
    } else {
        while (i != rear) {
            printf("%d", queue[i]);
            i = (i + 1) % N;
        }
        printf("%d", queue[rear]);
    }
}
```

---

## 5. Infix, Postfix, Prefix
**Operator Precedence:**
1. `^` (Highest, Right to Left)
2. `*`, `/` (Next highest, Left to Right)
3. `+`, `-` (Lowest, Left to Right)

* **Infix:** `<Operand> <Operator> <Operand>` -> `2 * 3 + 9 / 3 - 5`
* **Postfix:** `<Operand> <Operand> <Operator>` -> `A B * C D / +`
* **Prefix:** `<Operator> <Operand> <Operand>` -> `+ * A B / C D`

### Conversions (Without Stack)
**Infix to Postfix:**
`a+b*c+(d*e+f)*g` -> `abc*+de*f+g*+`

**Infix to Prefix:**
`(A*B)/D+C*F` -> `+/*ABD*CF`

**Postfix to Infix:**
`ABC*+DE/H*-` -> `A+(B*C)-((D/E)*H)`

**Prefix to Infix:**
`+/*ABD*CF` (Scan Right to Left) -> `(A*B/D)+(C*F)`

### Conversions (Using Stack)
* **Infix to Postfix:** Scan left to right. Highest priority operator will not stay in the stack when lowest priority operator is inserted. Pop all operators on `)` until `(`.
* **Infix to Prefix:** Reverse the infix string, scan left to right (or scan right to left). Apply stack rules.
* **Postfix to Infix/Prefix:** Scan left to right. Push operands. On operator, pop two operands, create a combined string, and push back.
* **Prefix to Infix/Postfix:** Scan right to left. Push operands. On operator, pop two operands, create string, push back.

---

## 6. Linked List
A linked list is a linear data structure that stores a collection of data elements dynamically. Nodes represent data elements and links/pointers connect each node.

**Types:**
1. **Singly Linked List:** Nodes only point to the address of the next node.
2. **Doubly Linked List:** Nodes point to the addresses of both previous and next nodes.
3. **Circular Linked List:** The last node points to the first node.

### Singly Linked List Implementation
```cpp
#include <iostream>
using namespace std;

// Creating a Node
class Node {
public:
    int value;
    Node* next;
};

int main() {
    Node* head;
    Node* one = NULL;
    Node* two = NULL;
    Node* three = NULL;

    // allocate 3 nodes in the heap
    one = new Node();
    two = new Node();
    three = new Node();

    // Assign data values
    one->value = 1;
    two->value = 2;
    three->value = 3;

    // connect nodes
    one->next = two;
    two->next = three;
    three->next = NULL;

    // Print the linked list
    head = one;
    while (head != NULL) {
        cout << head->value;
        head = head->next;
    }
}
```

---

## 7. Trees
A tree is a non-linear data structure, a collection of entities (nodes) that simulate hierarchy.

**Terminology:**
* **Root:** Node with no parent.
* **Node:** Stores information and links to other nodes.
* **Parent node:** Immediate predecessor.
* **Child Node:** Immediate successor.
* **Leaf Node:** Node with no children.
* **Non-Leaf / Internal Node:** Has at least one child.
* **Path:** Sequence of consecutive edges from source to destination.
* **Ancestor:** Predecessors on the path from the root.
* **Descendent:** Successors on the path to a leaf node.
* **Siblings:** Children from the same parent.
* **Degree:** Number of children a node has.
* **Depth of node:** Number of edges from the root to the node.
* **Height of node:** Number of edges on the longest path from the node to a leaf.
* **Level of node:** Same as depth. Level of tree = height of root.

### Binary Tree
Every node has at most 2 children (0, 1, 2).
* Max nodes for height $h$: $2^{h+1} - 1$
* Min nodes for height $h$: $h + 1$
* Min height for $n$ nodes: $\lfloor \log_2(n+1) - 1 \rfloor$
* Max height for $n$ nodes: $n - 1$

### Types of Binary Tree
1. **Full Binary Tree:** Every node has 0 or 2 children.
   * Min nodes: $2h + 1$
   * Max nodes: $2^{h+1} - 1$
   * Min height: $\lfloor \log_2(n+1) - 1 \rfloor$
   * Max height: $(n - 1) / 2$
2. **Complete Binary Tree:** Every level is completely filled except possibly the last, and the last level is filled from left to right.
   * Min height: $\lfloor \log_2(n+1) - 1 \rfloor$
   * Max height: $\lfloor \log_2 n \rfloor$
3. **Perfect Binary Tree:** All internal nodes have 2 children, and all leaf nodes are on the same level.

### Tree Traversals
1. **Pre Order:** Root, Left, Right
2. **In Order:** Left, Root, Right
3. **Post Order:** Left, Right, Root

*(Notes include rules for constructing a binary tree given Preorder/Inorder, Postorder/Inorder, and Preorder/Postorder traversals).*

---

## 8. Binary Search Tree (BST)
**Insertion:**
1. Left sub-tree values are less than the Root.
2. Right sub-tree values are greater than the Root.

**Deletion:**
1. Leaf node can be easily deleted.
2. To replace a deleted Root from the Left side, take the **Maximum** value from the left sub-tree.
3. To replace a deleted Root from the Right side, take the **Minimum** value from the right sub-tree.

---

## 9. B-Tree & B+ Tree
**B-Tree Properties:**
* Follows BST rules.
* All leaf nodes must be at the same level.
* Every node has a maximum of $m-1$ keys and $m$ children.
* Data is inserted in ascending order.
* Minimum no of keys: $\lceil m/2 \rceil - 1$

**B+ Tree Properties:**
* All data is stored in the leaf nodes.
* Internal nodes only act as routing indexes (data repeats in the leaf).
* Leaf nodes are linked together.

---

## 10. Graphs
**Representations:**
1. **Adjacency Matrix:** A 2D array of size $V \times V$. `adj[i][j] = 1` if there is an edge, else `0`.
2. **Incidence Matrix:** A 2D array of size $V \times E$. `adj[i][j] = 1` (outgoing), `-1` (incoming), `0` (no connection).
3. **Adjacency List:** An array of lists representing connections for each vertex.

### Graph Traversals
* **BFS (Breadth-First Search):** Uses a **Queue**. Visits all adjacent vertices level by level.
* **DFS (Depth-First Search):** Uses a **Stack**. Explores as far as possible along each branch before backtracking.

**Classification of edges in DFS:**
* **Tree edge:** Edges present in the DFS tree.
* **Forward edge:** Node $x$ to $y$ where $x$ is an ancestor of $y$.
* **Back edge:** Node $x$ to $y$ where $y$ is an ancestor of $x$ (creates a cycle).
* **Cross edge:** No ancestor-descendant relationship.

---

## 11. Hashing
**Hash Functions:**
1. **Division Method:** `k % m`
2. **Mid-square Method:** Square the key, extract middle digits.
3. **Folding Method:** Divide key into parts and add them.

**Collision Resolution:**
1. **Open Hashing (Closed Addressing):** Chaining (using linked lists).
2. **Closed Hashing (Open Addressing):**
   * **Linear Probing:** $h'(k) = (h(k) + i) \% m$
   * **Quadratic Probing:** $h'(k) = (h(k) + i^2) \% m$
   * **Double Hashing:** $h'(k) = (h_1(k) + i \times h_2(k)) \% m$

---

## 12. Array
An array is a collection of similar elements stored at contiguous memory locations.

**Characteristics:**
* **Fixed Size:** Memory allocated at compile time.
* **Random Access:** Can directly access any element using index.
* **0-indexed:** First element is at index 0.
* **Homogeneous:** All elements must be of the same data type.

**Operations:**
* **Insertion:** $O(n)$
* **Deletion:** $O(n)$
* **Search:** $O(n)$ Linear, $O(\log n)$ Binary (if sorted)
* **Access:** $O(1)$

**2D Array (Matrix):**
* Stored in **Row-major order** or **Column-major order**.
* Access: `array[i][j]` where $0 \leq i < rows$ and $0 \leq j < columns$

### Array Implementation
```cpp
// 1D Array
int arr[10];
arr[0] = 5;

// 2D Array
int matrix[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};

// Dynamic Array
int* arr = new int[n];
```

---

## 13. Heap
A heap is a complete binary tree that satisfies the heap property.

**Types:**
1. **Max Heap:** Parent node value is greater than or equal to its children.
2. **Min Heap:** Parent node value is less than or equal to its children.

**Formulas:**
* For node at index $i$:
  * Parent: $(i - 1) / 2$
  * Left Child: $2i + 1$
  * Right Child: $2i + 2$

**Operations:**
* **Insert:** $O(\log n)$
* **Delete (Remove root):** $O(\log n)$
* **Heapify:** $O(\log n)$
* **Build Heap:** $O(n)$

### Heap Operations
```cpp
// Insert in Max Heap
void insertMax(int x) {
    arr[size] = x;
    int i = size;
    size++;
    while (i > 0 && arr[(i-1)/2] < arr[i]) {
        swap(arr[i], arr[(i-1)/2]);
        i = (i-1)/2;
    }
}

// Delete from Max Heap (Remove root)
void deleteMax() {
    arr[0] = arr[size-1];
    size--;
    heapify(0);
}

// Heapify function
void heapify(int i) {
    int largest = i;
    int left = 2*i + 1;
    int right = 2*i + 2;
    
    if (left < size && arr[left] > arr[largest])
        largest = left;
    if (right < size && arr[right] > arr[largest])
        largest = right;
    
    if (largest != i) {
        swap(arr[i], arr[largest]);
        heapify(largest);
    }
}
```

---

## 14. Deque (Double Ended Queue)
A deque is a special kind of queue where insertion and deletion can be done from both ends.

**Operations:**
* **insertFront():** Insert at front end.
* **insertRear():** Insert at rear end.
* **deleteFront():** Delete from front end.
* **deleteRear():** Delete from rear end.

**Conditions:**
* **Overflow:** `front == -1`
* **Underflow:** `front > rear`

### Deque Implementation
```cpp
void insertFront(int x) {
    if (front == 0)
        printf("Overflow");
    else
        deque[--front] = x;
}

void insertRear(int x) {
    if (rear == n - 1)
        printf("Overflow");
    else
        deque[++rear] = x;
}

void deleteFront() {
    if (front > rear)
        printf("Underflow");
    else
        printf("%d", deque[front++]);
}

void deleteRear() {
    if (front > rear)
        printf("Underflow");
    else
        printf("%d", deque[rear--]);
}
```

---

## 15. Trie (Prefix Tree)
A trie is a tree-like data structure that stores strings efficiently. It's used for prefix-based searches.

**Characteristics:**
* Each node has up to 26 children (for lowercase English letters).
* Root node is empty.
* Each path from root represents a string.

**Operations:**
* **Insert:** $O(m)$ where $m$ is the length of the string.
* **Search:** $O(m)$
* **Delete:** $O(m)$

### Trie Node & Implementation
```cpp
struct TrieNode {
    map<char, TrieNode*> children;
    bool isEndOfWord = false;
};

class Trie {
private:
    TrieNode* root;
    
public:
    Trie() {
        root = new TrieNode();
    }
    
    void insert(string word) {
        TrieNode* node = root;
        for (char c : word) {
            if (node->children.find(c) == node->children.end())
                node->children[c] = new TrieNode();
            node = node->children[c];
        }
        node->isEndOfWord = true;
    }
    
    bool search(string word) {
        TrieNode* node = root;
        for (char c : word) {
            if (node->children.find(c) == node->children.end())
                return false;
            node = node->children[c];
        }
        return node->isEndOfWord;
    }
    
    bool startsWith(string prefix) {
        TrieNode* node = root;
        for (char c : prefix) {
            if (node->children.find(c) == node->children.end())
                return false;
            node = node->children[c];
        }
        return true;
    }
};
```

---

## 16. AVL Tree (Adelson-Velsky and Landis Tree)
An AVL tree is a self-balancing binary search tree where the heights of the left and right subtrees differ by at most 1.

**Balance Factor:** $BF = height(left) - height(right)$
**Valid BF:** $-1, 0, +1$
**Invalid BF:** $< -1$ or $> +1$

**Rotations (To balance tree):**
1. **Left Rotation:** When BF > 1 and left child's BF ≥ 0
2. **Right Rotation:** When BF < -1 and right child's BF ≤ 0
3. **Left-Right Rotation:** When BF > 1 and left child's BF < 0
4. **Right-Left Rotation:** When BF < -1 and right child's BF > 0

**Operations:**
* **Insert:** $O(\log n)$
* **Delete:** $O(\log n)$
* **Search:** $O(\log n)$

---

## 17. Red-Black Tree
A red-black tree is a self-balancing binary search tree with the following properties:

**Properties:**
1. Every node is either red or black.
2. Root is always black.
3. All leaves (NULL nodes) are black.
4. If a node is red, then both its children are black.
5. All paths from a node to its descendant leaves have the same number of black nodes.

**Operations:**
* **Insert:** $O(\log n)$
* **Delete:** $O(\log n)$
* **Search:** $O(\log n)$

---

## 18. Segment Tree
A segment tree is a tree data structure used for efficient range queries and updates on an array.

**Use Cases:**
* Range Sum Query
* Range Minimum/Maximum Query
* Range Update

**Operations:**
* **Build:** $O(n)$
* **Query:** $O(\log n)$
* **Update:** $O(\log n)$

### Segment Tree Implementation
```cpp
class SegmentTree {
private:
    vector<int> tree;
    
    void build(vector<int>& arr, int node, int start, int end) {
        if (start == end) {
            tree[node] = arr[start];
        } else {
            int mid = (start + end) / 2;
            build(arr, 2*node, start, mid);
            build(arr, 2*node+1, mid+1, end);
            tree[node] = tree[2*node] + tree[2*node+1];
        }
    }
    
    void update(int node, int start, int end, int idx, int val) {
        if (start == end) {
            tree[node] = val;
        } else {
            int mid = (start + end) / 2;
            if (idx <= mid)
                update(2*node, start, mid, idx, val);
            else
                update(2*node+1, mid+1, end, idx, val);
            tree[node] = tree[2*node] + tree[2*node+1];
        }
    }
    
    int query(int node, int start, int end, int l, int r) {
        if (r < start || end < l)
            return 0;
        if (l <= start && end <= r)
            return tree[node];
        
        int mid = (start + end) / 2;
        return query(2*node, start, mid, l, r) +
               query(2*node+1, mid+1, end, l, r);
    }
};
```

---

## 19. Union-Find (Disjoint Set Union)
Union-Find is a data structure that supports two main operations: union (merge sets) and find (determine which set an element belongs to).

**Operations:**
* **Find(x):** $O(\alpha(n))$ with path compression
* **Union(x, y):** $O(\alpha(n))$ with union by rank

### Union-Find Implementation
```cpp
class UnionFind {
private:
    vector<int> parent;
    vector<int> rank;
    
public:
    UnionFind(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; i++)
            parent[i] = i;
    }
    
    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]); // Path compression
        return parent[x];
    }
    
    void unite(int x, int y) {
        int px = find(x);
        int py = find(y);
        
        if (px == py) return;
        
        // Union by rank
        if (rank[px] < rank[py])
            parent[px] = py;
        else if (rank[px] > rank[py])
            parent[py] = px;
        else {
            parent[py] = px;
            rank[px]++;
        }
    }
    
    bool connected(int x, int y) {
        return find(x) == find(y);
    }
};
```

---

## 20. Doubly Linked List
A doubly linked list is a linked list where each node has pointers to both the next and previous nodes.

**Advantages:**
* Can traverse in both directions.
* Easier deletion (have both pointers).
* Suitable for implementing stacks, queues, and deques.

**Node Structure:**
```cpp
struct Node {
    int data;
    Node* next;
    Node* prev;
};
```

**Operations:**
* **Insert at Beginning:** $O(1)$
* **Insert at End:** $O(n)$
* **Delete from Beginning:** $O(1)$
* **Delete from End:** $O(n)$
* **Search:** $O(n)$
* **Traverse:** $O(n)$

### Doubly Linked List Implementation
```cpp
// Insert at beginning
void insertBeginning(int x) {
    Node* newNode = new Node();
    newNode->data = x;
    newNode->next = head;
    newNode->prev = NULL;
    
    if (head != NULL)
        head->prev = newNode;
    head = newNode;
}

// Delete from beginning
void deleteBeginning() {
    if (head == NULL) return;
    Node* temp = head;
    head = head->next;
    if (head != NULL)
        head->prev = NULL;
    delete temp;
}

// Traverse Forward
void traverseForward() {
    Node* temp = head;
    while (temp != NULL) {
        cout << temp->data << " ";
        temp = temp->next;
    }
}

// Traverse Backward
void traverseBackward() {
    Node* temp = head;
    if (temp == NULL) return;
    
    while (temp->next != NULL)
        temp = temp->next;
    
    while (temp != NULL) {
        cout << temp->data << " ";
        temp = temp->prev;
    }
}
```

---

## 21. Circular Linked List
A circular linked list is a linked list where the last node points back to the first node, forming a circle.

**Characteristics:**
* No NULL pointer at the end.
* Last node points to first node.
* Can be singly or doubly circular.

**Operations:**
* **Insert at Beginning:** $O(1)$
* **Delete from Beginning:** $O(1)$
* **Search:** $O(n)$
* **Traverse:** $O(n)$

### Circular Linked List Implementation
```cpp
struct Node {
    int data;
    Node* next;
};

// Insert at beginning
void insertBeginning(int x) {
    Node* newNode = new Node();
    newNode->data = x;
    
    if (head == NULL) {
        head = newNode;
        newNode->next = head;
    } else {
        Node* temp = head;
        while (temp->next != head)
            temp = temp->next;
        
        newNode->next = head;
        temp->next = newNode;
        head = newNode;
    }
}

// Delete from beginning
void deleteBeginning() {
    if (head == NULL) return;
    
    if (head->next == head) {
        delete head;
        head = NULL;
    } else {
        Node* temp = head;
        while (temp->next != head)
            temp = temp->next;
        
        Node* toDelete = head;
        head = head->next;
        temp->next = head;
        delete toDelete;
    }
}

// Traverse
void traverse() {
    if (head == NULL) return;
    
    Node* temp = head;
    do {
        cout << temp->data << " ";
        temp = temp->next;
    } while (temp != head);
}
```

---

## 22. Priority Queue
A priority queue is an abstract data type where elements are served based on their priority, not in FIFO order.

**Characteristics:**
* **Min Heap:** Smallest priority element comes out first.
* **Max Heap:** Largest priority element comes out first.
* **Implementation:** Usually implemented using heaps.

**Operations:**
* **Insert:** $O(\log n)$
* **Delete (Extract-max/min):** $O(\log n)$
* **Peek:** $O(1)$

### Priority Queue Implementation
```cpp
#include <queue>
using namespace std;

// Max Heap Priority Queue
priority_queue<int> pq;

// Min Heap Priority Queue
priority_queue<int, vector<int>, greater<int>> minPQ;

// Insert
pq.push(5);
pq.push(10);
pq.push(3);

// Get max element
int maxElem = pq.top();

// Delete max element
pq.pop();

// Size
int size = pq.size();
```

---

## 23. Fenwick Tree (Binary Indexed Tree)
A Fenwick tree is a data structure that efficiently supports prefix sum queries and updates on an array.

**Use Cases:**
* Range Sum Query
* Efficient updates and queries in $O(\log n)$
* Used in inversion count problems

**Operations:**
* **Update:** $O(\log n)$
* **Query:** $O(\log n)$
* **Build:** $O(n \log n)$

### Fenwick Tree Implementation
```cpp
class FenwickTree {
private:
    vector<int> tree;
    int n;
    
public:
    FenwickTree(int n) : n(n), tree(n + 1, 0) {}
    
    void update(int idx, int delta) {
        idx++; // 1-indexed
        while (idx <= n) {
            tree[idx] += delta;
            idx += idx & (-idx);
        }
    }
    
    int query(int idx) {
        idx++; // 1-indexed
        int sum = 0;
        while (idx > 0) {
            sum += tree[idx];
            idx -= idx & (-idx);
        }
        return sum;
    }
    
    int rangeQuery(int l, int r) {
        if (l == 0)
            return query(r);
        return query(r) - query(l - 1);
    }
};
```

---

## Handwritten Notes

I have documented my learning journey in Data Structures and Algorithms with handwritten notes. You can access the PDFs here:

- [📄 Data Structures Handwritten Notes] (https://drive.google.com/file/d/1BKg1VpmiADVZWj8bz27d-UdW1XkvRcFs/view?usp=sharing)