/*
** Algorithm Overview **

1. Kinds of Problems in Nature
*/

// Iteration Example: Factorial Calculation
long long factorial(int n) {
    long long result = 1;
    for (int i = 1; i <= n; ++i) {
        result *= i;
    }
    return result;
}

// Recursion Example: Fibonacci Series
int fibonacci(int n) {
    if (n <= 1) {
        return n;
    }
    return fibonacci(n - 1) + fibonacci(n - 2);
}

// Recursion Example: Tower of Hanoi
#include <stdio.h>
void towers(int n, char from, char to, char aux) {
    if (n == 1) {
        printf("Move disk 1 from %c to %c\n", from, to);
        return;
    }
    towers(n - 1, from, aux, to);
    printf("Move disk %d from %c to %c\n", n, from, to);
    towers(n - 1, aux, to, from);
}

int main() {
    int n;
    printf("Enter the number of Disks to be moved\n");
    scanf("%d", &n);
    towers(n, 'A', 'C', 'B');
    return 0;
}

// Backtracking Example: N-Queens Problem
#include <iostream>
using namespace std;

bool isSafe(int board[][10], int row, int col, int N) {
    for (int i = 0; i < row; i++) {
        if (board[i][col] == 1 || 
            (col - (row - i) >= 0 && board[i][col - (row - i)] == 1) || 
            (col + (row - i) < N && board[i][col + (row - i)] == 1)) {
            return false;
        }
    }
    return true;
}

bool solveNQueens(int board[][10], int row, int N) {
    if (row == N) {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                cout << (board[i][j] ? "Q " : ". ");
            }
            cout << endl;
        }
        cout << endl;
        return true;
    }
    
    bool res = false;
    for (int col = 0; col < N; col++) {
        if (isSafe(board, row, col, N)) {
            board[row][col] = 1;
            res = solveNQueens(board, row + 1, N) || res;
            board[row][col] = 0;
        }
    }
    return res;
}

void solveNQueens(int N) {
    int board[10][10] = {0};
    if (!solveNQueens(board, 0, N)) {
        cout << "Solution does not exist!" << endl;
    }
}

int main() {
    int N;
    cout << "Enter the value of N: ";
    cin >> N;
    solveNQueens(N);
    return 0;
}
#2. Space and Time Efficiency

## Space Efficiency
- *Definition*: The amount of memory an algorithm uses during execution.
- *Importance*: Reduces memory consumption, crucial in memory-constrained systems.
- *Example*: Recursive algorithms (like computing Fibonacci numbers) may need more memory because each recursive call adds a new layer to the call stack.

## Time Efficiency
- *Definition*: The time an algorithm takes to run, measured in terms of input size (asymptotic analysis).
- *Importance*: Reduces execution time, critical in time-sensitive systems like real-time applications.

---

# Classes of Problems

- *P*: Problems solvable in polynomial time (e.g., sorting).
- *NP*: Problems for which solutions can be verified in polynomial time (e.g., traveling salesman).
- *NP-Hard/NP-Complete*: Problems that are at least as hard as NP problems, with no known polynomial-time solutions.

---

# Orders of Growth

| Order      | Description                        | Example                           |
|------------|------------------------------------|-----------------------------------|
| O(1)       | Constant time                     | Accessing an element in an array |
| O(log n)   | Logarithmic time                  | Binary search                    |
| O(n)       | Linear time                       | Linear search                    |
| O(n log n) | Log-linear time                   | Sorting algorithms like MergeSort |
| O(n²)      | Quadratic time                    | Bubble Sort                      |
| O(2ⁿ)      | Exponential time                  | Solving the Tower of Hanoi       |
## 3. Takeaways from Design Principles

### Divide and Conquer
- Break a problem into smaller sub-problems, solve them, and combine results (e.g., MergeSort, QuickSort).

#### Merge Sort
```pseudo
ALGORITHM MergeSort(A[0..n-1])
    // Sorts a given array A[0..n-1] by recursive mergesort
    // Input: An array A[0..n-1] of orderable elements
    // Output: Array A[0...n-1] sorted in nondecreasing order

    if n > 1
        copy A[0...|_n/2_| - 1] to B[0...|_n/2_| - 1]
        copy A[|_n/2_| ... n - 1] to C[0...| ̄ n/2  ̄| - 1]
        MergeSort(B[0...|_n/2_| - 1])
        MergeSort(C[0...| ̄ n/2  ̄| - 1])
        Merge(B, C, A)

ALGORITHM Merge(B[0...p-1], C[0...q-1], A[0...p+q-1])
    // Merges two sorted arrays into one sorted array
    // Input: Arrays B[0...p-1] and C[0...q-1] both sorted
    // Output: Sorted array A[0...p+q-1] of the elements of B and C

    i <- 0
    j <- 0
    k <- 0
    while i < p and j < q do
        if B[i] <= C[j]
            A[k] <- B[i]
            i <- i + 1
        else
            A[k] <- C[j]
            j <- j + 1
        k <- k + 1
    if i = p
        copy C[j...q-1] to A[k...p+q-1]
    else
        copy B[i...p-1] to A[k...p+q-1]


### Divide and Conquer
- Break a problem into smaller sub-problems, solve them, and combine results (e.g., MergeSort, QuickSort).

## Greedy Algorithms
- Make locally optimal choices aiming for global optimum (e.g., Prim’s and Kruskal’s algorithms).

### Kruskal’s Algorithm
```cpp
int Find(int parent[], int i) {
    if (parent[i] != i)
        parent[i] = Find(parent, parent[i]);
    return parent[i];
}

