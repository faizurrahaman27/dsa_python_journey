# Week 6 of Learning DSA in Python: Sorting & Heaps — Foundation Complete

**Tags:** python, dsa, beginners, algorithms, 100daysofcode

---

## The Final Foundation Week

Week 1 → Tools
Week 2 → Patterns
Week 3 → Structures
Week 4 → Linked Lists + Recursion
Week 5 → Trees + Binary Search
Week 6 → Sorting + Heaps ← THIS WEEK

After Week 6 → Graphs, DP, Tries (advanced territory).
This was the last week of foundations.
It had to be owned completely.

---

## What I Learned

### Merge Sort — Divide and Conquer

```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left  = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i]); i += 1
        else:
            result.append(right[j]); j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result

# Time: O(n log n) ALWAYS · Space: O(n)
```

The key: merge sort is GUARANTEED O(n log n).
Quick sort can degrade to O(n²).
For interviews → merge sort is safer.

### Heap — Hospital Emergency Room

```python
import heapq

# Min heap — smallest always at top
heap = []
heapq.heappush(heap, 3)
heapq.heappush(heap, 1)
heapq.heappush(heap, 4)
print(heap[0])          # 1 — peek min O(1)
heapq.heappop(heap)     # remove min O(log n)

# Max heap — negate values!
max_heap = []
heapq.heappush(max_heap, -5)
max_val = -heapq.heappop(max_heap)  # 5
```

### Top-K Pattern

K largest → MIN heap of size K.
Counterintuitive but correct:
Keep K largest by removing smallest.
heap[0] = Kth largest always.

```python
for num in nums:
    heapq.heappush(heap, num)
    if len(heap) > k:
        heapq.heappop(heap)   # remove smallest
return heap[0]                # Kth largest
```

### Two Heaps — Median Stream

```python
# small = max heap (lower half) → negate!
# large = min heap (upper half)
# Balance sizes → median in O(1)

def findMedian(self):
    if len(self.small) > len(self.large):
        return -self.small[0]
    return (-self.small[0] + self.large[0]) / 2
```

### Interval Golden Rule

**ALWAYS sort by start time first.**
No exceptions. Then check overlap:
next.start <= prev.end → overlap!

```python
intervals.sort(key=lambda x: x[0])
# Exception: non-overlapping → sort by END
```

---

## The Hardest Problems This Week

### Find Median From Data Stream (Hard)
Two heaps working together.
Small heap = lower half (max heap).
Large heap = upper half (min heap).
Balance sizes → median always O(1).

### Sliding Window Maximum (Hard)
Monotonic deque from Week 3
applied to sliding window.
Store indices, not values.
Front = current window maximum.
O(n) — each element in and out once.

### IPO (Hard)
Min heap unlocks affordable projects.
Max heap picks most profitable.
Two heaps working together.

---

## The Biggest Insight

Everything connects:

```
Week 3 monotonic stack
→ Week 6 monotonic deque
→ Same idea, different structure

Week 2 prefix sum
→ Week 6 car pooling (difference array)
→ Same pattern, different application

Week 4 recursion
→ Week 5 tree traversal
→ Week 6 merge sort
→ Same divide-and-conquer thinking
```

Tools + Patterns don't exist in isolation.
They combine. They build on each other.
That's why the order matters.

---

## The Mental Framework

After 6 weeks and 84+ problems,
I built a complete mental framework:

9 layers covering:
→ Analogy bank (remember by feeling)
→ Decision engine (tool + pattern instantly)
→ One-line rules (solve instantly)
→ 5 step process (never skip)
→ Problem patterns by feel
→ Common mistakes to never repeat
→ Complexity cheat sheet
→ All 80+ problems grouped by pattern
→ Daily 5-minute drill

Available in my GitHub repo.

---

## 12 Problems This Week

| Problem | Concept | Difficulty |
|---------|---------|------------|
| Sort an Array | Merge Sort | Medium |
| Sort Colors | Dutch National Flag | Medium |
| Merge Intervals | Sort + overlap | Medium |
| Kth Largest Element | Min heap size K | Medium |
| K Closest Points | Heap + distance | Medium |
| Task Scheduler | Frequency formula | Medium |
| Find Median Stream | Two heaps | Hard |
| Sliding Window Max | Monotonic deque | Hard |
| IPO | Two heaps greedy | Hard |
| Kth Largest Stream | Min heap design | Easy |
| Car Pooling | Difference array | Medium |
| Meeting Rooms | Sort + overlap | Easy |

---

## What's Coming — Week 7

Graphs.

The biggest mental shift yet.
Trees are graphs with one root.
Graphs have cycles, multiple components,
weighted edges.

BFS + DFS from Week 5 apply directly.
New patterns: topological sort,
Dijkstra's shortest path,
Union-Find for connectivity.

Must own Weeks 1-6 completely
before advancing.
Revision complete. Foundation locked.

84+ problems · 6 weeks · 42 days.
All solutions on GitHub.

---

*Week 6 of a 10-week 80/20 DSA plan.*
*All solutions: https://github.com/faizurrahaman27*
*Mental Framework PDF: https://github.com/faizurrahaman27*
*Daily updates: #100DaysOfDSA*
