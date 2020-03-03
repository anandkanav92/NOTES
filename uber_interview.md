---
>**UBER**
---
 **`Generate all combinations`** 📡
 > Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

- Create a mapping from number to set of letters.
- For each number, for loop over every mapping one by one. if len == digits given (or len of digits == 0) add the combination
  

```python
class Solution:
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        phone = {'2': ['a', 'b', 'c'],
                 '3': ['d', 'e', 'f'],
                 '4': ['g', 'h', 'i'],
                 '5': ['j', 'k', 'l'],
                 '6': ['m', 'n', 'o'],
                 '7': ['p', 'q', 'r', 's'],
                 '8': ['t', 'u', 'v'],
                 '9': ['w', 'x', 'y', 'z']}
                
        def backtrack(combination, next_digits):
            # if there is no more digits to check
            if len(next_digits) == 0:
                # the combination is done
                output.append(combination)
            # if there are still digits to check
            else:
                # iterate over all letters which map 
                # the next available digit
                for letter in phone[next_digits[0]]:
                    # append the current letter to the combination
                    # and proceed to the next digits
                    backtrack(combination + letter, next_digits[1:])
                    
        output = []
        if digits:
            backtrack("", digits)
        return output
```

---
 **`Group Anagrams`** 📡
 > Given an array of strings, group anagrams together. Input: ["eat", "tea","tan", "ate", "nat", "bat"], Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
- generate a key for every input in array. store it in a dict as a list. o(NK) and space o(NK).
  

```python
class Solution:
    def groupAnagrams(strs):
        ans = collections.defaultdict(list)
        for s in strs:
            count = [0] * 26
            for c in s:
                count[ord(c) - ord('a')] += 1
            ans[tuple(count)].append(s)
        return ans.values()
```
---
 **`Group Shifted strings`** 📡
 > Given a string, we can “shift” each of its letter to its successive letter, for example: "abc" -> "bcd". We can keep “shifting” which forms the sequence:

- Generate a diff os consecutive strings i.e "abc" => "11".
- Use this diff as key and group every string.
- o(nk) and space o(nk)

---
**`Two Sum`** 🌄
>Given an array of integers, return indices of the two numbers such that they add up to a specific target.

- use hashtable. Store the current number and check if the complement exists already.
- o(n) and o(n) space

---
**`Generate Paranthesis`** 🍢
>Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

- key is to always first generate open bracket and then closed ones.
- add proper conditions

```python
def local(results,op,cl,n,current,para_open,para_close):
            # print("current {}".format(current))
            if cl==n:
                results.append(current)
            if op < n:
                op+=1
                current+=para_open
                local(results,op,cl,n,current+para_open,para_open,para_close)
            if cl < op:
                cl+=1
                current+=para_close
                local(results,op,cl,n,current,para_open,para_close)
```
---
**`24. Swap Nodes in Pairs`** 💦
>Given a linked list, swap every two adjacent nodes and return its head.

```python
def swapPairs(self, head: ListNode) -> ListNode:
        
        if not head or not head.next:
            return head
        dummy = ListNode(0)
        dummy.next = head
        prev = dummy
        while head is not None and head.next is not None:
            new_head = head.next
            prev.next = new_head
            temp = new_head.next
            new_head.next = head
            head.next = None
            prev = head
            head = temp
        if head is not None:
            prev.next = head
        return dummy.next
```
---
**`15. 3SUM`** 🐯
>Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

- Sort the array
- Fix the first value and find all the possible pairs where sum == 0.
- o(n^2+n log(n)) and o(1) space.
 
```python
def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = []
        n = len(nums)
        nums = sorted(nums)
        for i in range(n-2):
            if i > 0 and nums[i] == nums[i-1]:
                continue
            j = i+1
            k = n-1
            new_target = -nums[i]
            while j < k:
                summ = nums[j] + nums[k]
                if summ < new_target:
                    j += 1
                elif summ > new_target:
                    k -= 1
                else:
                    res.append([nums[i], nums[j], nums[k]])
                    while j < k and nums[j+1] == nums[j]:
                        j += 1
                    j += 1
                    while k > j and nums[k-1] == nums[k]:
                        k -= 1
                    k -= 1
        return res
```
---
**`23. Merge k Sorted Lists`** 🚴
>Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

- Use priority queue which uses min heap to keeo the data in sorted way. o(nlogn)
- other possible way is to merge two arrays at once and combine them. o(logn) times o(n) for merging two arrays into one.


