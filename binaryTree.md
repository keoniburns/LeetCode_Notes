# Binary Tree

## 102. Binary Tree Level Order Traversal

### Problem

Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

### Pseudocode and explanation

1. create a queue to store the nodes
2. add the root node to the queue
3. while the queue is not empty, remove the first node from the queue and add its value to the result list
4. if the node has a left child, add it to the queue
5. if the node has a right child, add it to the queue
6. return the result list

```
function LevelOrder(root):
    if root is null:
        return empty list

    result = empty list
    current_level = list containing only root

    while current_level is not empty:
        level_values = empty list
        next_level = empty list

        for each node in current_level:
            add node.value to level_values

            if node.left is not null:
                add node.left to next_level
            if node.right is not null:
                add node.right to next_level

        add level_values to result
        current_level = next_level

    return result
```

## 98. Validate Binary Search Tree

### Problem

Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:

- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than the node's key.
- Both the left and right subtrees must also be binary search trees.

### Pseudocode and explanation

1. create a helper function that takes in a node, a lower bound, and an upper bound
2. if the node is None, return True
3. if the node's value is less than the lower bound or greater than the upper bound, return False
4. return the helper function called on the left and right subtrees with the updated bounds

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isValidBST(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: bool
        """
        def validate(node, lower, upper):
            if not node:
                return True
            if node.val <= lower or node.val >= upper:
                return False
            # this is a v important step
            return validate(node.left, lower, node.val) and validate(node.right, node.val, upper)
        return validate(root,-sys.maxsize,sys.maxsize)
```

## 207. Course Schedule

### Problem

There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.

Return true if you can finish all courses. Otherwise, return false.

### Pseudocode and explanation

1. create a graph from the prerequisites
2. perform a topological sort on the graph
3. if the topological sort is successful, return True
4. otherwise, return False

```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        # Create a graph representation
        graph = {}
        for course, prereq in prerequisites:
            if course not in graph:
                graph[course] = []
            graph[course].append(prereq)

        # Keep track of visited courses
        visited = set()

        def dfs(course):
            # If we've seen this course in the current path, we have a cycle
            if course in path:
                return False
            # If we've already processed this course, no need to do it again
            if course in visited:
                return True

            path.add(course)
            for prereq in graph.get(course, []):
                if not dfs(prereq):
                    return False
            path.remove(course)

            visited.add(course)
            return True

        # Check each course
        for course in range(numCourses):
            path = set()
            if not dfs(course):
                return False

        return True
```

```
        Graph Representation:
1 -> [0]
2 -> [1]
3 -> [1, 2]

DFS Process:

Course 0:
0 (no prerequisites)
✓ Visited

Course 1:
1 -> 0 (already visited)
✓ Visited

Course 2:
2 -> 1 (already visited)
✓ Visited

Course 3:
3 -> 1 (already visited)
  -> 2 (already visited)
✓ Visited

Final Result: True (Can finish all courses)

Cyclic Example:
prerequisites = [[1,0], [0,1]]

Graph Representation:
1 -> [0]
0 -> [1]

DFS Process:

Course 0:
0 -> 1 -> 0 (cycle detected!)
✗ Cannot finish

Final Result: False (Cannot finish all courses)

```
