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

The name of the algorithm is "Union Find" because there are 2 functions that form this algorithm. 
- `union()` function is unionizing multiple nodes — connecting 2 nodes based on a given edge.
- The `find()` function is to find the root parent. If the parent for 2 nodes is the same, then it means these 2 nodes are connected since both have the same parent. In other words, the find function is to find the node belonging to which set, if 2 nodes belong to the same set it means it is connected.

Some intuition

- A tree is 1 connected component, if you add 1 extra edge, there will be a cycle. For example, if there are $n$ nodes in the tree and there are $n$ unique edges, there's a cycle for sure.
- path compression: assign the grandparent to be a new parent.
- use rank for "path comparison". 
