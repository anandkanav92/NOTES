---
**UBER** 🚗
---
**`Generate all combinations`** 🈺
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
 **`Group Anagrams`** 🍌
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

**`104. Maximum Depth of Binary Tree`** 🌲
>The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

- do a post traversal and for each level do a +1. If root is none, return -1, as we did a +1 for every level first even when the level doesn't exist.

```python
def maxDepth(self, root: TreeNode) -> int:
        if not root:
            return 0
        def getDepth(root):
            if root:
                ldepth = 1+getDepth(root.left)
                # print("ldepth {}".format(ldepth))
                rdepth = 1+getDepth(root.right)
                # print("rdepth {}".format(rdepth))

                return max(ldepth,rdepth)
            else:
                return 0
        
        return getDepth(root)+1
```
---
**`133. Clone Graph`** 🉐
>Given a reference of a node in a connected undirected graph. Return a deep copy (clone) of the graph.

- question is asking to do a dfs of a graph, and make a copy of the current graph and return.
- create a dict with key as val and containing list to neighbors.
- start with 1 and do dfs and keep creating new node when encountered for the first time, otherwise ad neighbors. simple code below.

```python
def cloneGraph(self, node: 'Node') -> 'Node':
    if not node:
        return node
    root = Node(node.val)
    stack = [node]
    visit = {}
    visit[node.val] = root
    while stack:
        top = stack.pop()

        for n in top.neighbors:
            if n.val not in visit:
                stack.append(n)
                visit[n.val] = Node(n.val)
            visit[top.val].neighbors.append(visit[n.val])

    return root
```

---
**`122. Best Time to Buy and Sell Stock II`** 💰
>Say you have an array for which the ith element is the price of a given stock on day i. Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

- trick is, we check the difference between consecutive elements to get profit.

```python
def cloneGraph(self, node: 'Node') -> 'Node':
    if not node:
        return node
    root = Node(node.val)
    stack = [node]
    visit = {}
    visit[node.val] = root
    while stack:
        top = stack.pop()

        for n in top.neighbors:
            if n.val not in visit:
                stack.append(n)
                visit[n.val] = Node(n.val)
            visit[top.val].neighbors.append(visit[n.val])

    return root
```
---
**`138. Copy List with Random Pointer`** 🍴
>A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

- Similar to clone graph. make a dict looking out for any future declaration of nodes in next and random pointer. Important twist is to make a dict on full node rather than just value asvalue will be repeated. 


```python
    def copyRandomList(self, head: 'Node') -> 'Node':
        visited = {
            
        }
        
        if not head:
            return head
        root = Node(head.val)
        ramba = head
        
        while head:
            if head not in visited:
                visited[head] = Node(head.val)
            if head.next and head.next not in visited:
                
                visited[head.next] = Node(head.next.val)
            
            if head.next:
                visited[head].next = visited[head.next]
            else:
                visited[head].next = None
                
            if head.random and head.random not in visited:
                visited[head.random] = Node(head.random.val)
                
            if head.random:
                visited[head].random = visited[head.random]
            else:
                visited[head].random = None
            head = head.next
        return visited[ramba]
```
---
**`Min value in a stack`** 📭
>getMin() -- Retrieve the minimum element in the stack.

- Very good technique is to store a tuple in the stack, storing the minimum value at that point inside the stack. update everytime you enter the new value in stack.


```python
    def push(self, x):
        """
        :type x: int
        :rtype: nothing
        """
        if not self.stack:
            self.stack.append((x,x)) 
        else:
            self.stack.append((x,min(x,self.stack[-1][1])))
```
---
**`K Closest Points to Origin`**
>We have a list of points on the plane.  Find the K closest points to the origin (0, 0).(Here, the distance between two points on a plane is the Euclidean distance.)

- Generalised concept: there is a metric for each datapoint, need to sort on the fly. 
- priority queue will do the sort in o(n log(n)), then retrieve the top K elements from the queue. 


