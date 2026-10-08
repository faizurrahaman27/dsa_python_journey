# Week 4 of Learning DSA in Python: Linked Lists & Recursion Changed How I Think

**Tags:** python, dsa, beginners, algorithms, 100daysofcode

---

## Quick Recap

Week 1 → Tools (set, dict, Counter)
Week 2 → Patterns (two pointers, sliding window, prefix sum)
Week 3 → New Structures (stack, queue, monotonic stack)
Week 4 → Linked Lists + Recursion

---

## The Biggest Mental Shift

Arrays gave me index access — lst[3] in O(1).
Linked lists took that away.

```
Array:        [1, 2, 3, 4, 5]
               ↑  ↑  ↑  ↑  ↑
               direct access

Linked List:  1 → 2 → 3 → 4 → 5
              must traverse from head
```

No shortcuts. No jumping. Just pointers.

---

## What I Learned

### Three Pointer Reverse

```python
prev = None
current = head

while current:
    next_node = current.next   # SAVE
    current.next = prev        # REVERSE
    prev = current             # MOVE prev
    current = next_node        # MOVE current

return prev
```

4 actions. Every iteration. Never changes.

### Dummy Node Pattern

```python
dummy = ListNode(0)
current = dummy

# build result...

return dummy.next
```

Dummy node = never lose the head reference.
Use it whenever building or modifying a list.

### Slow/Fast Pointers

```python
slow = head
fast = head

while fast and fast.next:
    slow = slow.next
    fast = fast.next.next
```

Fast moves 2x → when fast ends → slow = middle.
Same pattern detects cycles, finds nth from end,
checks palindromes, reorders lists.

### Recursion

Every recursive function needs exactly 2 things:
1. BASE CASE → when to stop
2. RECURSIVE CASE → smaller problem

Hidden cost people forget:
Recursion = O(n) call stack space.
Iterative = O(1) space.
Same time. Different space.

---

## The Hardest Problem — LRU Cache

Design a cache that evicts the least recently
used item when full. Both get and put must be O(1).

The solution: two structures together.

```
dict              → O(1) key lookup
doubly linked list → O(1) order tracking

HEAD side = most recently used
TAIL side = least recently used

get → find in dict + move to HEAD
put → add to HEAD + evict TAIL if full
```

```python
def get(self, key):
    if key in self.cache:
        node = self.cache[key]
        self._remove(node)
        self._insert_front(node)
        return node.val
    return -1
```

The lesson: design problems always ask
"what needs to be O(1)?" — then pick
the right structure for each need.

---

## 14 Problems This Week

| Problem | Key Concept |
|---------|-------------|
| Reverse Linked List | Three pointer technique |
| Merge Two Sorted Lists | Dummy node pattern |
| Linked List Cycle | Slow/fast detection |
| Middle of Linked List | Slow/fast middle |
| Remove Nth From End | Gap technique |
| Reverse List Recursive | Base case + recursive |
| Merge Lists Recursive | Smaller subproblem |
| Flatten Multilevel List | Pointer manipulation |
| Linked List Cycle II | Floyd's phase 2 |
| Palindrome Linked List | Find middle + reverse + compare |
| Reorder List | Find middle + reverse + merge |
| Add Two Numbers | Carry + dummy node |
| Copy Random List | Two pass + dict mapping |
| LRU Cache | Dict + doubly linked list |

---

## What's Coming in Week 5

Binary Trees + Binary Search.

Trees are linked lists but with TWO next pointers.
Everything from Week 4 applies — plus recursion
becomes the natural way to traverse them.

57+ problems solved in 4 weeks.
All solutions on GitHub.

---

*Week 4 of a 10-week 80/20 DSA plan.*
*All solutions: https://github.com/faizurrahaman27*
*Daily updates: #100DaysOfDSA*
