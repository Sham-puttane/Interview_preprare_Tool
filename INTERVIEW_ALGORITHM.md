# THE INTERVIEW ALGORITHM
### A Complete Pattern System for Data Scientist / AI Engineer / Data Engineer Interviews

> This is your single reference document. Every coding, SQL, or ML case-study problem runs through one of the three tracks in this file.

---

## Table of Contents

- [Part A — The Universal Problem-Solving Algorithm (UMPIRE+)](#part-a)
- [Part B — Read Constraints to Guess Complexity](#part-b)
- [Part C — The Pattern Recognition Decision Tree](#part-c)
- [Part D — The Full Pattern Library (20 Patterns)](#part-d)
- [Part E — SQL Pattern Track](#part-e)
- [Part F — ML / DS Case Study Track](#part-f)
- [Part G — The Meta-Algorithm: How to Actually Learn Patterns](#part-g)
- [Mental Model Summary](#summary)
- [Sources](#sources)

---

<a id="part-a"></a>
## Part A: The Universal Problem-Solving Algorithm (UMPIRE+)

This is the *meta-algorithm*. Every coding problem, every interview, runs through this exact sequence. Interviewers love it because it makes your thinking legible.

### U — Understand (3–5 min, do not skip)

Say out loud:
1. "Let me restate the problem in my own words…"
2. "What's the input type and size range?"
3. "What's the expected output?"
4. "Let me walk through an example with a small input."
5. "Edge cases: empty input, single element, duplicates, negatives, sorted, very large n, collisions, nulls?"

**Clarifying questions to ask (pick 2–3 relevant):**
- Is the input sorted?
- Are there duplicates?
- Can values be negative?
- Is the array modifiable in place?
- What is the range of `n`?
- Optimize for time or space?
- Is there one answer or multiple?

Skipping this step is the #1 reason candidates fail.

### M — Match (2 min) — THE MAGIC STEP

Map the problem to a known pattern. Scan signals, consult your pattern library (Part D), pick a candidate. Say aloud:
> "This looks like a sliding window problem because we have a contiguous subarray with a constraint."

Even if you're wrong, stating a hypothesis gives the interviewer a hook to nudge you.

### P — Plan (3–5 min)

1. Name the data structures you will use (hashmap, heap, stack…).
2. Write 5–10 pseudo-code lines.
3. State time and space complexity *before* coding.
4. Get interviewer buy-in: *"Does this approach make sense before I code it up?"*

Example pseudo-code:
```
initialize window_start = 0, max_len = 0, char_count = {}
for window_end in range(len(s)):
    add s[window_end] to char_count
    while len(char_count) > k:
        shrink window from left
    update max_len
return max_len
```

### I — Implement (10–15 min)

- Naming matches your pseudo-code.
- Talk occasionally while coding (every ~30 sec), not every keystroke.
- Get a working version first, then optimize.

### R — Review (3–5 min)

Pretend there is a bug. Walk through your code with a small example, tracing variable state line by line. Check: off-by-one errors, empty input, boundary conditions, integer overflow, null returns. Fix before the interviewer points it out.

### E — Evaluate / Expand (2 min)

- State final complexity.
- Mention trade-offs.
- Offer a follow-up: *"If this were a stream instead of a fixed array, we'd need a different approach."*

**45-min interview time budget:** 5 understand + 2 match + 5 plan + 15 implement + 5 review + 5 discuss = 37 min (buffer included).

---

<a id="part-b"></a>
## Part B: Read Constraints to Guess Complexity

Constraints are the interviewer telling you which algorithm they expect. Read them before anything else.

| If `n` is… | You need at most… | Probable patterns |
|---|---|---|
| n ≤ 10 | O(n!) or O(2ⁿ·n) | Backtracking, brute force, permutations |
| n ≤ 20 | O(2ⁿ) | Subsets, bitmask DP |
| n ≤ 100 | O(n⁴) | DP, brute force with optimization |
| n ≤ 500 | O(n³) | Floyd-Warshall, cubic DP |
| n ≤ 5,000 | O(n²) | DP, Dijkstra simple, quadratic loops |
| n ≤ 10⁵ | O(n log n) | Sorting, heaps, binary search, sweep line |
| n ≤ 10⁶ | O(n) | Sliding window, two pointers, hashmap |
| n ≤ 10⁸+ | O(log n) or O(1) | Binary search, math formula |

**Example in action:** *"Longest substring with at most k distinct characters. 1 ≤ n ≤ 10⁵."*
- n = 10⁵ forbids O(n²) → must be O(n).
- "substring with constraint" → **Sliding Window**.
- You just picked the pattern before reading the full problem.

---

<a id="part-c"></a>
## Part C: The Pattern Recognition Decision Tree

Run the problem through this tree in order. First match wins.

```
START
│
├── Is input a SORTED array or linked list?
│   ├── Looking for pair/triplet sum? → TWO POINTERS
│   ├── Searching for value or boundary? → BINARY SEARCH
│   └── Finding cycle or middle? → FAST & SLOW POINTERS
│
├── Is problem about CONTIGUOUS subarray / substring?
│   ├── Fixed size window? → SLIDING WINDOW (fixed)
│   ├── Variable size with constraint? → SLIDING WINDOW (dynamic)
│   └── Max/min in window? → MONOTONIC DEQUE
│
├── Is input a TREE?
│   ├── Level by level? → BFS (queue)
│   ├── Path from root to leaf? → DFS (recursion)
│   ├── Nth smallest / validation? → INORDER DFS
│   └── Lowest common ancestor? → DFS with return values
│
├── Is input a GRAPH / GRID / MATRIX?
│   ├── Shortest path unweighted? → BFS
│   ├── Shortest path weighted? → DIJKSTRA / BELLMAN-FORD
│   ├── Connected components / islands? → DFS/BFS or UNION-FIND
│   ├── Ordering with dependencies? → TOPOLOGICAL SORT
│   └── Cycle detection in directed graph? → DFS with colors
│
├── Is problem about INTERVALS / ranges?
│   ├── Overlaps or merge? → MERGE INTERVALS (sort by start)
│   ├── Max concurrent? → SWEEP LINE / HEAP
│   └── Scheduling? → GREEDY (sort by end)
│
├── Does it ask for TOP/LEAST K, kth element, or frequency?
│   → HEAP (priority queue) — or QUICKSELECT for O(n) average
│
├── Does it ask for ALL combinations / permutations / subsets?
│   → BACKTRACKING
│
├── Does it ask for "number of ways", "min/max cost", "longest/shortest",
│   AND subproblems overlap with optimal substructure?
│   → DYNAMIC PROGRAMMING
│     ├── 1D DP if state depends on 1 variable
│     ├── 2D DP if state depends on 2 variables (string pairs, grid)
│     └── DP on trees / DP on graphs for structural problems
│
├── Does it involve PREFIX / SUFFIX relationships?
│   ├── Range sum queries? → PREFIX SUM
│   ├── Next greater / smaller element? → MONOTONIC STACK
│   └── Prefix matching? → TRIE
│
├── Is it about RAW COUNTING or finding a unique element?
│   ├── "One appears once, rest twice" → XOR
│   ├── Frequency counting → HASHMAP
│   └── Numbers 1..n with missing/duplicate → CYCLIC SORT
│
└── None of the above?
    → Try brute force first, then look for redundant work to eliminate
```

---

<a id="part-d"></a>
## Part D: The Full Pattern Library (20 Patterns)

### 1. Two Pointers
- **Signal:** sorted input, pair/triplet sum, palindrome check, remove duplicates in place
- **Template:** `left=0, right=len-1; while left<right: move based on condition`
- **Canonical:** Two Sum II, 3Sum, Valid Palindrome, Container With Most Water

### 2. Sliding Window
- **Signal:** longest/shortest/any contiguous subarray/substring with a constraint
- **Template:** expand right; while constraint broken, shrink left; update answer
- **Canonical:** Longest Substring Without Repeating Chars, Min Window Substring, Max Sum Subarray of Size K

### 3. Fast & Slow Pointers (Floyd's)
- **Signal:** cycle detection, middle of linked list, happy number
- **Template:** `slow = slow.next; fast = fast.next.next; if slow == fast: cycle`
- **Canonical:** Linked List Cycle, Middle of Linked List, Happy Number

### 4. Merge Intervals
- **Signal:** overlapping ranges, meetings, booking
- **Template:** sort by start; for each interval: if overlaps last, merge; else append
- **Canonical:** Merge Intervals, Insert Interval, Meeting Rooms II

### 5. Cyclic Sort
- **Signal:** array contains integers in range [1, n] or [0, n], find missing/duplicate
- **Template:** `while nums[i] != i+1: swap nums[i] with nums[nums[i]-1]`
- **Canonical:** Find All Missing Numbers, Find Duplicate Number, First Missing Positive

### 6. In-place Linked List Reversal
- **Signal:** reverse whole or partial linked list without extra memory
- **Template:** `prev=None; while curr: nxt=curr.next; curr.next=prev; prev=curr; curr=nxt`
- **Canonical:** Reverse Linked List, Reverse Nodes in K-Group

### 7. Tree BFS
- **Signal:** level-order traversal, shortest path in tree, "by level"
- **Template:** `queue = deque([root]); while queue: size=len(q); for _ in range(size): process`
- **Canonical:** Level Order Traversal, Zigzag Traversal, Right Side View

### 8. Tree DFS
- **Signal:** root-to-leaf path, sum paths, tree validation, subtree problems
- **Template:** recursion with helper carrying running state
- **Canonical:** Path Sum, Max Depth, Validate BST, LCA

### 9. Graph BFS / DFS
- **Signal:** connected components, shortest path (unweighted), reachability, grid islands
- **Template:** `visited=set(); for node: if not visited: bfs/dfs(node)`
- **Canonical:** Number of Islands, Word Ladder, Clone Graph, Course Schedule

### 10. Topological Sort
- **Signal:** dependency/prerequisite, build order, "must come before"
- **Template:** Kahn's algorithm — compute indegree → queue of 0-indegree → BFS
- **Canonical:** Course Schedule I & II, Alien Dictionary

### 11. Union-Find (Disjoint Set)
- **Signal:** dynamic connectivity, "are A and B in the same group", count groups as you merge
- **Template:** `parent[]`, `find(x)` with path compression, `union(x,y)` with rank
- **Canonical:** Number of Islands II, Accounts Merge, Redundant Connection

### 12. Modified Binary Search
- **Signal:** sorted or rotated array, find boundary, "minimum capacity/days/speed such that…"
- **Template:** `while lo<hi: mid; if condition(mid): hi=mid else: lo=mid+1`
- **Canonical:** Search in Rotated Sorted Array, Find Peak Element, Koko Eating Bananas, Capacity to Ship

### 13. Top-K / Heap
- **Signal:** "k largest/smallest/most frequent", median of stream
- **Template:** `heapq.heappush`; if len > k: `heappop`
- **Canonical:** Kth Largest, Top K Frequent, Find Median from Data Stream

### 14. Two Heaps
- **Signal:** running median, scheduling with two halves
- **Template:** max-heap (small half) + min-heap (large half), balance after each add
- **Canonical:** Find Median from Data Stream, Sliding Window Median

### 15. Backtracking
- **Signal:** "all combinations/permutations/subsets", constraint satisfaction
- **Template:**
  ```
  def backtrack(path, choices):
      if done: result.append(path.copy()); return
      for c in choices:
          path.append(c)
          backtrack(path, updated_choices)
          path.pop()
  ```
- **Canonical:** Subsets, Permutations, N-Queens, Word Search, Combination Sum

### 16. Dynamic Programming
- **Signal:** optimal substructure + overlapping subproblems; "count ways", "min/max cost", "longest/shortest with constraint"
- **Approach:** define state → recurrence → base case → memo (top-down) or table (bottom-up)
- **Sub-patterns:**
  - **1D DP:** Climbing Stairs, House Robber, LIS
  - **2D DP (grid):** Unique Paths, Min Path Sum
  - **2D DP (two strings):** Edit Distance, LCS
  - **0/1 Knapsack:** Partition Equal Subset Sum, Target Sum
  - **Unbounded Knapsack:** Coin Change, Rod Cutting
  - **DP on intervals:** Matrix Chain, Burst Balloons
- **Recognition trick:** write brute-force recursion, notice the same arguments recurring, add memoization, done.

### 17. Monotonic Stack
- **Signal:** "next greater / smaller element", histogram, rain trapping
- **Template:** `stack=[]; for i,x in enumerate(arr): while stack and arr[stack[-1]] < x: pop and process; push i`
- **Canonical:** Next Greater Element, Daily Temperatures, Largest Rectangle in Histogram, Trapping Rain Water

### 18. Prefix Sum
- **Signal:** range sum queries, subarray sums, "number of subarrays equal to k"
- **Template:** `prefix[i] = prefix[i-1] + arr[i]; sum(i,j) = prefix[j]-prefix[i-1]`
- **Canonical:** Range Sum Query, Subarray Sum Equals K, Contiguous Array

### 19. Trie
- **Signal:** prefix search, autocomplete, word dictionary
- **Template:** node with children dict and end flag
- **Canonical:** Implement Trie, Word Search II, Design Autocomplete

### 20. Bitwise XOR
- **Signal:** "one number appears once, others twice", missing number without extra space
- **Key facts:** `x^x=0`, `x^0=x`, XOR is associative
- **Canonical:** Single Number, Missing Number, Two Single Numbers

---

<a id="part-e"></a>
## Part E: SQL Pattern Track

SQL has its own algorithm.

### The SQL Problem Algorithm

1. **Identify the grain** — "one row per ___?" (user, user-day, order)
2. **Identify the filter** — which rows survive (WHERE)
3. **Identify the group** — what aggregations (GROUP BY)
4. **Identify per-group logic** — ranking / running total / first or last → WINDOW FUNCTION
5. **Identify the final filter** — on aggregates (HAVING) or on ranks (outer query)
6. **Sanity check joins** — "could I be double-counting?"

### SQL Pattern Library

| Pattern | Signal | Template |
|---|---|---|
| **Nth highest per group** | "2nd highest salary per dept" | `ROW_NUMBER() OVER (PARTITION BY dept ORDER BY salary DESC)` then filter rn=2 |
| **Running total** | "cumulative sum by day" | `SUM(x) OVER (PARTITION BY user ORDER BY date)` |
| **Previous / next row** | "compare today vs yesterday" | `LAG(x) OVER (ORDER BY date)` |
| **Gaps & islands** | "longest streak of consecutive days" | Group by `date - ROW_NUMBER() days` |
| **Retention / cohorts** | "% returning in week N" | Self-join on user + date-diff bucketing |
| **Funnel analysis** | "users who did A then B then C" | Conditional aggregation with MIN(time) + ordering check |
| **Pivot without PIVOT** | "count by category as columns" | `SUM(CASE WHEN cat='A' THEN 1 ELSE 0 END)` |
| **Top-N per group** | "top 3 products per region" | `RANK()` with PARTITION + outer filter |
| **Duplicate detection** | "emails that appear twice" | `GROUP BY email HAVING COUNT(*) > 1` |
| **Self-join for hierarchy** | "employees with same manager" | `FROM t a JOIN t b ON a.mgr = b.mgr` |

### SQL Traps to Always Check

- Is your JOIN many-to-many (double-counting)?
- Are NULLs being silently dropped by `NOT IN`?
- Is your GROUP BY at the right grain?
- Did you remember `ORDER BY` inside `OVER()` when needed?
- Did you filter in `WHERE` when you should have filtered in `ON` (outer joins)?

---

<a id="part-f"></a>
## Part F: ML / DS Case Study Track

Used when the interviewer says *"Design a model to…"* — not a LeetCode problem.

### The 7-Step ML Case Study Algorithm (CRISP-ML simplified)

1. **Clarify**
   - What is the business objective?
   - How will success be measured (business metric + model metric)?
   - What is the scale (# users, # predictions/sec)?
   - Online or batch? Real-time or periodic?

2. **Frame as an ML problem**
   - Classification, regression, ranking, clustering, or LLM?
   - What is the label? (Often the hardest part — "what *exactly* is churn?")
   - Positive class rarity / imbalance?

3. **Data**
   - What tables / sources?
   - How do we get labels (historical events, surveys, implicit signals)?
   - How do we prevent leakage (future info in training)?
   - Sampling strategy

4. **Features**
   - Categorical (embeddings / one-hot), numerical (normalize), text (TF-IDF / embeddings)
   - Domain features (recency/frequency/monetary for churn)
   - Feature store — online vs offline consistency

5. **Model**
   - Start with a **baseline** (logistic regression or simple heuristic)
   - Justify each step up (gradient boosting → NN → LLM)
   - Mention regularization, cross-validation, hyperparameter tuning

6. **Evaluation**
   - Offline: confusion matrix → precision / recall / F1 / AUC / PR-AUC (imbalanced!)
   - Online: A/B test, guardrail metrics, statistical significance
   - Fairness and bias checks

7. **Deployment & Monitoring**
   - Serving (batch vs real-time, latency SLO)
   - Monitoring: data drift, concept drift, prediction distribution
   - Rollback, shadow deployment
   - Feedback loop for retraining

**Golden rule:** Always start with the simplest baseline and justify every step up the ladder. Interviewers hate candidates who jump straight to "I'd use a transformer."

---

<a id="part-g"></a>
## Part G: The Meta-Algorithm — How to Actually Learn Patterns

Knowing patterns is not enough. You need **pattern recognition reflexes**. Deliberate practice loop:

### The 4-Pass Method (per problem)

**Pass 1 — Understand (day 1)**
1. Read problem. Timer 10 min.
2. Identify the pattern *before* coding.
3. Stuck? Peek at pattern hint (not solution).
4. Solve it.
5. Journal 1 line: *"Problem X → Pattern Y. The signal was __."*

**Pass 2 — Internalize (day 3–4)**
Redo from scratch. No looking. Time yourself.

**Pass 3 — Blind recall (day 10)**
Redo again. Should finish in <15 min.

**Pass 4 — Teach (day 21)**
Explain pattern out loud as if teaching. If you can't explain *why*, you don't know it.

### The Pattern Journal (your secret weapon)

Keep a running file: `patterns.md`. Each entry:

```
Pattern: Sliding Window (variable size)
Trigger signals: substring/subarray + "longest/shortest" + constraint on content
Template: expand right, shrink left when broken, track best
Problems solved with it: Longest Substring K Distinct, Min Window Substring
Mistakes I've made: forgot to shrink while loop; used if instead of while
```

Re-read every Sunday.

### Daily Ritual (fits 2 hrs/day)

- **60 min:** 1–2 coding problems using UMPIRE out loud
- **45 min:** SQL problems + SQL algorithm steps
- **15 min:** Update pattern journal + review yesterday's mistakes

**Rule:** Never solve a problem without naming the pattern first. If you can't name it, look it up *before* coding — you are training recognition, not brute-force solving.

---

<a id="summary"></a>
## Mental Model Summary

When you walk into an interview and see a new problem:

1. **Read constraints** → cut the pattern space in half (Part B)
2. **Run the decision tree** → land on a pattern candidate (Part C)
3. **Recall the pattern template** from your library (Part D)
4. **Execute UMPIRE** — Understand → Match → Plan → Implement → Review → Evaluate (Part A)

- SQL problem → switch to the SQL algorithm (Part E)
- ML case study → switch to CRISP-ML (Part F)

Three tracks, one meta-process.

---

<a id="sources"></a>
## Sources

- [Grokking the Coding Interview (Educative)](https://www.educative.io/courses/grokking-coding-interview)
- [14 Patterns to Ace Any Coding Interview — Grokking / Fahim ul Haq](https://grokkingtechinterview.com/14-patterns-to-ace-any-coding-interview-question-c5bb3357f6ed)
- [Mastering the 20 Coding Patterns — DesignGurus](https://www.designgurus.io/blog/grokking-the-coding-interview-patterns)
- [seanprashad/leetcode-patterns (GitHub)](https://github.com/seanprashad/leetcode-patterns)
- [UMPIRE Interview Strategy — CodePath](https://guides.codepath.com/compsci/UMPIRE-Interview-Strategy)
- [Mastering the UMPIRE Strategy — DesignGurus](https://www.designgurus.io/blog/mastering-the-umpire-interview-strategy-in-coding-a-step-by-step-guide)
- [LeetCode Was HARD Until I Learned These 15 Patterns — Algomaster](https://blog.algomaster.io/p/15-leetcode-patterns)
- [Time Complexity Constraints Reference — LeetCode Discuss](https://leetcode.com/discuss/post/6067881/cp-special-learn-time-complexity-on-cons-n3of/)
- [Top SQL Patterns from FAANG Data Science Interviews — KDnuggets](https://www.kdnuggets.com/top-sql-patterns-from-faang-data-science-interviews-with-code)
- [SQL Window Functions Cheat Sheet — The Query Lab](https://www.thequerylab.com/blog/sql-window-functions-cheat-sheet)
- [Gap and Island SQL Problems — Practice Window Functions](https://www.practicewindowfunctions.com/learn/gap_and_island)
- [Memoization vs Tabulation — Educative](https://www.educative.io/blog/memoization-vs-tabulation)
- [ML System Design Interview Guide 2026 — Exponent](https://www.tryexponent.com/blog/machine-learning-system-design-interview-guide)
- [alirezadir/machine-learning-interviews (GitHub)](https://github.com/alirezadir/machine-learning-interviews)
- [Data Science Case Study Interview Questions — Interview Query](https://www.interviewquery.com/p/data-science-case-study-interview-questions)
