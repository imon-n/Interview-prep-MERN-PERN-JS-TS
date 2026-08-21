# 🔥Coding Problems — Fresher Interview Preparation

### 🟢 Basic Number & Logic

**1. Factorial of a Number** — <a href="https://www.geeksforgeeks.org/problems/factorial5739/1" target="_blank">GeeksforGeeks</a>
```
class Solution:
    def factorial(self, n: int) -> int:
        # code here
        fact = 1
        for i in range(1, n+1):
            fact = fact * i
        return fact
```
**2. Fibonacci Series** — <a href="https://leetcode.com/problems/fibonacci-number/" target="_blank">LeetCode</a>
```
class Solution(object):
    def fib(self, n):
        a = 0
        b = 1
        if n==0 or n==1:
            return n
        for i in range(1,n):
            next = a + b
            a = b
            b = next
        return next
```
**3. Check Prime Number** — <a href="https://www.geeksforgeeks.org/problems/prime-number2314/1" target="_blank">GeeksforGeeks</a>
```
class Solution:
    def isPrime(self, n):
        if n < 2:
            return False
        for i in range(2, int(n**0.5)+1):
            if n % i == 0:
                return False
                break
        
        return True
```
- [ ] **4. Reverse a Number** — <a href="https://www.geeksforgeeks.org/problems/reverse-digit0316/1" target="_blank">GeeksforGeeks</a>
- [ ] **5. Check Palindrome Number** — <a href="https://leetcode.com/problems/palindrome-number/" target="_blank">LeetCode</a>
- [ ] **6. Find GCD and LCM** — <a href="https://www.geeksforgeeks.org/problems/lcm-and-gcd4516/1" target="_blank">GeeksforGeeks</a>

### 🟢 String

- [ ] **7. Reverse a String ⭐** — <a href="https://www.geeksforgeeks.org/problems/reverse-a-string/1" target="_blank">GeeksforGeeks</a>
- [ ] **8. Check Palindrome String ⭐** — <a href="https://leetcode.com/problems/valid-palindrome/" target="_blank">LeetCode</a>
- [ ] **9. Check Anagram ⭐** — <a href="https://leetcode.com/problems/valid-anagram/" target="_blank">LeetCode</a>
- [ ] **10. Count Character Frequency ⭐** — <a href="https://www.geeksforgeeks.org/problems/frequency-of-array-elements-1587115620/1" target="_blank">GeeksforGeeks</a>
- [ ] **11. First Non-Repeating Character** — <a href="https://leetcode.com/problems/first-unique-character-in-a-string/" target="_blank">LeetCode</a>
- [ ] **12. Reverse Words in a String** — <a href="https://leetcode.com/problems/reverse-words-in-a-string/" target="_blank">LeetCode</a>

### 🟡 Array

- [ ] **13. Find Largest & Smallest Element** — <a href="https://www.geeksforgeeks.org/problems/find-minimum-and-maximum-element-in-an-array4428/1" target="_blank">GeeksforGeeks</a>
- [ ] **14. Find Second Largest Element ⭐** — <a href="https://www.geeksforgeeks.org/problems/second-largest3735/1" target="_blank">GeeksforGeeks</a>
- [ ] **15. Remove Duplicates from Array ⭐** — <a href="https://leetcode.com/problems/remove-duplicates-from-sorted-array/" target="_blank">LeetCode</a>
- [ ] **16. Find Duplicate Elements** — <a href="https://leetcode.com/problems/find-all-duplicates-in-an-array/" target="_blank">LeetCode</a>
- [ ] **17. Find Missing Number ⭐** — <a href="https://leetcode.com/problems/missing-number/" target="_blank">LeetCode</a>
- [ ] **18. Move All Zeros to End ⭐** — <a href="https://leetcode.com/problems/move-zeroes/" target="_blank">LeetCode</a>
- [ ] **19. Merge Two Sorted Arrays** — <a href="https://leetcode.com/problems/merge-sorted-array/" target="_blank">LeetCode</a>
- [ ] **20. Find Intersection of Two Arrays** — <a href="https://leetcode.com/problems/intersection-of-two-arrays/" target="_blank">LeetCode</a>

### 🟠 Interview Patterns

- [ ] **21. Two Sum ⭐⭐⭐** — <a href="https://leetcode.com/problems/two-sum/" target="_blank">LeetCode</a>
- [ ] **22. Maximum Subarray Sum ⭐** — <a href="https://leetcode.com/problems/maximum-subarray/" target="_blank">LeetCode</a>
- [ ] **23. Best Time to Buy & Sell Stock ⭐** — <a href="https://leetcode.com/problems/best-time-to-buy-and-sell-stock/" target="_blank">LeetCode</a>
- [ ] **24. Binary Search ⭐⭐⭐** — <a href="https://leetcode.com/problems/binary-search/" target="_blank">LeetCode</a>
- [ ] **25. Search Insert Position** — <a href="https://leetcode.com/problems/search-insert-position/" target="_blank">LeetCode</a>
- [ ] **26. Valid Parentheses ⭐** — <a href="https://leetcode.com/problems/valid-parentheses/" target="_blank">LeetCode</a>
- [ ] **27. Longest Substring Without Repeating Characters ⭐** — <a href="https://leetcode.com/problems/longest-substring-without-repeating-characters/" target="_blank">LeetCode</a>
- [ ] **28. Reverse a Linked List** — <a href="https://leetcode.com/problems/reverse-linked-list/" target="_blank">LeetCode</a>
- [ ] **29. Detect Cycle in Linked List** — <a href="https://leetcode.com/problems/linked-list-cycle/" target="_blank">LeetCode</a>
- [ ] **30. Majority Element** — <a href="https://leetcode.com/problems/majority-element/" target="_blank">LeetCode</a>
