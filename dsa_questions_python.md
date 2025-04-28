# Frequently Asked DSA Questions in Python (with Explanations)

---

## 1. Reverse a Linked List

**Question:**  
Given the head of a singly linked list, reverse it.

**Explanation:**  
We need to reverse the pointers of each node so that they point to the previous node instead of the next.

**Solution:**
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def reverseList(head):
    prev = None
    curr = head
    while curr:
        next_temp = curr.next
        curr.next = prev
        prev = curr
        curr = next_temp
    return prev
```

---

## 2. Detect Cycle in a Linked List

**Question:**  
Given a linked list, determine if it has a cycle.

**Explanation:**  
Use two pointers moving at different speeds (Floyd’s Tortoise and Hare algorithm). If they meet, there’s a cycle.

**Solution:**
```python
def hasCycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False
```

---

## 3. Merge Two Sorted Lists

**Question:**  
Merge two sorted linked lists and return it as a new sorted list.

**Explanation:**  
Compare the heads of the two lists and build a new list by choosing the smaller value at each step.

**Solution:**
```python
def mergeTwoLists(l1, l2):
    dummy = ListNode()
    curr = dummy
    while l1 and l2:
        if l1.val < l2.val:
            curr.next = l1
            l1 = l1.next
        else:
            curr.next = l2
            l2 = l2.next
        curr = curr.next
    curr.next = l1 or l2
    return dummy.next
```

---

## 4. Implement Stack using Queue

**Question:**  
Implement a stack using only queue operations.

**Explanation:**  
Use a single queue and rearrange elements so that the newest element is always at the front.

**Solution:**
```python
from collections import deque

class MyStack:
    def __init__(self):
        self.q = deque()

    def push(self, x):
        self.q.append(x)
        for _ in range(len(self.q) - 1):
            self.q.append(self.q.popleft())

    def pop(self):
        return self.q.popleft()

    def top(self):
        return self.q[0]

    def empty(self):
        return not self.q
```

---

## 5. Valid Parentheses

**Question:**  
Given a string containing '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

**Explanation:**  
Use a stack to match opening and closing brackets.

**Solution:**
```python
def isValid(s):
    stack = []
    mapping = {')':'(', '}':'{', ']':'['}
    for char in s:
        if char in mapping.values():
            stack.append(char)
        elif char in mapping:
            if not stack or mapping[char] != stack.pop():
                return False
        else:
            return False
    return not stack
```

---

## 6. Binary Search

**Question:**  
Implement binary search on a sorted array.

**Explanation:**  
Repeatedly divide the search interval in half.

**Solution:**
```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

---

## 7. Find the Missing Number

**Question:**  
Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing.

**Explanation:**  
Sum the numbers from 0 to n and subtract the sum of the array.

**Solution:**
```python
def missingNumber(nums):
    n = len(nums)
    return n * (n + 1) // 2 - sum(nums)
```

---

## 8. Maximum Subarray Sum (Kadane's Algorithm)

**Question:**  
Find the contiguous subarray with the maximum sum.

**Explanation:**  
Use Kadane’s algorithm to keep track of the current sum and the maximum sum found so far.

**Solution:**
```python
def maxSubArray(nums):
    max_sum = curr_sum = nums[0]
    for num in nums[1:]:
        curr_sum = max(num, curr_sum + num)
        max_sum = max(max_sum, curr_sum)
    return max_sum
```

---

## 9. Two Sum

**Question:**  
Given an array of integers, return indices of the two numbers that add up to a target.

**Explanation:**  
Use a hash map to store numbers and their indices for O(1) lookups.

**Solution:**
```python
def twoSum(nums, target):
    lookup = {}
    for i, num in enumerate(nums):
        if target - num in lookup:
            return [lookup[target - num], i]
        lookup[num] = i
```

---

## 10. Inorder Traversal of Binary Tree

**Question:**  
Return the inorder traversal of a binary tree’s nodes’ values.

**Explanation:**  
Traverse left subtree, visit root, then traverse right subtree.

**Solution:**
```python
def inorderTraversal(root):
    res, stack = [], []
    while True:
        while root:
            stack.append(root)
            root = root.left
        if not stack:
            return res
        node = stack.pop()
        res.append(node.val)
        root = node.right
```

---

## 11. Lowest Common Ancestor in a Binary Search Tree

**Question:**  
Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes.

**Explanation:**  
In a BST, the LCA of two nodes p and q is the node with the largest value smaller than both p and q, and the smallest value larger than both. Traverse from the root: if both p and q are less than root, go left; if both are greater, go right; otherwise, root is the LCA.

**Solution:**
```python
def lowestCommonAncestor(root, p, q):
    while root:
        if p.val < root.val and q.val < root.val:
            root = root.left
        elif p.val > root.val and q.val > root.val:
            root = root.right
        else:
            return root
```

---

## 12. Top K Frequent Elements

**Question:**  
Given a non-empty array of integers, return the k most frequent elements.

**Explanation:**  
Count the frequency of each element using a hash map, then use a heap to extract the k elements with the highest frequency.

**Solution:**
```python
import heapq
from collections import Counter

def topKFrequent(nums, k):
    count = Counter(nums)
    return [item for item, freq in count.most_common(k)]
```

---

## 13. Longest Substring Without Repeating Characters

**Question:**  
Given a string, find the length of the longest substring without repeating characters.

**Explanation:**  
Use a sliding window and a hash map to track the last seen index of each character. Move the window start forward when a repeat is found.

**Solution:**
```python
def lengthOfLongestSubstring(s):
    char_index = {}
    left = max_len = 0
    for right, char in enumerate(s):
        if char in char_index and char_index[char] >= left:
            left = char_index[char] + 1
        char_index[char] = right
        max_len = max(max_len, right - left + 1)
    return max_len
```

---

## 14. Implement Min Stack

**Question:**  
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

**Explanation:**  
Use an auxiliary stack to keep track of the minimum value at each level of the main stack.

**Solution:**
```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []

    def push(self, x):
        self.stack.append(x)
        if not self.min_stack or x <= self.min_stack[-1]:
            self.min_stack.append(x)

    def pop(self):
        if self.stack.pop() == self.min_stack[-1]:
            self.min_stack.pop()

    def top(self):
        return self.stack[-1]

    def getMin(self):
        return self.min_stack[-1]
```

---

## 15. Number of Islands

**Question:**  
Given a 2D grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically.

**Explanation:**  
Use DFS or BFS to traverse each island and mark visited land. Increment the count for each new island found.

**Solution:**
```python
def numIslands(grid):
    if not grid:
        return 0
    rows, cols = len(grid), len(grid[0])
    count = 0
    def dfs(r, c):
        if r < 0 or r >= rows or c < 0 or c >= cols or grid[r][c] != '1':
            return
        grid[r][c] = '0'
        dfs(r+1, c)
        dfs(r-1, c)
        dfs(r, c+1)
        dfs(r, c-1)
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1':
                dfs(r, c)
                count += 1
    return count
```