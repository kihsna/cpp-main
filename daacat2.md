

* **Short bullet logic**
* **Pseudocode** (brief, complete, commented)
* **Time complexity**

DAA - CAT II
---

# **1. Huffman Coding**

**Logic:**

* Build a min-heap of symbols by frequency.
* Iteratively combine two least frequent nodes into a new node.
* Traverse tree to assign `0/1` codes.

**Pseudocode:**

```
function HuffmanCoding(symbols, frequencies):
    create min-heap of leaf nodes (symbol, frequency)
    while heap has >1 node:
        left = extractMin()
        right = extractMin()
        merged = Node(left.freq + right.freq)
        merged.left = left
        merged.right = right
        insert merged into heap
    root = remaining node
    traverse tree to generate codes (0-left, 1-right)
```

**Time Complexity:** O(n log n) (heap operations for n symbols)

**C++:** *(see previous Huffman code snippet above)*

---

# **2. 0/1 Knapsack**

**Logic:**

* Dynamic Programming approach.
* For each item and weight, choose max of including or excluding item.

**Pseudocode:**

```
function Knapsack(weights, values, W, n):
    DP[n+1][W+1] = 0
    for i = 1 to n:
        for w = 0 to W:
            if weights[i-1] <= w:
                DP[i][w] = max(values[i-1]+DP[i-1][w-weights[i-1]], DP[i-1][w])
            else:
                DP[i][w] = DP[i-1][w]
    return DP[n][W]
```

**Time Complexity:** O(n·W)

---

# **3. Fractional Knapsack**

**Logic:**

* Greedy: take items in descending value/weight ratio.
* Take fraction if item cannot fully fit.

**Pseudocode:**

```
function FractionalKnapsack(weights, values, W, n):
    items = [(value, weight, value/weight)]
    sort items by descending ratio
    totalValue = 0
    for item in items:
        if item.weight <= W:
            totalValue += item.value
            W -= item.weight
        else:
            totalValue += item.value * (W / item.weight)
            break
    return totalValue
```

**Time Complexity:** O(n log n) (for sorting)

---

# **4. Travelling Salesman Problem (TSP)**

**Logic:**

* Brute-force: check all permutations of cities.
* DP Held-Karp: use bitmask to store visited set and minimum cost to each city.

**Pseudocode (Brute-force):**

```
function TSP_BruteForce(graph, n):
    bestCost = ∞
    for each permutation of cities[1..n-1]:
        cost = sum of edges along permutation + return to start
        bestCost = min(bestCost, cost)
    return bestCost
```

**Pseudocode (DP):**

```
function TSP_DP(graph, n):
    DP[2^n][n] = ∞
    DP[1][0] = 0
    for state in 1..(2^n-1):
        for i in all cities in state:
            for j not in state:
                DP[state | (1<<j)][j] = min(DP[state | (1<<j)][j], DP[state][i]+graph[i][j])
    return min(DP[(1<<n)-1][i] + graph[i][0])
```

**Time Complexity:**

* Brute-force: O(n!)
* DP Held-Karp: O(n²·2^n)

---

# **5. N-Queens**

**Logic:**

* Backtracking: place one queen per row, check safety.
* Backtrack if placement leads to conflict.

**Pseudocode:**

```
function solveNQueens(n):
    board[n][n] = empty
    function backtrack(row):
        if row == n: record solution
        for col = 0..n-1:
            if safe(row, col):
                place queen
                backtrack(row+1)
                remove queen
    backtrack(0)
```

**Time Complexity:** O(n!) worst case

---

# **6. Sum of Subsets**

**Logic:**

* Backtracking: explore including or excluding each number.
* Record subset if sum equals target.

**Pseudocode:**

```
function sumOfSubsets(nums, target):
    function backtrack(i, currentSum, subset):
        if currentSum == target: record subset
        if i == len(nums) or currentSum > target: return
        backtrack(i+1, currentSum + nums[i], subset + nums[i]) // include
        backtrack(i+1, currentSum, subset) // exclude
    backtrack(0,0,[])
```

**Time Complexity:** O(2^n)

---

# **7. String Matching**

**Naive Logic:**

* Check pattern at every position of text.

**Rabin-Karp Logic:**

* Use rolling hash to avoid unnecessary string comparisons.

**Pseudocode (Naive):**

```
function NaiveMatch(text, pattern):
    for i = 0..n-m:
        if text[i..i+m-1] == pattern: report i
```

**Pseudocode (Rabin-Karp):**

```
function RabinKarp(text, pattern, d, q):
    compute initial hash for pattern and first window
    for i = 0..n-m:
        if hash matches and text window == pattern: report i
        update rolling hash for next window
```

**Time Complexity:**

* Naive: O(n·m)
* Rabin-Karp: O(n + m) average, O(n·m) worst case

---

# **8. Bellman-Ford (Shortest Path)**

**Logic:**

* Initialize distances from source to ∞, source = 0
* Relax all edges V-1 times
* Detect negative cycles in an extra pass

**Pseudocode:**

```
function BellmanFord(V, edges, source):
    dist[v] = ∞ for all v
    dist[source] = 0
    for i = 1..V-1:
        for each edge (u,v,w):
            if dist[u] + w < dist[v]: dist[v] = dist[u] + w
    for each edge (u,v,w):
        if dist[u] + w < dist[v]: report negative cycle
    return dist
```

**Time Complexity:** O(V·E)

---
