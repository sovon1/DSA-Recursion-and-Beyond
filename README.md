# Sovon's DSA and CP Journey 🚀

Welcome to my journey of mastering Competitive Programming and Data Structures & Algorithms (DSA).  
I'm currently learning from various online resources and solving problems on platforms like Codeforces and LeetCode.

## Table of Contents
- [Topics Covered](#topics-covered)
- [Progress Tracker](#progress-tracker)
- [Example Code Snippets](#example-code-snippets)
  - [Backtracking Algorithm](#backtracking-algorithm)
  - [Permutation Generation](#permutation-generation)
  - [Permutation Tree Visualization](#permutation-tree-visualization)
  - [N-Queens Problem](#n-queens-problem)
- [Contribution](#contribution)

## Topics Covered
- [x] Recursion
- [ ] Backtracking
- [ ] Dynamic Programming

## Progress Tracker
| Topic          | Problems Solved |
|----------------|-----------------|
| Recursion      | 11              |
| Backtracking   | 0               |

## Example Code Snippets

### Backtracking Algorithm
```cpp
void backtrack(params, state, result) {
    // Base case: solution found
    if (condition_met) {
        result.push_back(state);
        return;
    }
    // Base case: invalid path
    if (out_of_bounds || invalid_state) return;

    for (each choice in possible_choices) {
        // Make a choice
        update_state(choice);
        // Recurse
        backtrack(params, state, result);
        // Undo choice (backtrack)
        revert_state(choice);
    }
}
```

### Permutation Generation
This example demonstrates generating all permutations of an array using backtracking.

```cpp
#include <bits/stdc++.h>
using namespace std;

void permutation(int idx, int arr[], int n, vector<vector<int>> &nv) {
    // Base case: when idx reaches n, store the permutation
    if (idx == n) {
        vector<int> ds(arr, arr + n);
        nv.push_back(ds);
        return;
    }

    for (int i = idx; i < n; i++) {
        swap(arr[idx], arr[i]); // Swap the current element with the element at index i
        permutation(idx + 1, arr, n, nv); // Recursively call the function with the next index
        swap(arr[idx], arr[i]); // Backtrack: swap the elements back to their original positions
    }
}

int main() {
    int arr[] = {1, 2, 3};
    int n = sizeof(arr) / sizeof(arr[0]);

    vector<vector<int>> nv; // Stores all permutations

    permutation(0, arr, n, nv);

    // Print all permutations
    for (auto &perm : nv) {
        for (int num : perm) cout << num << " ";
        cout << endl;
    }

    return 0;
}
```

### Permutation Tree Visualization
Here's a visual representation of the permutation generation process:

```
Root: idx=0, arr={1,2,3}
├── i=0: arr={1,2,3}
│   ├── idx=1, arr={1,2,3}
│   │   ├── i=1: arr={1,2,3}
│   │   │   └── idx=2, arr={1,2,3} → idx=3 (Base: {1,2,3})
│   │   └── i=2: arr={1,3,2}
│   │       └── idx=2, arr={1,3,2} → idx=3 (Base: {1,3,2})
├── i=1: arr={2,1,3}
│   ├── idx=1, arr={2,1,3}
│   │   ├── i=1: arr={2,1,3}
│   │   │   └── idx=2, arr={2,1,3} → idx=3 (Base: {2,1,3})
│   │   └── i=2: arr={2,3,1}
│   │       └── idx=2, arr={2,3,1} → idx=3 (Base: {2,3,1})
└── i=2: arr={3,2,1}
    ├── idx=1, arr={3,2,1}
    │   ├── i=1: arr={3,2,1}
    │   │   └── idx=2, arr={3,2,1} → idx=3 (Base: {3,2,1})
    │   └── i=2: arr={3,1,2}
    │       └── idx=2, arr={3,1,2} → idx=3 (Base: {3,1,2})
```

### N-Queens Problem
This example demonstrates solving the N-Queens problem using backtracking.

```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to check if it's safe to place a queen at board[row][col]
bool issafe(int row, int col, vector<string>& board, int n) {
    int duprow = row;
    int dupcol = col;

    // Check upper diagonal on left side
    while (row >= 0 && col >= 0) {
        if (board[row][col] == 'Q') return false;
        row--;
        col--;
    }

    // Check left side
    row = duprow;
    col = dupcol;
    while (col >= 0) {
        if (board[row][col] == 'Q') return false;
        col--;
    }

    // Check lower diagonal on left side
    row = duprow;
    col = dupcol;
    while (row < n && col >= 0) {
        if (board[row][col] == 'Q') return false;
        row++;
        col--;
    }

    return true;
}

// Function to solve the N-Queen problem
void solve(int col, vector<string> &board, vector<vector<string>> &ans, int n) {
    if (col == n) {
        ans.push_back(board);
        return;
    }

    // Perform row-wise traversal to check if placing queen is safe
    for (int row = 0; row < n; row++) {
        if (issafe(row, col, board, n)) {
            board[row][col] = 'Q';
            solve(col + 1, board, ans, n);
            board[row][col] = '.'; // Backtrack
        }
    }
}

int main() {
    int n = 4; 

    // Initialize the board with empty strings
    vector<string> board(n, string(n, '.'));
  
    // This will store all the possible solutions
    vector<vector<string>> ans;

    // Start solving from the first column
    solve(0, board, ans, n);

    // Print all the solutions
    for (auto solution : ans) {
        for (auto row : solution) {
            cout << row << endl;
        }
        cout << endl;
    }

    return 0;
}
```

### N-Queens Backtracking Visualization (N=4)

#### Initial Board
```
. . . .
. . . .
. . . .
. . . .
```

#### The Backtracking Process

##### Column 0 Exploration

1. **Try row=0, col=0**
   - Is it safe? YES
   - Place queen and move to next column
   ```
   Q . . .
   . . . .
   . . . .
   . . . .
   ```

##### Column 1 Exploration (after placing queen at row=0, col=0)

2. **Try row=0, col=1**
   - Is it safe? NO (same row attack)
   
3. **Try row=1, col=1**
   - Is it safe? NO (diagonal attack)
   
4. **Try row=2, col=1**
   - Is it safe? YES
   - Place queen and move to next column
   ```
   Q . . .
   . . . .
   . Q . .
   . . . .
   ```

##### Column 2 Exploration (after placing queens at [0,0] and [2,1])

5. **Try row=0, col=2**
   - Is it safe? NO (diagonal attack from [2,1])
   
6. **Try row=1, col=2**
   - Is it safe? NO (diagonal attack from [0,0])
   
7. **Try row=2, col=2**
   - Is it safe? NO (same row as [2,1])
   
8. **Try row=3, col=2**
   - Is it safe? NO (diagonal attack from [2,1])
   
9. **BACKTRACK:** No valid placement in column 2, so remove queen from [2,1]
   ```
   Q . . .
   . . . .
   . . . .
   . . . .
   ```

##### Column 1 Exploration (continued)

10. **Try row=3, col=1**
    - Is it safe? YES
    - Place queen and move to next column
    ```
    Q . . .
    . . . .
    . . . .
    . Q . .
    ```

##### Column 2 Exploration (after placing queens at [0,0] and [3,1])

11. **Try row=0, col=2**
    - Is it safe? NO (diagonal attack)
    
12. **Try row=1, col=2**
    - Is it safe? YES
    - Place queen and move to next column
    ```
    Q . . .
    . . Q .
    . . . .
    . Q . .
    ```

##### Column 3 Exploration (after placing queens at [0,0], [3,1], and [1,2])

13. **Try row=0, col=3**
    - Is it safe? NO (diagonal attack)
    
14. **Try row=1, col=3**
    - Is it safe? NO (same row attack)
    
15. **Try row=2, col=3**
    - Is it safe? YES
    - Place queen and we've reached the end!
    ```
    Q . . .
    . . Q .
    . . . Q
    . Q . .
    ```
    
16. **SOLUTION FOUND!** Add to answer list

17. **BACKTRACK:** Remove queen from [2,3] and try next row
    ```
    Q . . .
    . . Q .
    . . . .
    . Q . .
    ```

18. **Try row=3, col=3**
    - Is it safe? NO (same row attack)
    
19. **BACKTRACK:** No more options in column 3, so remove queen from [1,2]
    ```
    Q . . .
    . . . .
    . . . .
    . Q . .
    ```

##### Column 2 Exploration (continued)

... (continuing the backtracking process through all possibilities)

#### Final Solutions for N=4

##### Solution 1
```
. Q . .
. . . Q
Q . . .
. . Q .
```

##### Solution 2
```
. . Q .
Q . . .
. . . Q
. Q . .
```

The algorithm found 2 solutions for N=4.

## Contribution
Feel free to contribute by submitting issues or pull requests. Make sure to follow the contribution guidelines.