```python
def kClosest(self, points: List[List[int]], K: int) -> List[List[int]]:
        def calc(point):
            return math.sqrt(point[0]*point[0]+point[1]*point[1])
        if not points:
            return []
        
        queue = PriorityQueue()
        
        for index in range(len(points)):
            dist = calc(points[index])
            queue.put((dist,points[index]))
        
        results = [
            
        ]
        for index in range(0,K):
            # print(queue.get())
            ramu = queue.get()
            results.append(ramu[1])
        return results
```
---
**`Word Break`** 1️⃣
>Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

- think with recursion and then build up to DP.
- store value at every break point, so that itcould be used in the future. 
- at every point if the current word is in dict, break it. if all the following breakpoints in the word are true, then return true else false.


```python
def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        if not s:
            return s
        
        n=len(s)
        memo = [-1]*n
        
        def local(s,worDict,index,n):
            if index>=n:
                return True
            
            if memo[index] != -1:
                return memo[index]
            
            for count in range(index,len(s)):
                if s[index:count+1] in worDict:
                    if local(s,wordDict,count+1,n):
                        memo[index]= True
                        return memo[index]
            memo[index]= False
            return memo[index]
        return local(s,wordDict,0,n)
```
---
**`Word Break 2`** 2️⃣
>Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

- Very Important trick! instead of starting with string, start with words in dict. As the string should start or match atleast one word, if s doesn't start with word, continue.
- if there is a match : 
    + if len(s) == word that means no other word exist. so just append the word and continue. This is the base case that makes sure the string is added only if there is a positive end.
    + if there is more string left, recurse to the new substring and add every new result with a space.
    

```python
def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
        if not s:
            return s
        
        n = len(s)
        memo = {}
        def helper(s,wordDict,memo):
            if s in memo: return memo[s]
            if not s: return []

            res = []
            for word in wordDict:
                if not s.startswith(word):
                    continue
                if len(word) == len(s):
                    res.append(word)
                else:
                    resultOfTheRest = helper(s[len(word):], wordDict, memo)
                    for item in resultOfTheRest:
                        item = word + ' ' + item
                        res.append(item)
            memo[s] = res
            return res
        
        return helper(s,wordDict,memo)
```
---
`** Reverse Words in a String II**` 🔁
> Given an input string, reverse the string word by word. A word is defined as a sequence of non-space characters. For example, Given s = "the sky is blue",
return "blue is sky the".

- key is first reverse every word seperately. Then reverse the whole string.

---
**`72. Edit Distance`**🎲
>Given two words word1 and word2, find the minimum number of operations required to convert word1 to word2.You have the following 3 operations permitted on a word:
Insert a character
Delete a character
Replace a character

- at every step, we have 3 options. 
    + Delete a character from host string <==> Inserting a character in other string.
    + Replace a charcter in the host string.
    + insert a character in the host string <==> Delete a character from host string.
- If two character indexes are equal, we move both indexes forward.

```python
def minDistance(self, word1: str, word2: str) -> int:
        
        n = len(word1)
        m = len(word2)
        memo = {}
        def local(word1,word2,m_index,n_index,n,m):
            if m_index>=m:
                return max(n-n_index,0)
            elif n_index>=n:
                # print(m-m_index)
                return max(m-m_index,0)
            if (n_index,m_index) in memo:
                return memo[(n_index,m_index)]
            if word1[n_index] == word2[m_index]:
                memo[(n_index,m_index)] = local(word1,word2,m_index+1,n_index+1,n,m)
                return memo[(n_index,m_index)] 
            
            memo[(n_index,m_index)] =   min(
                      1+local(word1,word2,m_index,n_index+1,n,m),
                      1+local(word1,word2,m_index+1,n_index,n,m),
                      1+local(word1,word2,m_index+1,n_index+1,n,m)
            )
            return memo[(n_index,m_index)] 
        
        return local(word1,word2,0,0,n,m)
```
---
**`Reverse Linked List II`**🔗
>Reverse a linked list from position m to n. Do it in one-pass.

- loop over until m is reached.
- take three pointer approach. prev=m-1, curr = m, third=m+1
- keep track of tail global node, and the node that would be new head of the reversed list i.e current.

