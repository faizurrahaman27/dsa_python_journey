# 🗺️ My DSA Journey — Day by Day
# 42 Days · 6 Weeks · 84+ Problems · Complete Foundation

---

## 📅 WEEK 1 — TOOLS (Days 1-7)
> "Give a man the right tools and he can solve anything"

---

### Day 1 — Big-O + Lists + Dicts

**What I learned:**
Big-O = how my algorithm slows down as input grows.
Not about exact speed — about GROWTH RATE.

**The xy graph visualization:**
```
iterations
    |         O(n²)  ← quadratic (nested loops)
    |       /
    |      /  O(n)   ← linear (single loop)
    |    /
    |   / O(log n)   ← logarithmic (binary search)
    |  /___________
    | O(1)           ← constant (dict lookup)
    |________________________
                        input size (n)
```

**The Rules:**
```
Single loop          → O(n)
Two nested loops     → O(n²)
Two separate loops   → O(n)   ← NOT O(n²)!
Binary search        → O(log n)
Sort                 → O(n log n)
Hash map operation   → O(1)
```

**Why trade space for time?**
```
Brute force: check every pair → O(n²) time, O(1) space
Dict approach: store + lookup  → O(n) time,  O(n) space

Time is more expensive than space in interviews.
Always trade space for time.
```

**Problems solved:**
- Two Sum → dict complement lookup
- Contains Duplicate → set membership

---

### Day 2 — Set + Dict + Counter + defaultdict

**The Analogy Bank (locked in today):**
```
SET         → Bouncer's stamp log
              "Have I seen this face before?"
              YES or NO. Nothing else.
              Membership check O(1)

DICT        → Phone book
              "Give me Ravi's number"
              Key → Value. Direct lookup O(1)

COUNTER     → Tally chart
              "How many times did this appear?"
              Counter('aab') = {'a':2, 'b':1}

DEFAULTDICT → Phone book that auto-creates pages
              Never throws KeyError
              defaultdict(list) for grouping
```

**When to use which:**
```
"Have I seen this?"          → SET
"What's stored at this key?" → DICT
"How many times?"            → COUNTER
"Group under shared key?"    → DEFAULTDICT
```

**Visual — how dict works:**
```
Two Sum: [2,7,11,15], target=9

seen = {}

num=2: complement=7, 7 in seen? NO → seen={2:0}
num=7: complement=2, 2 in seen? YES → return [0,1] ✅

Key insight: store what you've SEEN
             look for what you NEED
```

**Problems solved:**
- Valid Anagram → Counter comparison
- First Unique Character → Counter + loop
- Group Anagrams → defaultdict(list) + sorted key
- Ransom Note → Counter subtraction

---

### Day 3 — Hashing Internals + In-place Algorithms

**How hashing actually works:**
```
hash('apple') → some_number → index in array
                              → O(1) lookup!

Collision: two keys → same index
Python handles with chaining.
Worst case O(n) but average O(1).
```

**In-place = modify without extra space:**
```
Two pointers trick:

[0,1,0,3,12]  → move zeroes to end

slow=0, fast=0

fast scans, slow marks position for non-zero:
fast=0: nums[0]=0 → skip
fast=1: nums[1]=1 → swap(slow,fast) → slow++
fast=2: nums[2]=0 → skip
fast=3: nums[3]=3 → swap(slow,fast) → slow++
...

Result: [1,3,12,0,0] ✅ O(1) space!
```

**Problems solved:**
- Move Zeroes → two pointers in-place
- Remove Duplicates → slow/fast pointer
- Best Time to Buy Stock → track min price

---

### Day 4 — XOR + Bit Manipulation

**XOR magic:**
```
a XOR a = 0      (same number cancels)
a XOR 0 = a      (zero doesn't change)
XOR is commutative and associative

Single Number: [4,1,2,1,2]
4 XOR 1 XOR 2 XOR 1 XOR 2
= 4 XOR (1 XOR 1) XOR (2 XOR 2)
= 4 XOR 0 XOR 0
= 4 ✅
```

