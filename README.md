# Sovon's DSA and CP Journey 🚀
Welcome to my journey of mastering Competitive Programming and Data Structures & Algorithms (DSA).  
I'm currently learning from various online resources and solving problems on platforms like Codeforces and LeetCode.

## Topics Covered
- [x] Recursion
- [ ] Backtracking
- [ ] Dynamic Programming

## Progress Tracker
| Topic          | Problems Solved |
|----------------|-----------------|
| Recursion      | 11             |
| Backtracking   | 0              |

```
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