```python
from Queue import PriorityQueue

class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        head = point = ListNode(0)
        q = PriorityQueue()
        for l in lists:
            if l:
                q.put((l.val, l))
        while not q.empty():
            val, node = q.get()
            point.next = ListNode(val)
            point = point.next
            node = node.next
            if node:
                q.put((node.val, node))
        return head.next
```
---
**`23. Merge intervals`** 🚹
>Given a collection of intervals, merge all overlapping intervals.


- Sort the starting time and append to the result. For every next item, check if there is a disjoint set or if it overlaps


```python
def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        if not intervals:
            return None
        sorted_intervals = sorted(intervals,key=lambda l:(l[0],l[1]))
        print(sorted_intervals)
        start = sorted_intervals[0][0]
        end = sorted_intervals[0][1]
        time = end-start
        max_start = start
        max_end = end
        result = []
        for index in range(1,len(sorted_intervals)):
            if sorted_intervals[index][0] <= end:
                if end<sorted_intervals[index][1]:
                    end = sorted_intervals[index][1]
                continue
            else:
                result.append([start,end])
                start = sorted_intervals[index][0]
                end = sorted_intervals[index][1]
                continue
        result.append([start,end])
        return result
```
---
**`54. Spiral Matrix`** 🚹
>Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.


- Use the distance concept. Start with 0 and then increase one by one.


```python
if not matrix:
            return None
        dist = 0
        row,col = 0,0
        m,n = len(matrix),len(matrix[0])
        
        condition = min(m,n)
        if condition%2!=0:
            condition = condition+1
        result = []
        while dist<condition//2:
            
            for ri in range(dist,n-dist):
                result.append(matrix[dist][ri])
            print("result row{}".format(result))
            row +=1            
            for ci in range(row,m-row+1):
                result.append(matrix[ci][n-dist-1])
            col+=1
            print("result col{}".format(result))
            
            if m-dist-1 != dist:
                for ri in range(n-dist-2,dist-1,-1):
                    result.append(matrix[m-dist-1][ri])
                print("result row back{}".format(result))
            if dist != n-dist-1:
                for ci in range(m-row-1,row-1,-1):
                    result.append(matrix[ci][dist])
            dist+=1
            print("result row fwd{}".format(result))
     
        return result
```
---
**`29. Decode ways`** 🚹
>A message containing letters from A-Z is being encoded to numbers using the following mapping:

- DP problem. Similar to stair problem where you can take either 1 or more steps, or game problem where you play with other person.
- For every step, you can pick one or two strings and validate if it could be mapped to our criteria. If it reaches end, that means all the below ones had valid combinations.
- In DP, you have runtime = number of unique states/parameter X time taken for each state. In this case, each state is O(1) and unique states are n, so O(n) with O(n) space.


```python
def numDecodings(self, s: str) -> int:
        if not s:
            return None
        if int(s[0])==0:
            return 0
        dp = [-1] * len(s)
        def recursive(s):
            if not s:
                return 1
           
            if dp[len(s)-1]>-1:
                return dp[len(s)-1]
            
            count = 0
            if 0<int(s[0])<10:
                count = count + recursive(s[1:])
            
            if len(s)>=2:
                if 0<int(s[0]+s[1])<27 and int(s[0])!=0:
                    count = count + recursive(s[2:])
            dp[len(s)-1] = count        
            return dp[len(s)-1] 
        
        count = 0
        return recursive(s)
        return count
```
---
**`29. Decode ways`** 🚹
>A message containing letters from A-Z is being encoded to numbers using the following mapping:

- DP problem. Similar to stair problem where you can take either 1 or more steps, or game problem where you play with other person.
- For every step, you can pick one or two strings and validate if it could be mapped to our criteria. If it reaches end, that means all the below ones had valid combinations.
- In DP, you have runtime = number of unique states/parameter X time taken for each state. In this case, each state is O(1) and unique states are n, so O(n) with O(n) space.


```python
def numDecodings(self, s: str) -> int:
        if not s:
            return None
        if int(s[0])==0:
            return 0
        dp = [-1] * len(s)
        def recursive(s):
            if not s:
                return 1
           
            if dp[len(s)-1]>-1:
                return dp[len(s)-1]
            
            count = 0
            if 0<int(s[0])<10:
                count = count + recursive(s[1:])
            
            if len(s)>=2:
                if 0<int(s[0]+s[1])<27 and int(s[0])!=0:
                    count = count + recursive(s[2:])
            dp[len(s)-1] = count        
            return dp[len(s)-1] 
        
        count = 0
        return recursive(s)
        return count
```
