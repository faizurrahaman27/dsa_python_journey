# Week 1 of Learning DSA in Python: Big-O Finally Makes Sense

**Tags:** python, dsa, beginners, algorithms, 100daysofcode

---

## Why I'm Doing This

[2-3 sentences — why you started, what you want to achieve]

Example:
"I've been writing Python for some time but always avoided
Data Structures and Algorithms. I decided to learn it publicly —
every problem, every mistake, every breakthrough — so I stay
accountable and hopefully help someone else on the same journey."

---

## What Week 1 Covered

Following an 80/20 study plan — the 20% of DSA that solves
80% of real problems. Week 1 was pure foundations:

- Big-O notation — measuring algorithm efficiency
- Python's core structures — list, dict, set and their real costs
- Counter and defaultdict from collections
- In-place algorithms — solving with O(1) space
- Hashing internals — why dict lookup is O(1)

---

## The Concept That Changed Everything

Before this week, I thought fast code just meant "good code."

Big-O showed me the truth: it's about growth rate, not raw speed.

The difference between O(n) and O(n²) isn't noticeable at n=10.
At n=1,000,000 — one takes 1 second, the other takes 11 days.

The single most useful pattern I learned:

```python
# Question to always ask yourself:
# "Can I trade O(n) space for O(n) time?"

# Example — Two Sum:
# Brute force: O(n²) — check every pair
# Optimised:   O(n)  — store seen numbers in a dict

def two_sum(nums, target):
    seen = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
```

Swapping a list for a dict. That's it.
The whole trick. Works in dozens of problems.

---

## The Problem That Stumped Me Most

[Be honest here — this is what makes posts relatable]

Example:
"Best Time to Buy and Sell Stock looked simple but I stared
at it for 20 minutes. I kept thinking about indices and pairs.

The breakthrough: I don't need to track every pair.
I just need to track ONE thing — the minimum price seen so far.

```python
min_price = prices[0]
max_profit = 0

for price in prices:
    profit_today = price - min_price
    if profit_today > max_profit:
        max_profit = profit_today
    if price < min_price:
        min_price = price

return max_profit
# Time: O(n) · Space: O(1)
```

Two variables. One pass. Done."

---

## The Bonus Concept — XOR Bit Manipulation

This one genuinely surprised me.

Single Number problem: every number appears twice except one.
Find the lone number.

My first instinct: use a dict to count frequencies. O(n) space.

The optimal solution uses XOR:

```python
def single_number(nums):
    result = 0
    for num in nums:
        result ^= num    # pairs cancel, lone number survives
    return result

# Time: O(n) · Space: O(1) — no extra memory at all
```

The magic:
- a ^ a = 0  → same number XOR itself = 0 (pairs vanish)
- a ^ 0 = a  → anything XOR 0 survives

No dict. No set. Just one variable and math.

---

## 16 Problems in 7 Days

| Problem | Key Concept | Complexity |
|---------|-------------|------------|
| Two Sum | dict lookup | O(n) / O(n) |
| Single Number | XOR | O(n) / O(1) |
| Contains Duplicate | set | O(n) / O(n) |
| Valid Anagram | freq dict | O(n) / O(1) |
| Group Anagrams | defaultdict | O(nk log k) |
| Ransom Note | Counter | O(n+m) / O(1) |
| Best Time Stocks | one variable | O(n) / O(1) |
| Word Pattern | two dicts | O(n) / O(n) |
| Sort Array Parity | two pointers | O(n) / O(1) |
| + 7 more... | | |

---

## The Hardest Mental Shift

Stopping myself from jumping straight to code.

Every problem — I now force myself to:
1. Understand the problem in plain English
2. Answer: "what question am I actually trying to answer?"
3. Trace a small example on paper
4. THEN open the editor

This process alone cut my debugging time in half.

---

## What's Coming in Week 2

Two Pointers · Sliding Window · Prefix Sums

These three patterns solve around 30% of all array
problems on LeetCode. Can't wait.

---

## Follow Along

All 16 solutions with complexity analysis:
→ GitHub: https://github.com/faizurrahaman27

Daily updates:
→ Twitter/X: #100DaysOfDSA

Drop a comment if you're on the same journey.
Let's learn together. 🚀

---
*This is Week 1 of a 10-week 80/20 DSA study plan.*
