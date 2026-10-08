# Week 5 of Learning DSA in Python: Trees & Binary Search Unlocked

**Tags:** python, dsa, beginners, algorithms, 100daysofcode

---

## Quick Recap

Week 1 → Tools (set, dict, Counter)
Week 2 → Patterns (two pointers, sliding window, prefix sum)
Week 3 → Structures (stack, queue, monotonic stack)
Week 4 → Linked Lists + Recursion
Week 5 → Trees + Binary Search

---

## The Mental Shift

Week 4 gave me linked lists — one next pointer.
Week 5 gave me trees — TWO next pointers.

```python
# Linked List Node — one pointer
class ListNode:
    def __init__(self, val):
        self.val  = val
        self.next = None

# Tree Node — two pointers!
class TreeNode:
    def __init__(self, val):
        self.val   = val
        self.left  = None
        self.right = None
```

Everything from Week 4 applied here.
Recursion became the natural way to traverse trees.

---

## The Tree Recursion Template

Most tree problems fit this one template:

```python
def solve(node):
    if not node:
        return base_case

    left  = solve(node.left)
    right = solve(node.right)

    return combine(left, right)
```

This template solved 6 different problems.
One template. Six problems. That's the power of patterns.

---

## DFS vs BFS

DFS → go deep first → recursion or stack
BFS → go wide first → queue

Key rule:
  Shortest path → always BFS
  Max/min depth → DFS natural fit

BFS template:
```python
queue = deque([root])
while queue:
    size = len(queue)
    for _ in range(size):
        node = queue.popleft()
        if node.left:  queue.append(node.left)
        if node.right: queue.append(node.right)
```

---

## BST Superpower

BST: left < node < right at every level.

O(log n) search — eliminates half each step.
Inorder traversal = sorted order — used for Kth Smallest.

---

## Binary Search

```python
while left <= right:    # <= not <
    mid = left + (right - left) // 2
    if nums[mid] == target:  return mid
    elif nums[mid] < target: left = mid + 1
    else:                    right = mid - 1
```

Why left <= right?
Handles single element where left == right.
Use < and you miss the last element!

---

## The Hardest Problem — Max Path Sum

```python
left_gain  = max(0, solve(node.left))
right_gain = max(0, solve(node.right))
path = node.val + left_gain + right_gain
self.max_sum = max(self.max_sum, path)
return node.val + max(left_gain, right_gain)
```

max(0, subtree) = never include negative paths.
path = update global max.
return = only go ONE direction up.

---

## 15 Problems This Week

| Problem | Key Concept |
|---------|-------------|
| Max Depth | recursion template |
| Invert Tree | swap + recurse |
| Same Tree | compare subtrees |
| Level Order | BFS level freeze |
| Right Side View | last node per level |
| Min Depth | BFS first leaf |
| Validate BST | min/max boundaries |
| LCA of BST | split = ancestor |
| Kth Smallest | inorder = sorted |
| Binary Search | left <= right |
| Search Rotated | one half sorted |
| Find Min Rotated | mid vs right |
| Path Sum | subtract + leaf |
| Balanced Tree | -1 = unbalanced |
| Max Path Sum | max(0,subtree) |

---

## What's Coming in Week 6

Sorting + Heaps — final foundation week.
After this → Graphs, DP, Tries (advanced).

78+ problems in 5 weeks.
All solutions: https://github.com/faizurrahaman27
Daily updates: #100DaysOfDSA
