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

### Detailed Permutation Tree Visualization
Here's a detailed visual representation of the permutation generation process:

```
Root: idx=0, arr={1,2,3}
├── i=0: swap(arr[0], arr[0]) → {1,2,3} (no change)
│   ├── Call: idx=1, arr={1,2,3}
│   │   ├── i=1: swap(arr[1], arr[1]) → {1,2,3} (no change)
│   │   │   ├── Call: idx=2, arr={1,2,3}
│   │   │   │   └── i=2: swap(arr[2], arr[2]) → {1,2,3} (no change)
│   │   │   │       ├── Call: idx=3, arr={1,2,3}
│   │   │   │       │   └── Base case: Add {1,2,3} to nv
│   │   │   │       └── Backtrack: swap(arr[2], arr[2]) → {1,2,3}
│   │   │   └── Backtrack: swap(arr[1], arr[1]) → {1,2,3}
│   │   └── i=2: swap(arr[1], arr[2]) → {1,3,2}
│   │       ├── Call: idx=2, arr={1,3,2}
│   │       │   └── i=2: swap(arr[2], arr[2]) → {1,3,2} (no change)
│   │       │       ├── Call: idx=3, arr={1,3,2}
│   │       │       │   └── Base case: Add {1,3,2} to nv
│   │       │       └── Backtrack: swap(arr[2], arr[2]) → {1,3,2}
│   │       └── Backtrack: swap(arr[1], arr[2]) → {1,2,3}
│   └── Backtrack: swap(arr[0], arr[0]) → {1,2,3}
├── i=1: swap(arr[0], arr[1]) → {2,1,3}
│   ├── Call: idx=1, arr={2,1,3}
│   │   ├── i=1: swap(arr[1], arr[1]) → {2,1,3} (no change)
│   │   │   ├── Call: idx=2, arr={2,1,3}
│   │   │   │   └── i=2: swap(arr[2], arr[2]) → {2,1,3} (no change)
│   │   │   │       ├── Call: idx=3, arr={2,1,3}
│   │   │   │       │   └── Base case: Add {2,1,3} to nv
│   │   │   │       └── Backtrack: swap(arr[2], arr[2]) → {2,1,3}
│   │   │   └── Backtrack: swap(arr[1], arr[1]) → {2,1,3}
│   │   └── i=2: swap(arr[1], arr[2]) → {2,3,1}
│   │       ├── Call: idx=2, arr={2,3,1}
│   │       │   └── i=2: swap(arr[2], arr[2]) → {2,3,1} (no change)
│   │       │       ├── Call: idx=3, arr={2,3,1}
│   │       │       │   └── Base case: Add {2,3,1} to nv
│   │       │       └── Backtrack: swap(arr[2], arr[2]) → {2,3,1}
│   │       └── Backtrack: swap(arr[1], arr[2]) → {2,1,3}
│   └── Backtrack: swap(arr[0], arr[1]) → {1,2,3}
└── i=2: swap(arr[0], arr[2]) → {3,2,1}
    ├── Call: idx=1, arr={3,2,1}
    │   ├── i=1: swap(arr[1], arr[1]) → {3,2,1} (no change)
    │   │   ├── Call: idx=2, arr={3,2,1}
    │   │   │   └── i=2: swap(arr[2], arr[2]) → {3,2,1} (no change)
    │   │   │       ├── Call: idx=3, arr={3,2,1}
    │   │   │       │   └── Base case: Add {3,2,1} to nv
    │   │   │       └── Backtrack: swap(arr[2], arr[2]) → {3,2,1}
    │   │   └── Backtrack: swap(arr[1], arr[1]) → {3,2,1}
    │   └── i=2: swap(arr[1], arr[2]) → {3,1,2}
    │       ├── Call: idx=2, arr={3,1,2}
    │       │   └── i=2: swap(arr[2], arr[2]) → {3,1,2} (no change)
    │       │       ├── Call: idx=3, arr={3,1,2}
    │       │       │   └── Base case: Add {3,1,2} to nv
    │       │       └── Backtrack: swap(arr[2], arr[2]) → {3,1,2}
    │       └── Backtrack: swap(arr[1], arr[2]) → {3,2,1}
    └── Backtrack: swap(arr[0], arr[2]) → {1,2,3}
```

## Contribution
Feel free to contribute by submitting issues or pull requests. Make sure to follow the contribution guidelines.