**Problems solved:**
- Single Number → XOR all elements
- Intersection of Arrays → set intersection

---

### Day 5 — Top K + Sorting by Key

**Sorting by custom key:**
```python
# Sort words by frequency then alphabet
sorted(freq.keys(),
       key=lambda word: (-freq[word], word))

# Tuple comparison:
(-2, "i")    ← comes first (higher freq)
(-2, "love") ← comes second (same freq, alphabet)
(-1, "coding")
```

**Problems solved:**
- Top K Frequent Elements → Counter + sort
- Top K Frequent Words → tuple sort (-freq, word)

---

### Day 6 — Review + Patterns Recognition

**The 3 Questions (locked in today):**
```
Q1. What am I STORING?    → picks the TOOL
Q2. How am I MOVING?      → picks the PATTERN
Q3. Time + Space cost?    → states COMPLEXITY

Never skip these 3. Ever.
```

---

### Day 7 — Publish Week 1

**Week 1 Summary:**
```
8 Tools learned:
  set, dict, Counter, defaultdict,
  list, XOR trick, sorting by key, tuple sort

Key insight of the week:
  Trade SPACE for TIME using dict/set
  O(n²) brute force → O(n) with hash map
```

---

## 📅 WEEK 2 — PATTERNS (Days 8-14)
> "Tools + Patterns = solve anything"

---

### Day 8 — Two Pointers (3 Types)

**Analogy: Two fingers on a frozen array**
```
Array never changes.
Just two fingers moving on it.
```

**Type 1 — Opposite ends (sorted array):**
```
[1, 2, 3, 4, 5, 6], target=7

L=0, R=5
nums[L]+nums[R] = 1+6 = 7 ✅ found!

If sum > target → R--  (need smaller)
If sum < target → L++  (need larger)
If sum == target → found!
```

**Type 2 — Slow/Fast (same direction):**
```
Move zeroes: slow marks position, fast scans
Remove duplicates: slow=last unique, fast scans
```

**Type 3 — Fix one + two pointers (3Sum):**
```
Fix nums[i], then L/R on rest
O(n²) instead of O(n³)
```

**Problems solved:**
- Two Sum II → opposite ends
- Valid Palindrome → L and R meeting middle
- Valid Palindrome II → try removing one char
- 3Sum → fix + two pointers

---

### Day 9 — Fixed Sliding Window

**Analogy: Cardboard frame over frozen array**
```
L and R are just boundaries.
Array NEVER changes.
Frame MOVES.

[1, 3, -1, -3, 5, 3]
 |_____|               ← window of size 3
    |_____|            ← slide right
       |_____|         ← slide right
```

**The template:**
```python
# Fixed window of size k
window_sum = sum(nums[:k])
max_sum = window_sum

for i in range(k, len(nums)):
    window_sum += nums[i]        # add new element
    window_sum -= nums[i - k]   # remove old element
    max_sum = max(max_sum, window_sum)

# Window size = R - L + 1 (both endpoints included)
```

**Problems solved:**
- Max Average Subarray → fixed window
- Find All Anagrams → fixed window + Counter

---

### Day 10 — Variable Sliding Window

**Fixed vs Variable:**
```
Fixed  → "of size k", "of length k" → window stays same size
Variable → "longest", "shortest", "at most k" → window grows/shrinks
```

**The template:**
```python
L = 0
for R in range(len(s)):
    # expand window
    window.add(s[R])

    # shrink when condition broken
    while window is invalid:
        window.remove(s[L])
        L += 1

    # update answer
    result = max(result, R - L + 1)
```

**Problems solved:**
- Longest Substring No Repeat → set + shrink when duplicate
- Longest Repeating Char Replace → shrink when invalid
- Min Size Subarray Sum → shrink when sum >= target

---

### Day 11 — Prefix Sum

**Analogy: Car odometer**
```
Never resets. Accumulates.
Distance from A to B =
  odometer_at_B - odometer_at_A

prefix = [0, 1, 4, 9, 16]
         ↑
      extra 0 at start (makes formula clean)

Sum from index L to R:
  prefix[R+1] - prefix[L]
  O(1) query after O(n) build!
```

