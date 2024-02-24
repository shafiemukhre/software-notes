# Graph Algorithms

## When Input is a 2D Array

I think the Number Islands problem is the Two Sums version for graph problems when the given input is a 2D Array.

### Recursive DFS template

```python
def fn(grid):
    rows, cols = len(grid), len(grid[0])

    def dfs(r, c):
        # handle invalid cases
        if r not in range(rows) or c not in range(cols): return  # out of bound
        # if (r, c) is invalid or has been visited: return

        # process node: do some logic and mark node as visited
        grid[r][c] = 'x' # or visited.add((r, c))

        # traverse all directions
        dirs = [(-1, 0), (0, 1), (1, 0), (0, -1)] # top, right, btm, left
        for dr, dc in dirs:
            nr, nc = r + dr, c + dc
            dfs(nr, nc)

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] is valid:
                dfs(r, c)
                # update res
    return res
```

<details>
<summary>Example solution for Number Islands problem using recursive DFS approach:</summary>

```python
def numIslands(self, grid: List[List[str]]) -> int:
    # approach: recursive DFS. O(M * N) runtime, O(M * N) space
    rows, cols = len(grid), len(grid[0])

    def dfs(r, c):
        # handle invalid cases
        if r not in range(rows) or c not in range(cols): return  # out of bound
        if grid[r][c] != "1": return  # not a land

        # process node
        grid[r][c] = "0"  # mark node as visited

        # traverse all directions
        dirs = [(-1, 0), (0, 1), (1, 0), (0, -1)]  # top, right, btm, left
        for dr, dc in dirs:
            nr, nc = r + dr, c + dc
            dfs(nr, nc)

    count = 0
    for i in range(rows):
        for j in range(cols):
            if grid[i][j] == "1":
                dfs(i, j)
                count += 1
    return count
```

</details>

### Iterative DFS template

Example solution for Number Islands problem using Iterative DFS approach:

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        # approach: iterative DFS w stack. O(M * N) runtime, O(M)
        if not grid or not grid[0]: return 0 # edge case

        rows, cols = len(grid), len(grid[0])
        count = 0

        def dfs(r, c):
            stack = [(r, c)]
            while stack:
                r, c = stack.pop()

                # process node
                grid[r][c] = '0' # mark node as visited

                # traverse all directions
                dirs = [(-1, 0), (0, 1), (1, 0), (0, -1)] # top, right, btm, left
                for dr, dc in dirs:
                    nr, nc = r + dr, c + dc
                    # handle valid cases
                    if nr in range(rows) and nc in range(cols) and grid[nr][nc] == '1':
                        stack.append((nr, nc))

        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == '1':
                    dfs(r, c)
                    count += 1

      return count
```

### BFS (iterative) template

## Union Find

> A disjoint-set data structure, also called a union–find data structure or merge–find set, is a data structure that stores a collection of disjoint (non-overlapping) sets. Equivalently, it stores a partition of a set into disjoint subsets. It provides operations for adding new sets, merging sets (replacing them by their union), and finding a representative member of a set. It implements two useful operations:

> 1. `Find`: Determine which subset a particular element is in. This can be used to determine if two elements are in the same subset aka a 'connected component'. Also, to find root parent.
> 2. `Union`: Join two subsets into a single subset. Connecting 2 nodes based on a given edge.

Some intuition

- A tree is 1 connected component, if you add 1 extra edge, there will be a cycle. For example, if there are $n$ nodes in the tree and there are $n$ unique edges, there's a cycle for sure.
- path compression: assign the grandparent to be a new parent.
- use rank for "path comparison".

```python
class UnionFind(object):
    def init (self, n) :
        self.parents = list(range(n))
        self.sizes = [1] * n

    def find(self, i):
        # option 1: using recursion
        While i != self.parents[i]:
            # path compression, have i points to the cluster centroid
            self.parents[i] = self.find(self.parents[i])
            i = self.parents[i]
            return i
        # # option 2: not using recursion?
        # root = i
        # while self.parents [root] != root:
        #     root = self.parents[root]
        # while self.parents[i] != root:
        #     parent = self.parents[i]
        #     self.parents[i] = root
        #     i = parent
        # return root

    def union (self, p, q):
        root_p, root_q = map(self.find, (p, q))
        if root_p == root_q: return
        small, big = sorted([root_p, root_q], key=lambda x: self.sizes[x])
        self .parents[small] = big
        self.sizes[big] += self.sizes[small]
```

## Topological Sort

- Problems: Course Schedule 1 & 2, Alien Dictionary
- Khan's Algorithm -> uses the in-degree technique.
- Topological sort -> DFS with visited set and a stack. Make sure to have recursion_check set as well to detect the cycle.

## Tips and Tricks

- If the input graph has weight, use `defaultdict(dict)`.
- if the input graph doesn't have weight, use `defaultdict(set)`.
- If nodes are unique, you can use `defaultdict(set)`, the nodes are not unique make sure to use `defaultdict(list)`.
- The membership test for the element in a `set` is $O(1)$ which is better than in a `list` with $O(n)$. Regardless, you will need to do a for loop anyway to visit all neighbors, so you can do a membership test here in the for loop.
- Be very comfortable with BFS, BFS usually has better space complexity. Use BFS if you can tell that BFS is more optimized, though DFS sometimes are more intuitive. No point spending 30+ minutes in an interview trying to get your DFS to work when it's not even the most optimized solution.
- There are 2 ways to backtrack in recursive DFS when traversing to neighbor nodes. Either create a temp variable to be into the next DFS function and backtrack it to the previous value, or pass in the variable with its operation into the DFS function directly e.g. `dfs(next_currency, target_currency, product * rate)`.

Resources:

- Study this: https://leetcode.com/discuss/general-discussion/971272/Python-Graph-Algorithms-One-Place-for-quick-revision