void Union(int parent[], int rank[], int x, int y) {
    int xroot = Find(parent, x);
    int yroot = Find(parent, y);

    if (rank[xroot] < rank[yroot])
        parent[xroot] = yroot;
    else if (rank[xroot] > rank[yroot])
        parent[yroot] = xroot;
    else {
        parent[yroot] = xroot;
        rank[xroot]++;
    }
}

void KruskalMST(Edge edges[], int E, int V) {
    int weights[E], idx[E];
    for (int i = 0; i < E; i++) {
        weights[i] = edges[i].weight;
        idx[i] = i;
    }

    MergeSort(weights, idx, 0, E - 1);

    int parent[V], rank[V];
    for (int i = 0; i < V; i++) {
        parent[i] = i;
        rank[i] = 0;
    }

    Edge mst[V - 1];
    int mstSize = 0;

    for (int i = 0; i < E && mstSize < V - 1; i++) {
        Edge edge = edges[idx[i]];
        int x = Find(parent, edge.src);
        int y = Find(parent, edge.dest);

        if (x != y) {
            mst[mstSize++] = edge;
            Union(parent, rank, x, y);
        }
    }

    cout << "Edges in the Minimum Spanning Tree:\n";
    int cost = 0;
    for (int i = 0; i < mstSize; i++) {
        cout << mst[i].src << " -- " << mst[i].dest << " == " << mst[i].weight << endl;
        cost += mst[i].weight;
    }
    cout << "Cost = " << cost << endl;
}
## Brute Force
- Exhaustively explore all possibilities (e.g., string matching).
## 4. Hierarchical Data and Tree Structures

- **Tree**: A hierarchical structure with a root node and child nodes.
- **Binary Search Tree (BST)**: Maintains sorted order for efficient searches.
- **AVL Tree**: Self-balancing BST that prevents skewness.
- **Red-Black Tree**: A balanced BST ensuring logarithmic time operations.
- **Heap**: A complete binary tree used in priority queues.
- **Trie**: Specialized for prefix-based search.
## 5. Array Query Algorithms

- **Segment Tree**: Handles range queries efficiently.
- **Fenwick Tree**: Optimized for cumulative frequency queries.
- **Sparse Table**: Precomputes answers for range queries.
## 6. Trees vs Graphs

### Trees
- A connected, acyclic graph with a single path between nodes.

#### Applications
- XML parsing
- Game trees

### Graphs
- Generalized structure with nodes (vertices) and edges (connections).

#### Applications
- Networking
- Shortest path calculations
## 7. Sorting and Searching Algorithms

### Sorting Techniques
- **Bubble Sort (O(n²))**
- **MergeSort (O(n log n))**
- **QuickSort (average O(n log n))**

#### Bubble Sort
```pseudo
ALGORITHM BubbleSort(A[0..n-1])
    // Sorts a given array using bubble sort
    // Input: An array A[0..n-1] of orderable elements
    // Output: Array A[0...n-1] sorted in ascending order

    for i <- 0 to n - 2 do
        for j <- 0 to n - 2 - i do
            if A[j+1] < A[j]
                swap A[j] and A[j+1]

### Searching Techniques
- **Linear Search (O(n))**
- **Binary Search (O(log n))**
#### Linear Search
```cpp
int linearSearch(const vector& arr, int key) {
    for (int i = 0; i < arr.size(); i++) {
        if (arr[i] == key) return i;
    }
    return -1;
}
#### Binary Search
```cpp
int binarySearch(const vector& arr, int key) {
    int left = 0, right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == key) return mid;
        if (arr[mid] < key) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
## 8. Graph Algorithms

### Spanning Trees
- Minimal cost connectivity (e.g., Prim’s, Kruskal’s).

### Shortest Paths
- Algorithms like Dijkstra, Bellman-Ford, Floyd-Warshall.
## 9. Algorithm Design Techniques

### Divide and Conquer
- Splits problems recursively.

### Dynamic Programming
- Stores intermediate results to avoid recomputation.

### Greedy Algorithms
- Chooses the best current option.

### Backtracking
- Explores solutions and backtracks when constraints fail.

### Branch and Bound
- Optimized searching for combinatorial problems.