**Visual:**
```
nums   = [1, 3, 5, 7]
prefix = [0, 1, 4, 9, 16]

Sum from index 1 to 2 (nums[1]+nums[2] = 3+5 = 8):
  prefix[3] - prefix[1] = 9 - 1 = 8 ✅
```

**Subarray Sum = K (prefix + dict):**
```python
# count subarrays summing to k
count = 0
prefix_sum = 0
seen = {0: 1}     # empty subarray

for num in nums:
    prefix_sum += num
    count += seen.get(prefix_sum - k, 0)
    seen[prefix_sum] = seen.get(prefix_sum, 0) + 1
```

**Problems solved:**
- Range Sum Query → prefix array
- Subarray Sum = K → prefix + dict
- Product Except Self → prefix + suffix products

---

### Day 12-13 — Mixed Patterns

**Problems solved:**
- Continuous Subarray Sum → prefix + dict
- Max Vowels → fixed sliding window
- 3Sum → fix + two pointers

---

### Day 14 — Publish Week 2

**Week 2 Summary:**
```
3 Patterns learned:
  Two Pointers   → pairs, palindromes, sorted
  Sliding Window → best subarray problems
  Prefix Sum     → range queries O(1)

Key formula locked in:
  R - L + 1 = window size
  prefix[R+1] - prefix[L] = range sum
```

---

## 📅 WEEK 3 — STRUCTURES (Days 15-21)
> "Stack = plates. Queue = tickets. Mono Stack = waiting room."

---

### Day 15 — Stack (LIFO)

**Analogy: Plates on a table**
```
Last plate placed = First plate taken
LIFO = Last In First Out

push → place plate on top
pop  → take plate from top
peek → look at top plate (stack[-1])

When to use:
  → matching brackets
  → undo operations
  → saving state before going deeper
```

**Valid Parentheses visual:**
```
"({[]})"

char='(' → push  stack=['(']
char='{' → push  stack=['(', '{']
char='[' → push  stack=['(', '{', '[']
char=']' → match '[' → pop  stack=['(', '{']
char='}' → match '{' → pop  stack=['(']
char=')' → match '(' → pop  stack=[]

stack empty → True ✅
```

**Problems solved:**
- Valid Parentheses → stack matching
- Min Stack → two stacks in sync
- Decode String → stack saves state at '['

---

### Day 16 — Queue (FIFO) + Monotonic Stack

**Queue Analogy: Ticket counter**
```
First person in line = First served
FIFO = First In First Out

from collections import deque
queue = deque()
queue.append(x)    # enqueue O(1)
queue.popleft()    # dequeue O(1)

NEVER use list.pop(0) → O(n)!
ALWAYS use deque.popleft() → O(1)!
```

**Monotonic Stack Analogy: Waiting room**
```
Each person waits for their answer.
New taller person arrives →
everyone shorter behind them
gets their answer (pop them)!

Daily Temperatures: [73,74,75,71,69,72,76,73]

For each temp, find days until warmer:

Stack stores INDICES (not values!)
Why indices? Need position to calculate distance.

73 pushed → stack=[0]
74 arrives: 74>73 → 73 found answer! pop, distance=1-0=1
            push 74 → stack=[1]
75 arrives: 75>74 → 74 found answer! distance=2-1=1
            push 75 → stack=[2]
71 arrives: 71<75 → push → stack=[2,3]
...
```

**Why O(n) despite while loop?**
```
Each element pushed ONCE → n pushes total
Each element popped ONCE → n pops total
Total = 2n = O(n)

The while loop doesn't multiply —
it just does the pops that were
already counted!
```

**Problems solved:**
- Daily Temperatures → mono stack decreasing
- Next Greater Element → mono stack + dict
- Asteroid Collision → stack collision logic

---

### Day 17 — Advanced Stack Problems

**Largest Rectangle in Histogram:**
```
When a bar gets POPPED:
  → found its RIGHT boundary (current i)
  → LEFT boundary = new stack top
  → width = right - left - 1
  → area = height × width

heights = [2,1,5,6,2,3]

Always store INDICES!
Pop when heights[i] < heights[stack[-1]]
```

