# Week 3 of Learning DSA in Python: Stacks Changed How I Think

**Tags:** python, dsa, beginners, algorithms, 100daysofcode

---

## Quick Recap

Week 1 → Tools (set, dict, Counter)
Week 2 → Patterns (two pointers, sliding window, prefix sum)
Week 3 → New Structures (stack, queue, monotonic stack)

---

## What I Learned

### Stack — LIFO

Stack = plates. Last in, first out.

```python
stack = []
stack.append(x)   # push O(1)
stack.pop()       # pop  O(1)
stack[-1]         # peek O(1)
```

Use when: bracket matching, state saving,
undo operations, processing in reverse.

### Queue — FIFO

Queue = ticket counter. First in, first out.

```python
from collections import deque
queue = deque()
queue.append(x)    # enqueue O(1)
queue.popleft()    # dequeue O(1)
```

Never use list.pop(0) for a queue — it's O(n).
Always use deque.popleft() — O(1).

### Monotonic Stack

A stack where elements stay in order.
When new element breaks order → pop until restored.

```python
stack = []   # stores indices
for i in range(n):
    while stack and nums[i] > nums[stack[-1]]:
        idx = stack.pop()
        result[idx] = nums[i]   # found next greater!
    stack.append(i)
```

Key insight: store INDICES not values.
Indices give you both position AND value.

---

## The Problem That Taught Me The Most

Largest Rectangle in Histogram (LeetCode Hard).

I couldn't solve it alone. But working through
it step by step taught me something deeper:

When a bar gets POPPED from the monotonic stack:
  → it found its RIGHT boundary (current i)
  → its LEFT boundary = new stack top
  → width = right - left - 1
  → area = height × width

Every element pushed and popped exactly once
→ O(n) total. Elegant.

---

## The Biggest Non-Technical Lesson

I Googled a solution on Challenge Day.

Then admitted it. Then solved it properly.

The lesson:
Discomfort of not knowing = learning happening.
Googling removes the discomfort AND the learning.

New rule: Paper trace first. Code second.
If stuck → back to paper. Never Google first.

---

## The Mental Framework I Built

After 3 weeks I built a framework to lock
everything into my head permanently:

3 Questions for every problem:
1. What am I STORING?   → picks the tool
2. How am I MOVING?     → picks the pattern
3. Time + Space cost?   → states complexity

7 tools. 9 patterns. 5 step process.
Daily 5-minute drill every morning.

Full framework in my GitHub repo.

---

## 14 Problems This Week

| Problem | Difficulty | Key Concept |
|---------|------------|-------------|
| Valid Parentheses | Easy | Stack bracket matching |
| Queue Using Stacks | Easy | Two stacks = one queue |
| Daily Temperatures | Medium | Monotonic stack |
| Next Greater Element | Easy | Monotonic stack + dict |
| Min Stack | Medium | Two stacks in sync |
| Decode String | Medium | Stack state saving |
| Find All Anagrams | Medium | Counter + sliding window |
| Four Sum II | Medium | Counter + complement |
| Majority Element | Easy | Boyer-Moore voting |
| Longest Consecutive | Medium | Set O(1) membership |
| Asteroid Collision | Medium | Stack collision logic |
| Top K Frequent Words | Medium | Counter + tuple sort |
| Largest Rectangle | Hard | Monotonic stack |
| Make String Great | Easy | Stack bad pair removal |

---

## What's Coming in Week 4

Linked Lists + Recursion.

The mental shift from arrays to linked lists
is significant — no more index access.
Everything becomes pointer manipulation.

43+ problems solved in 3 weeks.
All solutions on GitHub.

---

*Week 3 of a 10-week 80/20 DSA plan.*
*All solutions: (https://github.com/faizurrahaman27)
*Daily updates: #100DaysOfDSA*
