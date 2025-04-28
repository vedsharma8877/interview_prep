# Frequently Asked Python Coding Questions & Solutions

This document collects frequently asked Python coding questions, along with concise code solutions for each.

---

## 1. Reverse a String

```python
def reverse_string(s):
    return s[::-1]
```

---

## 2. Factorial Using Recursion

```python
def factorial(n):
    return 1 if n == 0 else n * factorial(n-1)
```

---

## 3. Check if a String is a Palindrome

```python
def is_palindrome(s):
    return s == s[::-1]
```

---

## 4. Remove Duplicates from a List

```python
def remove_duplicates(lst):
    return list(set(lst))
```

---

## 5. Find Largest/Smallest Number in a List

```python
def find_largest(lst):
    return max(lst)

def find_smallest(lst):
    return min(lst)
```

---

## 6. Count Frequency of Elements in a List or String

```python
from collections import Counter
def count_frequency(collection):
    return dict(Counter(collection))
```

---

## 7. Merge Two Sorted Lists

```python
def merge_sorted_lists(lst1, lst2):
    return sorted(lst1 + lst2)
```

---

## 8. Find the Second Largest Element in a List

```python
def second_largest(lst):
    unique_lst = list(set(lst))
    unique_lst.sort()
    return unique_lst[-2] if len(unique_lst) >= 2 else None
```

---

## 9. Check if a Number is Prime

```python
def is_prime(n):
    if n <= 1:
        return False
    for i in range(2, int(n**0.5)+1):
        if n % i == 0:
            return False
    return True
```

---

## 10. Fibonacci Series (Recursion & Iteration)

```python
def fibonacci_recursive(n):
    if n <= 1:
        return n
    return fibonacci_recursive(n-1) + fibonacci_recursive(n-2)

def fibonacci_iterative(n):
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a+b
    return a
```

---

## 11. Sort a List of Tuples by the Second Item

```python
def sort_tuples_by_second(lst):
    return sorted(lst, key=lambda x: x[1])
```

---

## 12. Read and Write to a File

```python
def write_to_file(filename, text):
    with open(filename, 'w') as f:
        f.write(text)

def read_from_file(filename):
    with open(filename, 'r') as f:
        return f.read()
```

---

## 13. Find All Pairs Summing to a Specific Value

```python
def find_pairs_with_sum(lst, target):
    seen = set()
    pairs = set()
    for num in lst:
        comp = target - num
        if comp in seen:
            pairs.add(tuple(sorted((num, comp))))
        seen.add(num)
    return list(pairs)
```

---

## 14. Flatten a Nested List

```python
def flatten_list(nested_list):
    result = []
    for item in nested_list:
        if isinstance(item, list):
            result.extend(flatten_list(item))
        else:
            result.append(item)
    return result
```

---

## 15. Check if Two Strings are Anagrams

```python
def are_anagrams(str1, str2):
    return sorted(str1) == sorted(str2)
```

---

## 16. Find Intersection and Union of Two Lists

```python
def intersection(lst1, lst2):
    return list(set(lst1) & set(lst2))

def union(lst1, lst2):
    return list(set(lst1) | set(lst2))
```

---

## 17. Check if Substring is Present in String

```python
def substring_present(sub, s):
    return sub in s
```

---

## 18. Convert List of Strings to a Single String

```python
def list_to_string(lst):
    return ''.join(lst)
```

---

## 19. Remove All Vowels from a String

```python
def remove_vowels(s):
    vowels = 'aeiouAEIOU'
    return ''.join([c for c in s if c not in vowels])
```

---

## 20. Length of Longest Word in a Sentence

```python
def longest_word_length(sentence):
    words = sentence.split()
    return max(len(word) for word in words)
```

---

## 21. Count the Number of Words in a String

```python
def word_count(s):
    return len(s.split())
```

---

## 22. Extract Digits from a String

```python
def extract_digits(s):
    return [int(c) for c in s if c.isdigit()]
```

---

## 23. Check if a List is Sorted

```python
def is_sorted(lst):
    return lst == sorted(lst)
```

---

## 24. Group Words with Same Characters (Anagram Groups)

```python
from collections import defaultdict
def group_anagrams(words):
    groups = defaultdict(list)
    for word in words:
        key = ''.join(sorted(word))
        groups[key].append(word)
    return list(groups.values())
```

---

## 25. Find Common Elements in Three Sorted Arrays

```python
def common_elements(arr1, arr2, arr3):
    return list(set(arr1) & set(arr2) & set(arr3))
```

---

## 26. Rotate a List Right/Left by k Places

```python
def rotate_right(lst, k):
    k %= len(lst)
    return lst[-k:] + lst[:-k]

def rotate_left(lst, k):
    k %= len(lst)
    return lst[k:] + lst[:k]
```

---

## 27. Find Missing Numbers in a Range from a List

```python
def missing_numbers(lst, start, end):
    return list(set(range(start, end+1)) - set(lst))
```

---

## 28. All Permutations of a String

```python
from itertools import permutations
def all_permutations(s):
    return [''.join(p) for p in permutations(s)]
```

---

## 29. Sort a Dictionary by Value

```python
def sort_dict_by_value(d):
    return dict(sorted(d.items(), key=lambda item: item[1]))
```

---

## 30. Convert List of Tuples into a Dictionary

```python
def tuples_to_dict(tuples):
    return dict(tuples)
```

---

## 31. Find the Most Frequent Element in a List

```python
def most_frequent(lst):
    return max(set(lst), key=lst.count)
```

---

## 32. Check if Two Lists are Permutations of Each Other

```python
def are_permutations(lst1, lst2):
    return sorted(lst1) == sorted(lst2)
```

---

## 33. Generate All Subsets (Power Set) of a List

```python
from itertools import chain, combinations
def power_set(lst):
    return list(chain.from_iterable(combinations(lst, r) for r in range(len(lst)+1)))
```

---

## 34. Find the First Non-Repeating Character in a String

```python
from collections import Counter
def first_non_repeating(s):
    counts = Counter(s)
    for c in s:
        if counts[c] == 1:
            return c
    return None
```

---

## 35. Implement a Stack and Queue Using Lists

```python
class Stack:
    def __init__(self):
        self.items = []
    def push(self, item):
        self.items.append(item)
    def pop(self):
        return self.items.pop()
    def is_empty(self):
        return not self.items

class Queue:
    def __init__(self):
        self.items = []
    def enqueue(self, item):
        self.items.append(item)
    def dequeue(self):
        return self.items.pop(0)
    def is_empty(self):
        return not self.items
```

---