**Problems solved:**
- Largest Rectangle → monotonic stack (Hard)
- Make String Great → stack bad pair removal
- Top K Frequent Words → Counter + tuple sort

---

### Day 18-20 — Review + Challenge Day

**The Paper First Rule (established Day 19):**
```
BEFORE: read → open editor → code → stuck → Google
AFTER:  read → paper → trace → understand → code

Paper trace first. Code second. ALWAYS.
If stuck → back to paper. Never Google first.
```

**Problems solved:**
- Four Sum II → Counter complement
- Majority Element → Boyer-Moore voting
- Longest Consecutive → set + counting

---

### Day 21 — Publish Week 3

**Week 3 Summary:**
```
3 Structures learned:
  Stack      → LIFO, brackets, state
  Queue      → FIFO, BFS, level order
  Mono Stack → next greater/smaller O(n)

Biggest lesson:
  Paper trace first. Code second.
  The discomfort of not knowing
  IS the learning happening.
```

---

## 📅 WEEK 4 — LINKED LISTS + RECURSION (Days 22-28)
> "Treasure hunt — each clue points to next"

---

### Day 22 — Linked List Structure + Traversal

**The Mental Shift:**
```
Array:
  [1, 2, 3, 4, 5]
   ↑  ↑  ↑  ↑  ↑
   direct index access O(1)

Linked List:
  1 → 2 → 3 → 4 → 5 → None
  must traverse from HEAD
  no jumping → O(n) access
```

**The Node:**
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val  = val    # the data
        self.next = None   # pointer to next node

# Tree has TWO pointers:
class TreeNode:
    self.left  = None
    self.right = None
```

**Traversal:**
```python
current = head
while current:
    print(current.val)
    current = current.next
# NEVER current.next on None → AttributeError!
```

**Three Pointer Reverse:**
```
1 → 2 → 3 → None

prev=None, curr=1

Step 1: save=2, curr.next=None, prev=1, curr=2
        1 → None
Step 2: save=3, curr.next=1, prev=2, curr=3
        2 → 1 → None
Step 3: save=None, curr.next=2, prev=3, curr=None
        3 → 2 → 1 → None

return prev (=3) ✅
```

**Dummy Node Pattern:**
```python
dummy = ListNode(0)    # stable anchor
current = dummy

# build result...

return dummy.next      # skip dummy, return real head

# Why dummy?
# Without: head might change, lots of edge cases
# With: head is just another node, clean code
```

**Problems solved:**
- Reverse Linked List → three pointers
- Merge Two Sorted Lists → dummy node

---

### Day 23 — Slow/Fast Pointers

**Analogy: Two runners on a circular track**
```
Slow → 1 step per second
Fast → 2 steps per second

No cycle: fast reaches end
Cycle: fast laps slow → they MEET!
```

**Finding Middle:**
```
1 → 2 → 3 → 4 → 5

slow=1, fast=1

Step 1: slow=2, fast=3
Step 2: slow=3, fast=5
        fast.next=None → stop

slow = 3 = middle ✅

Template:
while fast and fast.next:
    slow = slow.next
    fast = fast.next.next
```

**Gap Technique (Remove Nth From End):**
```
1 → 2 → 3 → 4 → 5,  n=2

Move fast n=2 steps ahead:
  fast = node(3)

Move both until fast.next=None:
  slow=2, fast=4
  slow=3, fast=5  → fast.next=None → stop

slow.next = slow.next.next
→ skips node(4)
→ 1 → 2 → 3 → 5 ✅
```

**Problems solved:**
- Linked List Cycle → slow/fast meet
- Middle of Linked List → slow at middle
- Remove Nth From End → gap technique

---

### Day 24 — Recursion

**Analogy: Standing in a queue**
```
"What position am I in?"
Ask person ahead.
They ask person ahead.
...until first person says "I'm #1"
Answer travels BACK.

That's recursion!
```

**Two Parts — Always:**
```
1. BASE CASE → when to STOP
   "I'm the first person → return 1"

