# Week 2 of Learning DSA in Python: 3 Patterns That Solve 60% of Array Problems

**Tags:** python, dsa, beginners, algorithms, 100daysofcode

---

## Quick Recap — Where I Left Off

In Week 1 I built my toolkit:
set, dict, Counter, defaultdict — the data structures
that answer "what do I store?"

Week 2 was about patterns — the techniques that answer
"how do I move through the data?"

Together they form the complete framework for
solving array problems.

---

## The 3 Patterns I Learned

### Pattern 1 — Two Pointers

Place two pointers strategically and move them
toward each other. Same result as nested loops —
but O(n) instead of O(n²).

Three types:
- Opposite ends → sorted array pair problems
- Slow/fast → move elements in place
- Fix one + two pointers → triplet problems (3Sum)

The golden rule: **only works on sorted arrays.**
Sorted order gives the pointers direction.
Without sorting, they're blind.

```python
# Two Sum II — sorted array
L, R = 0, len(numbers) - 1
while L < R:
    total = numbers[L] + numbers[R]
    if total == target:
        return [L+1, R+1]
    elif total < target:
        L += 1
    else:
        R -= 1
```

### Pattern 2 — Sliding Window

A window is just two boundaries (L and R) on a
frozen array. The array never changes —
you just move the frame.

Two types:
- Fixed size k → slide across maintaining size k
- Variable size → expand when condition met,
                  shrink when condition broken

```python
# Longest Substring Without Repeating Characters
seen = set()
L = 0
max_len = 0
for R in range(len(s)):
    while s[R] in seen:
        seen.remove(s[L])
        L += 1
    seen.add(s[R])
    max_len = max(max_len, R - L + 1)
```

The key insight: **R - L + 1 is the window size.**
Both endpoints included. Moving L or R just moves
the boundary — nothing is deleted.

### Pattern 3 — Prefix Sum

Precompute running totals once → answer any
range query in O(1).

```python
# Build prefix
prefix = [0] * (n + 1)
for i in range(1, n + 1):
    prefix[i] = prefix[i-1] + nums[i-1]

# Answer any range query
sum(L, R) = prefix[R+1] - prefix[L]
```

Combined with a dict → Subarray Sum = K
becomes O(n) instead of O(n²).

---

## The Mistake That Taught Me The Most

3Sum — I tried to solve it with Counter
and sliding window. Both completely wrong.

The lesson:

**Never pick a tool before understanding
what the problem is actually asking.**

The right order:
1. Understand the problem
2. Ask "what question am I answering?"
3. THEN pick tool and pattern

I was doing step 3 before step 1. That's
why I kept getting stuck.

---

## The Framework — Tools + Patterns

```
Every problem = Tool + Pattern

Tool    → "what to store?"
Pattern → "how to move through the data?"

set          → membership check
dict         → key-value lookup
Counter      → frequency counting
defaultdict  → grouping

two pointers → pairs in sorted array
sliding win  → best/longest/shortest subarray
prefix sum   → range sum queries
```

---

## 13 Problems This Week

| Problem | Tool | Pattern |
|---------|------|---------|
| Two Sum II | variables | two pointers |
| Valid Palindrome | variables | two pointers |
| 3Sum | variables | fix + two pointers |
| Max Average Subarray | variables | fixed window |
| Longest Substring | set | variable window |
| Range Sum Query | list | prefix sum |
| Subarray Sum = K | dict | prefix sum |
| Product Except Self | list | prefix sum (×) |
| Min Size Subarray | variables | variable window |
| Valid Palindrome II | variables | two pointers |
| Char Replacement | Counter | variable window |
| Max Vowels | set | fixed window |
| Continuous Subarray | dict | prefix sum |

---

## What's Coming in Week 3

Stacks, Queues, and the Monotonic Stack pattern.

These unlock a whole new family of problems —
"next greater element", bracket matching,
and temperature problems.

29+ problems solved in 2 weeks.
All solutions on GitHub below.

---

*Week 2 of a 10-week 80/20 DSA plan.*
*All solutions: https://github.com/faizurrahaman27*
*Daily updates: #100DaysOfDSA*
