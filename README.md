[blahh](./waste.html)

![image](https://github.com/user-attachments/assets/b2bf3de3-26fe-4907-b0d3-d957306282ba)

# DAA_

## Hello! Welcome to our city.

Let me help you go through the content.
- [Introduction](./Introduction.md)
- [Course Reflection](https://apekshadambal.github.io/Course-Learning-Reflections/)



| Order      | Description                        | Example                           |
|------------|------------------------------------|-----------------------------------|
| O(1)       | Constant time                     | Accessing an element in an array |
| O(log n)   | Logarithmic time                  | Binary search                    |
| O(n)       | Linear time                       | Linear search                    |
| O(n log n) | Log-linear time                   | Sorting algorithms like MergeSort |
| O(n²)      | Quadratic time                    | Bubble Sort                      |
| O(2ⁿ)      | Exponential time                  | Solving the Tower of Hanoi       |


## Algorithm Overview

1. Kinds of Problems in Nature

## Iteration Example: Factorial Calculation

    long long factorial(int n) {
    long long result = 1;
    for (int i = 1; i <= n; ++i) {
        result *= i;
    }
    return result;
    }

## Recursion Example: Fibonacci Series

    int fibonacci(int n) {
    if (n <= 1) {
        return n;
    }
    return fibonacci(n - 1) + fibonacci(n - 2);
    }

## Recursion Example: Tower of Hanoi

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

## Backtracking Example: N-Queens Problem

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