2. RECURSIVE CASE → smaller problem
   "My position = ahead_position + 1"
```

**The Hidden Cost:**
```
Each recursive call = stack frame in memory
n calls = O(n) space

Iterative → O(1) space ✅
Recursive → O(n) space (hidden!)
Same time. Different space. Know both!
```

**Recursion Tree (fibonacci):**
```
fib(4):
          fib(4)
         /      \
      fib(3)   fib(2)
      /    \   /    \
  fib(2) fib(1) fib(1) fib(0)
  /    \
fib(1) fib(0)

fib(2) calculated TWICE!
fib(1) calculated THREE times!
→ Why memoization exists (Week 8)
```

**Problems solved:**
- Reverse List Recursive → base + recursive
- Merge Lists Recursive → smaller subproblem
- Flatten Multilevel List → pointer manipulation

---

### Day 25 — Slow/Fast Pointers Deeper

**Floyd's Cycle Detection (Full):**
```
Phase 1: Detect meeting point
  slow moves 1 step
  fast moves 2 steps
  They meet → cycle exists

Phase 2: Find cycle START
  Reset slow to HEAD
  Keep fast at MEETING POINT
  Move BOTH 1 step
  They meet → CYCLE START!

Math: F = C - a
  (distance head to cycle start
   = distance meeting to cycle start)
```

**Palindrome Linked List (3 steps):**
```
1 → 2 → 2 → 1

Step 1: Find middle (slow/fast)
        middle = node(2) [second]

Step 2: Reverse second half
        2 → 1 becomes 1 → 2

Step 3: Compare both halves
        1==1 ✅, 2==2 ✅ → True
```

**Problems solved:**
- Linked List Cycle II → Floyd phase 2
- Palindrome Linked List → 3 steps
- Reorder List → find middle + reverse + merge

---

### Day 26 — Challenge Day

**Add Two Numbers:**
```
342 + 465 = 807
stored as: 2→4→3 and 5→6→4
result:    7→0→8