```python
def reverseBetween(self, head: ListNode, m: int, n: int) -> ListNode:
        if not head:
            return None

        # Move the two pointers until they reach the proper starting point
        # in the list.
        cur, prev = head, None
        while m > 1:
            prev = cur
            cur = cur.next
            m, n = m - 1, n - 1

        # The two pointers that will fix the final connections.
        tail, con = cur, prev

        # Iteratively reverse the nodes until n becomes 0.
        while n:
            third = cur.next
            cur.next = prev
            prev = cur
            cur = third
            n -= 1

        # Adjust the final connections as explained in the algorithm
        if con:
            con.next = prev
        else:
            head = prev
        tail.next = cur
        return head
```
---
**`230. Kth Smallest Element in a BST`**
>Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

- if doing via recursion, store the value in thelist and get kth index.

```python
    def kthSmallest(self, root, k):
        """
        :type root: TreeNode
        :type k: int
        :rtype: int
        """
        stack = []
        
        while True:
            while root:
                stack.append(root)
                root = root.left
            root = stack.pop()
            k -= 1
            if not k:
                return root.val
            root = root.right
```
---
**`106. Construct Binary Tree from Inorder and Postorder Traversal`**🌴

- Very simple recursive solution! The last value in postorder is the root. And then next value is right root, and go on.
- So for every value in postorder we would divide the tree to root.right and root.left. See below!

```python
def buildTree(self, inorder: List[int], postorder: List[int]) -> TreeNode:
    if inorder:
        val = postorder.pop()
        index = inorder.index(val)
        root = TreeNode(val)
        root.right = self.buildTree(inorder[index+1:], postorder)
        root.left = self.buildTree(inorder[0:index], postorder)
        return root
```
---
**`Group shifted strings`**🚢
>Given an array of strings (all lowercase letters), the task is to group them in such a way that all strings in a group are shifted versions of each other.
- store each string in hashmap using key as (len,consecutive_difference)
- if key exists, append to list.
---
```python
def group_shifted(n):
    store = {}

    for word in n:
        tup = cal_dist(word)
        if tup in store:
            store[tup].append(word)
        else:
            store[tup] = [word]

    print(store)
    return store
```
---
**`Word Pattern II`**
>Given a pattern and a string str, find if str follows the same pattern.

```python
def match(self, pattern, str, r1, r2):
        if not (pattern or str):
            return True

        if not pattern and str or pattern and not str:
            return False

        char = pattern[0]
        for j in xrange(len(str)):
            substr = str[:j + 1]
            if char not in r1 and substr not in r2:
                r1[char] = substr
                r2[substr] = char

                if self.match(pattern[1:], str[j + 1:], r1, r2):
                    return True

                del r1[char]
                del r2[substr]

            elif (char in r1 and r1[char] == substr and
                    self.match(pattern[1:], str[j + 1:], r1, r2)):
                return True

        return False

def wordPatternMatch(self, pattern, str):
    r1, r2 = {}, {}
    return self.match(pattern, str, r1, r2)
```
---
**`Serialize deserialize tree`**
>Serialize and deserialize methods for tree.

```python
def serialize(self, root):
        if not root: return 'x'
        return root.val, self.serialize(root.left), self.serialize(root.right)
        # return (1, (2, 'x', 'x'), (3, (4, 'x', 'x'), (5, 'x', 'x')))

def deserialize(self, data):
    if data[0] == 'x': return None
    node = TreeNode(data[0])
    node.left = self.deserialize(data[1])
    node.right = self.deserialize(data[2])
    return node
```
---
**`House robbery DP`**
>You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.
- similar structure to coin problem, stair problem etc


```python
def get_max(nums):
            if len(nums)<=2:
                return max(nums)
        
            dp = [0]*len(nums)
            dp[0] = nums[0]
            dp[1] = max(nums[0], nums[1])
            for i in range(1, len(nums)):
                dp[i] = max(nums[i] + dp[i-2], dp[i-1])
            # print(nums, dp)
            return max(dp)
        
        return max(get_max(nums[:-1]), get_max(nums[1:]))
```