Key: carry = total // 10
     digit = total % 10
     while l1 or l2 or carry (don't miss carry!)
```

**Copy List with Random Pointer:**
```
Two pass approach:
Pass 1: create all new nodes
        old_to_new = {old: Node(old.val)}

Pass 2: connect next and random
        new.next   = old_to_new[old.next]
        new.random = old_to_new[old.random]
```

**LRU Cache (the design problem):**
```
Two structures:
  dict          → O(1) key lookup
  doubly linked list → O(1) order tracking

HEAD = most recently used
TAIL = least recently used

get: find → move to HEAD
put: add to HEAD → evict TAIL if full

_remove(node): disconnect from list
_insert_front(node): connect after HEAD
```

---

### Day 27-28 — Review + Publish Week 4

**Week 4 Summary:**
```
14 problems solved
Key techniques:
  Three pointer reverse
  Dummy node pattern
  Slow/fast pointers
  Floyd's algorithm
  Recursion (hidden O(n) space!)
  LRU Cache design
```

---

## 📅 WEEK 5 — TREES + BINARY SEARCH (Days 29-35)
> "Recursion from Week 4 = natural tree traversal"

---

### Day 29 — Binary Tree + DFS

**Tree Node (linked list + 1 pointer):**
```python
class TreeNode:
    def __init__(self, val=0):
        self.val   = val
        self.left  = None   # TWO pointers!
        self.right = None
```

**DFS Three Types:**
```
        1
       / \
      2   3
     / \
    4   5

Preorder  (root first):  1, 2, 4, 5, 3
Inorder   (root middle): 4, 2, 5, 1, 3
Postorder (root last):   4, 5, 2, 3, 1

Just move where you process the node:
```

**The Universal Tree Template:**
```python
def solve(node):
    if not node:           # base case
        return base_value

    left  = solve(node.left)   # go left
    right = solve(node.right)  # go right

    return combine(left, right)  # combine

# This template solved:
# Max Depth, Invert Tree, Same Tree,
# Path Sum, Balanced Tree, Max Path Sum
```

**Problems solved:**
- Max Depth → 1 + max(left, right)
- Invert Tree → swap left/right + recurse
- Same Tree → check both subtrees match

---

### Day 30 — BFS + Level Order

**BFS Analogy: Going wide not deep**
```
DFS → go DEEP first (stack/recursion)
BFS → go WIDE first (queue)

        1
       / \
      2   3
     / \
    4   5

DFS: 1,2,4,5,3  (goes all way down left)
BFS: 1,2,3,4,5  (level by level)
```

**BFS Template:**
```python
from collections import deque

queue = deque([root])
while queue:
    level_size = len(queue)    # FREEZE level size!
    level = []

    for _ in range(level_size):
        node = queue.popleft()
        level.append(node.val)
        if node.left:  queue.append(node.left)
        if node.right: queue.append(node.right)

    result.append(level)

# len(queue) at START of loop
# = exact nodes in current level
```

**BFS Superpower:**
```
First leaf BFS finds = shallowest leaf
= minimum depth!

DFS must visit ALL leaves to find minimum.
BFS stops at FIRST leaf found. ✅
```

**Problems solved:**
- Level Order Traversal → BFS template
- Right Side View → last node each level
- Minimum Depth → BFS stops at first leaf

---

### Day 31 — Binary Search Tree

**BST Property:**
```
For EVERY node:
  ALL left subtree  < node.val
  ALL right subtree > node.val

        8
       / \
      3   10
     / \    \
    1   6    14

Search 6:
  8 > 6 → go LEFT
  3 < 6 → go RIGHT
  found! O(log n) ✅
```

**BST Superpower — Inorder = Sorted:**
```
Inorder: left → root → right
BST:     left < root < right
→ naturally sorted! ✅

Used for: Kth Smallest without sorting
```

**Validate BST (tricky part):**
```
Just checking children is WRONG!

    5
   / \
  1   7
     / \
    4   8

Node 7 looks valid locally.
But 4 < 5! → invalid!

Must pass min/max boundaries:
validate(node, min_val, max_val)
  if node.val <= min_val or node.val >= max_val:
      return False
```

**Problems solved:**
- Validate BST → min/max boundaries
- LCA of BST → split point = ancestor
- Kth Smallest → inorder = sorted

---

### Day 32 — Binary Search

**Analogy: Finding word in dictionary**
```
1000 pages, find "monkey":
  Open page 500 → "lion"
  monkey > lion → right half
  Open page 750 → "rabbit"
  monkey < rabbit → left half
  Open page 625 → "monkey" ✅

1000 pages → ~10 steps
log₂(1000) ≈ 10
```

**The Template:**
```python
left, right = 0, len(nums) - 1

while left <= right:    # <= NOT <
    mid = left + (right - left) // 2

    if nums[mid] == target:  return mid
    elif nums[mid] < target: left = mid + 1
    else:                    right = mid - 1

return -1
```

**Why left <= right not left < right:**
```
nums=[5], target=5

With left <= right:
  0 <= 0 → TRUE → enters loop → finds 5 ✅

With left < right:
  0 < 0 → FALSE → never runs → returns -1 ❌

Single element case where left==right!
```

**Rotated Array Insight:**
```
[4,5,6,7,0,1,2]

ONE half always sorted!

If nums[left] <= nums[mid]:
  → left half sorted
  → check if target in [nums[left], nums[mid])
  → if yes → search left, else → search right

If nums[mid] <= nums[right]:
  → right half sorted
  → check if target in (nums[mid], nums[right]]
  → if yes → search right, else → search left
```

**Problems solved:**
- Binary Search → classic template
- Search Rotated Array → one half sorted
- Find Minimum Rotated → compare mid to right

---

### Day 33 — Challenge Day (Trees)

**Path Sum:**
```
targetSum -= node.val at each level
Leaf + targetSum==0 → True!

Base cases:
  not node → False
  leaf + sum==0 → True
```

**Balanced Binary Tree (-1 signal):**
```
-1 = special signal meaning "unbalanced"

height(node):
  if not node: return 0
  left = height(node.left)
  right = height(node.right)
  if left==-1 or right==-1: return -1  (propagate)
  if abs(left-right) > 1: return -1    (unbalanced)
  return 1 + max(left, right)

return height(root) != -1
```

**Max Path Sum (Hard):**
```
Key insight:
  left_gain = max(0, solve(left))   ← never include negatives!
  right_gain = max(0, solve(right))

Two calculations at each node:
  path = left + node + right → update global max
  return = node + max(left, right) → go up ONE direction
```

---

### Day 34-35 — Review + Publish Week 5

**Week 5 Summary:**
```
15 problems solved
Key techniques:
  Tree recursion template (1 template, 6 problems!)
  BFS level order (freeze len(queue)!)
  BST min/max boundary validation
  Binary search left <= right rule
  max(0, subtree) for negative paths
```

---

## 📅 WEEK 6 — SORTING + HEAPS (Days 36-42)
> "Final foundation week — everything connects here"

---

### Day 36 — Sorting Algorithms

**Merge Sort — Divide and Conquer:**
```
[8,3,1,5,2,7]

Split:    [8,3,1]    [5,2,7]
Split:  [8][3,1]  [5][2,7]
Split: [8][3][1] [5][2][7]

Merge: [3,8][1] → [1,3,8]   [2,5][7] → [2,5,7]
Merge: [1,3,8] + [2,5,7] → [1,2,3,5,7,8] ✅

Time: O(n log n) ALWAYS
Space: O(n)
```

**Quick Sort — Pivot:**
```
Pick last element as pivot.
Smaller elements → left of pivot.
Larger elements → right of pivot.
Pivot is now in CORRECT position!
Recursively sort left and right.

Time: O(n log n) average, O(n²) worst
Space: O(log n)
```

**Dutch National Flag (Sort Colors):**
```
Three pointers: low, mid, high
0 → swap with low, low++, mid++
1 → mid++
2 → swap with high, high--

O(n) time, O(1) space ✅
```

**Merge Intervals:**
```
SORT BY START FIRST!

[[1,3],[2,6],[8,10],[15,18]]
After sort: [[1,3],[2,6],[8,10],[15,18]]

[2,6]: 2 <= 3 → overlap! merge → [1,6]
[8,10]: 8 > 6 → new interval
[15,18]: 15 > 10 → new interval

Result: [[1,6],[8,10],[15,18]] ✅
```

**Problems solved:**
- Sort an Array → merge sort implementation
- Sort Colors → Dutch national flag
- Merge Intervals → sort + overlap check

---

### Day 37 — Heap + Priority Queue

**Analogy: Hospital Emergency Room**
```
Patients arrive at different times.
Most CRITICAL patient treated first.
New critical patient → jumps to front.

Min Heap → least critical first (smallest)
Max Heap → most critical first (largest)
```

**Python heapq (MIN heap only):**
```python
import heapq

heap = []
heapq.heappush(heap, 3)    # O(log n)
heapq.heappush(heap, 1)
heapq.heappush(heap, 4)

print(heap[0])              # peek min = 1, O(1)
heapq.heappop(heap)         # remove min, O(log n)

# MAX HEAP → negate values!
heapq.heappush(heap, -5)
max_val = -heapq.heappop(heap)   # = 5
```

**Top-K Pattern:**
```
K LARGEST → MIN heap of size K

Why MIN heap for K LARGEST?
  Keep K largest by removing SMALLEST.
  When heap > K → pop smallest.
  heap[0] = smallest of top K = Kth largest!

Visual with k=3, nums=[3,1,4,1,5,9,2,6]:
  push 3 → [3]
  push 1 → [1,3]
  push 4 → [1,3,4]  size=k
  push 1 → [1,1,3,4] size>k → pop 1 → [1,3,4]
  push 5 → [1,3,4,5] size>k → pop 1 → [3,4,5]
  push 9 → [3,4,5,9] size>k → pop 3 → [4,5,9]
  push 2 → [2,4,5,9] size>k → pop 2 → [4,5,9]
  push 6 → [4,5,6,9] size>k → pop 4 → [5,6,9]

heap[0] = 5 = 3rd largest ✅
```

**Problems solved:**
- Kth Largest Element → min heap size K
- K Closest Points → heap + x²+y² distance
- Task Scheduler → frequency formula

---

### Day 38 — Two Heaps + Hard Problems

**Two Heap Pattern (Median Stream):**
```
Analogy: Two airport queues
  small = max heap (lower half, negate values)
  large = min heap (upper half)

Numbers: [1, 2, 3, 4, 5]

small (max heap): [1, 2]  → top = 2
large (min heap): [3,4,5] → top = 3

Median = (2 + 3) / 2 = 2.5 ✅

Balance rule:
  sizes differ by more than 1 → rebalance
  top of small > top of large → rebalance
```

**Sliding Window Maximum:**
```
Monotonic DEQUE (decreasing values, stores indices)

For each element:
  Remove indices outside window from front
  Remove smaller elements from back
  Append current index
  Front = current window maximum

O(n) — each element enters and exits deque once!
```

**Problems solved:**
- Find Median From Stream → two heaps
- Sliding Window Maximum → monotonic deque
- IPO → two heaps greedy

---

### Day 39 — Interval Problems + Challenge Day

**Insert Interval (3 phases):**
```
Phase 1: add intervals that END before new starts
Phase 2: merge all overlapping intervals
Phase 3: add remaining intervals

Overlap condition: intervals[i][0] <= newInterval[1]
```

**Non-overlapping Intervals:**
```
SORT BY END TIME (exception to the rule!)

Keep interval with EARLIEST end.
When overlap → remove later ending one.
Greedy: earlier end = more room for future.
```

**Meeting Rooms II:**
```
Sort by start time.
Min heap stores END TIMES of rooms.

For each meeting:
  if heap[0] <= meeting.start:
    reuse that room (heapreplace)
  else:
    new room needed (heappush)

Heap size = rooms needed! ✅
```

**Car Pooling (Difference Array):**
```
This is PREFIX SUM from Week 2!

stops[start] += passengers   (pick up)
stops[end]   -= passengers   (drop off)

Walk stops, accumulate total.
If total > capacity → False!
```

**Problems solved:**
- Meeting Rooms → sort + overlap check
- Kth Largest Stream → min heap design
- Car Pooling → difference array

---

### Day 40-41 — Review + Mental Framework

**Built Complete Mental Framework:**
```
9 Layers:
  1. Analogy Bank
  2. Decision Engine
  3. One-Line Rules
  4. 5 Step Process
  5. Problem Patterns by Feel
  6. Common Mistakes
  7. Complexity Cheat Sheet
  8. 80+ Problems by Pattern
  9. Daily 5-Minute Drill
```

---

### Day 42 — Publish Week 6

**Week 6 + Foundation Summary:**
```
12 problems solved this week
84+ total problems
6 weeks complete

Everything connects:
  Week 3 mono stack → Week 6 mono deque
  Week 2 prefix sum → Week 6 car pooling
  Week 4 recursion  → Week 5 trees → Week 6 merge sort

Foundation = COMPLETE.
Ready for advanced territory.
```

---

## 🏆 FOUNDATION COMPLETE — WEEKS 1-6

```
WEEK 1 → 8 tools mastered
WEEK 2 → 3 patterns mastered
WEEK 3 → 3 structures mastered
WEEK 4 → 5 linked list techniques
WEEK 5 → 4 tree/search patterns
WEEK 6 → 4 sorting/heap patterns

TOTAL:
  84+ problems solved
  42 days consistent
  6 blog posts published
  GitHub repo live
  Twitter updates daily
  Mental Framework built

NEXT:
  Week 7  → Graphs
  Week 8  → Dynamic Programming
  Week 9  → Advanced Trees (Tries)
  Week 10 → Mastery + Interview Prep
```

---

*Generated from 42 days of learning · All solutions in /week-01 through /week-06*
*Mental Framework PDF in repo root*
*#100DaysOfDSA #Python #DSA*
