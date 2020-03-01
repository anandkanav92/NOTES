# System Design
`Steps to approach system design problem`
---
1. `feature extraction (2mins)`:
  -   It is extremely important hence to get a very clear understanding of whats the requirement for the question.
2. `Estimations ( 2-5 mins )`:
  - Next step is usually to estimate the scale required for the system. The goal of this step is to understand the level of sharding required ( if any ) and to zero down on the design goals for the system. 
  - For example, if the total data required for the system fits on a single machine, we might not need to go into sharding and the complications that go with a distributed system design. 
  - OR if the most frequently used data fits on a single machine, in which case caching could be done on a single machine.
3. `Design Goals ( 1 mins )`
  - Figure out what are the most important goals for the system. It is possible that there are systems which are latency systems in which case a solution that does not account for it, might lead to bad design. 
4. `Skeleton of the design ( 4 - 5 mins )`
  - A good strategy is to discuss a very high level with the interviewer and go into a deep dive of components as enquired by the interviewer. 
5. `Deep dive ( 20-30 mins )`

`Key outcomes of a good system design`
---
1. Resilient : shouldn't lose data, no single point of failure.
2. more inter process communincation and less over the network.
3. Consistency. The data should be consistent. Atomic operations help in rebuilding the data.
4. should scale well, horizontal scaling.

 
     
`scalability talk for websites` [link](https://www.youtube.com/watch?v=-W9F__D3oY4&list=PLmhRNZyYVpDmLpaVQm3mK5PY5KB_4hLjE&index=10)
---
1. cores are like multiple brain inside single chip. Quad core means, computer can perform 4 operations at once in parallel without considering context switching schduling algorithms.
2. Load balancers helps distribute the load on your website to different servers. DNS can have only one IP and other server IP would be private and that makes it a bit secure. 
3. Load balancer can work on multiple heuristics or just simple round robin.

`gaurav sen sharding`
---
1. sharding is dividing your databases over multiple servers based on a certain condition(like userid, or location).
2. problems : 
  - Join over network between servers 
  - consistency
3. use master slave architecture where master is for write operations and slave can be used to handle read requests
4. go for indexing -> nosql and then sharding as it is very complex

`Bloomfilter`
---
1. it is used to check if an item definitely does not exist or may be exists.
2. k hash functions (murmur and not crypto), m bits to represent data and n items already inserted determine the false positive that an item might exist. 
3. Bigger the bloom filter size(m), lower the false positive. 
4. Higher the cache functions, lower false positive but more time.
5. used by: google big table to check if a data exists before disk lookup.** 

# Algorithms
 `tips`
 ---
	1. Ask questions.
	2. Provide high level approach
	3. Ask if runtime complexity is okay?
	4. Code as modular as possible.
	5. Dry run on complicated example.
	6. Understand where the bug is coming from and then fix it properly.
	7. Do one more dry run.
	8. Test your code by adding edge cases.
	9. Elegantly fix your bug.
	10. Comment on run and space complexity.
	11. The time complexity of any recursive solution is always dependent upon what variables define its state and if that state is cached or not and also the computation taking place per recursive call.
---
`Sort Colors`


> Given an array with _n_ objects colored red, white or blue, sort them **[in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** so that objects of the same color are adjacent, with the colors in the order red, white and blue.

 1. store count for each color and ezpz
 2. tricky is to do in one pass with no extra space
 `Awesome Solution below`
```python
 def sortColors(self, nums):
        red = white = 0
        for k in range(0,len(nums)):
            current = nums[k]
            nums[k] = 2 #blue
            if v < 2:
                nums[white] = 1 #white
                white += 1
            if v == 0:
                nums[red] = 0 #red
                red += 1
```
 ---
`Simplify Path`


> Given an **absolute path** for a file (Unix-style), simplify it. Or in other words, convert it to the **canonical path**.

 1. Use stack to store the directories.
 2. If `..` found pop the directory from stack.
 3. Ignore everything else.
 
---
`Subsets`
> Find all the **distinctive** subsets of the given array.
1. Start with empty set.
2. For each element in array, form a subset with already existing subsets.
3. Append it to subset list.

```python
if nums is None: 
	return None
subsets = [[]] 
next = [] 
for n in nums:
	for s in subsets:
		next.append(s + [n])
	subsets += next
	next = []
return subsets
```

---
`python is pass by object reference`
```python
a = [] #a is not empty list
#a is the variable referring to empty list
```
1. Python passes a reference as value. So if a is passed to a function, it will create a new reference and pass it. 
2. If there are update changes made in the function, it will be shown in the original variable.
3. If the variable is assigned with new values, it detaches from initial object and the changes are no longer replicated to original variable.
---
`Word Search [DFS]`
> Given a 2D board and a word, find if the word exists in the grid. Use one letter only once.

```python
#recursive function for each char
def check_match(hor,ver,word,x,y,current,state):
    if hor>=x:
        return False
    if ver>=y:
        return False
    if hor<0 or ver<0:
        return False
    # print("{} board {} word {}".format(state,state[hor][ver],word[current]))

    if state[hor][ver]==word[current]:
        state[hor][ver] = '-1'
        if len(word) == current+1:
            return True
        else:
            
            if check_match(hor+1,ver,word,x,y,current+1,state):
                return True
            if check_match(hor,ver+1,word,x,y,current+1,state):
                return True
            if check_match(hor,ver-1,word,x,y,current+1,state):
                return True
            if check_match(hor-1,ver,word,x,y,current+1,state):
                return True 
        
        state[hor][ver] = word[current]
        return False
#main function
x = len(board)
for i in range(0,x):
    y = len(board[i])
    for j in range(0,len(board[i])):
        if check_match(i,j,word,x,y,0,board):
            return True
return False
        
```
1. For each char in 2-d list, check if the first word matches. If it does, start a search party checking all the adjacent elements for the next word.
2. The search party will check 4 locations - right, left, botoom and top. 
3. If there is a match move ahead and update the path with '-1' to prevent matching same char again.
4. Return true if complete word is matched.
5. python being `call by object reference value` makes it difficult to manage the state of last visited variables. That's why update after every move the original values. (Cover your tracks)
6. RUNTIME: $$O(N*M*4^K)$$ where n is row size, m is column size and K is word size.

---
`Increasing Triplets`
> Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

```python
first = second = float('inf')
for n in nums:
    if n<=first:
        first = n
    elif n<=second:
        second = n
    else:
        return True
return False
```
1. MindBoggling :O
2. Start with inf as first and second element in the list.
3. Add the first min as first and second min as second.
4. return true if found an element greater than both.
5. `Gist`: We only replace second element as when there is a smaller second min element available. When we replace first, the order breaks. But if the new element is bigger than the second min element, it is greater than the previous first element for sure. Thus, return true.
6. If we want to keep track of triplets, store the last first min when replacing the first min and breaking the order. 

---
`Max agents required`
> We have x number of agents attending to calls. Given a 2-d list with start and end times of calls, find how many more hiring is required #booking

	1. Sort the start and end time seperately.
	2. Compare start and end time.
	3. if start is smaller than end, increment start and the number of person required at that moment.
	4.  if start is greater, that means new range is starting. Thus, increment end and decrement the count. Keep a record of max count globally.
---
`Remove Duplicates from Sorted Array II`
>Given a sorted array  _nums_, remove the duplicates  **in-place** such that duplicates appeared at most _twice_  and return the new length.
```python
if nums is None:
   return None
n = len(nums)
if n<3:
   return n
index, current, start,second = 1,1,nums[0],0
while index<n:
   if start != nums[index]:
       start = nums[index]
       nums[current] = nums[index]
       current += 1
       second = 0
   else:
       if second == 0:
           second=1
           nums[current] = nums[index]
           current+=1
   index+=1
return current
```

 1. check length of the array and return if less than 3.
 2. use two pointer approach. stop incrementing start after two duplicates of same variable. return the counter in the end.
---
`merge sorted arrays`
> Given two sorted arrays, merge them.
```python
m, n = m-1, n-1
while m >= 0 and n >= 0:
    if nums1[m] > nums2[n]:
        nums1[m+n+1] = nums1[m]
        m -= 1
    else:
        nums1[m+n+1] = nums2[n]
        n -= 1
if n != -1: # nums2 is still left
    nums1[:n+1] = nums2[:n+1]
```
 1. Start from last element of both arrays. Put the biggest element in the end and decrement count from the array with the biggest number.
 2. Repeat until the counter goes below 0.
 3. Push all the elements from num2 array to num1 in case there are still remaining.

---
**`Word Search`**
> Given a 2D board and a list of words from the dictionary, find all words in the board.

1. Create a trie data structure to store the list of words so that similar prefix are not checked multiple times.
2. Starting with the root node. 
	- For each children, call DFS.
	- If there is a match, go deeper.
	- check for word end, and if there is a word end add it to result list. 
	- Four directions to explore, and update the root position with '#' to prevent reusing characters twice.
3. Repeat for each character in the 2-d board.
```python
class TrieNode():
    def __init__(self):
        self.children = collections.defaultdict(TrieNode)
        self.isWord = False
    
class Trie():
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word):
        node = self.root
        for w in word:
            node = node.children[w]
        node.isWord = True
    
    def search(self, word):
        node = self.root
        for w in word:
            node = node.children.get(w)
            if not node:
                return False
        return node.isWord
    
class Solution(object):
    def findWords(self, board, words):
        res = []
        trie = Trie()
        node = trie.root
        for w in words:
            trie.insert(w)
        for i in xrange(len(board)):
            for j in xrange(len(board[0])):
                self.dfs(board, node, i, j, "", res)
        return res
    
    def dfs(self, board, node, i, j, path, res):
        if node.isWord:
            res.append(path)
            node.isWord = False
        if i < 0 or i >= len(board) or j < 0 or j >= len(board[0]):
            return 
        tmp = board[i][j]
        node = node.children.get(tmp)
        if not node:
            return 
        board[i][j] = "#"
        self.dfs(board, node, i+1, j, path+tmp, res)
        self.dfs(board, node, i-1, j, path+tmp, res)
        self.dfs(board, node, i, j-1, path+tmp, res)
        self.dfs(board, node, i, j+1, path+tmp, res)
        board[i][j] = tmp
```   

---
`TREES`

```
1. Node with no children -> Leaves.
2. Nodes with same parents -> Siblings.
3. Number of edges from root to node -> Depth of node.
4. Height of the node = number of edges from node to deepest leaf.
5. Height of tree = Height of root.
```

`General trees - used for file system`
```java
public class  TNode  {

	private  Object data;

	private  MyLinkedList  siblings;

	private  TNode  myLeftChild;
	
	public  TNode(Object n){
		data=n; 			 	
		siblings=NULL;
		myLeftChild=NULL;
	}
}
```
`Binary trees`
```java
public class BNode

{

   private Object data;

   private BNode left, right;

   public BNode()

   {

      data=left=right=null;

   }

   public BNode(Object data)

   {

      this.data=data;

      left=right=null;

   }

}
```
1. Full binary tree = All nodes have exactly 0 or 2 child.
2. Complete tree = **A complete binary tree** is a tree, which is completely filled, with the possible exception of the bottom level, which is filled from left to right. A complete binary tree of the height h has between 2h and 2(h+1)-1 nodes.

`BST - Binary search trees`

> A binary search tree (BST) is a tree, where inorder traversal is an ordered sequence.
1. BSTs are used in cases where data needs to be retrieved often and in a sorted sequence.
2. The **left** subtree has all the values **less** than the key.
3. The **right** subtree has all the values **greater** than the key.
4. **Duplicate** keys are not allowed.

`BFS`
> Breadth first search also known as level first search uses queues. Add a vertex to queue. Next, add all the children to queue. Repeat. If it is a graph, check for visited flag.


`AVL trees`
>BST is highly used for search. They provide logn(n) search time but only if balanced. In order to keep it balanced, we follow AVL algorithm.
```
1. A tree is said to be unbalanced if any node has (left subtree height - right subtree height) not belnoging to the set {-1,0,1}.
2. If the unbalance is caused due to an addition of node on left and left subtree, it is called `l-l balance` and it is rebalanced using ll rotation.
3. If the unbalance is caused due to an addition of node on left and right subtree, it is called `l-R balance` and it is rebalanced using LR rotation.
4. LR rotation is a double rotation. That means there are two steps involved - one to left and then to the right. Any rotation involved just involves 3 nodes at a time.
```
---
`Course Schedule II` **`TOPOLOGICAL SORT`**
>There are a total of  _n_  courses you have to take, labeled from  `0`  to  `n-1`.
Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair:  `[0,1]`
Given the total number of courses and a list of prerequisite  **pairs**, return the ordering of courses you should take to finish all courses.
5.  For each of the nodes in our graph, we will run a depth first search in case that node was not already visited in some other node's DFS traversal.
6.  Suppose we are executing the depth first search for a node  `N`. We will recursively traverse all of the neighbors of node  `N`  which have not been processed before.
7.  Once the processing of all the neighbors is done, we will add the node  `N`  to the stack. We are making use of a stack to simulate the ordering we need. When we add the node  `N`  to the stack, all the nodes that require the node  `N`  as a prerequisites (among others) will already be in the stack.
8.  Once all the nodes have been processed, we will simply return the nodes as they are present in the stack from top to bottom.
```python
from collections import defaultdict
class trie:
    def __init__(self):
        self.child = []
        self.visited = False
class Solution:
    
            
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        
        def sortData(data_store,current,result,cycle):
            if cycle[0] == True:
                return
            data_store[current].visited = True
            for element in  data_store[current].child:
                if data_store[element].visited == False:
                    sortData(data_store,element,result,cycle)
                else:
                    cycle[0] = True
                    return
            # print(cycle)
            data_store[current].visited = False
            if current not in result:
                result.append(current)
            return
                
            
        
        
        if numCourses<=1:
            return [0]
        
        
        data_store = defaultdict(trie)
        for element in prerequisites:            
            data_store[element[1]].child.append(element[0])
        result = []
        cycle = [False]
        print(data_store)

        for index in range(numCourses):
            if index not in result:
                sortData(data_store,index,result,cycle)
                
        print(result)
        if cycle[0]==True:
            return []
        return result[::-1]
        
```
---
`Lowest Common Ancestor of a Binary Tree`

>  Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.
 1.  Start traversing the tree from the root node.
 2.  If the current node itself is one of  `p`  or  `q`, we would mark a variable  `mid`  as  `True`  and continue the search for the other node in the left and right branches.
3.  If either of the left or the right branch returns  `True`, this means one of the two nodes was found below.
4.  If at any point in the traversal, any two of the three flags  `left`,  `right`  or  `mid`  become  `True`, this means we have found the lowest common ancestor for the nodes  `p`  and  `q`. 

```python
def local(root,p, q):
   if root is not None:
       mid = (root.val == p.val or root.val == q.val)
       if mid==True:
           self.ans = root
           return mid
       left = local(root.left,p,q)
       right = local(root.right,p,q)
       if (mid and right) or (mid and left) or (left and right):
           self.ans = root
       return (left or mid or right)
```
---
**`Find all ANAGRAMS`** 
> Given a string  **s**  and a  **non-empty**  string  **p**, find all the start indices of  **p**'s anagrams in  **s**.
 1. Use sliding window method.
 2. Two maps, one for count of pattern and one for sliding window of size p.
 3. After each iteration, include the end and remove the start variable to slide the window.
 4. O(K * 26) [as fixed size of characters]  
 
 ```python
 while end < len(s):
	if is_anagram(pattern,window):
	     result.append(start)
	window[s[start]] = window[s[start]] - 1
	start = start+1
	end = end+1
	if end<len(s):
	    window[s[end]] = window[s[end]] + 1
```

---
**`Next Permutation`**
> Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers. If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).
 
 ![](resource/next_permutation.gif)

 1. Find the decreasing element in the list from right to left.
 2. Replace the decreasing element with the number just greater to the element going left to right.
 3.  Reverse the list starting from the decreased element.

 ```python
    n = len(nums)
    left,right = n-2,n-1
    while left>=0:
        if nums[left]<nums[right]:
            break
        else:
            left = left-1
            right = right-1
    if left<0:
        reverse(nums,0,n-1)
        return nums
    decreasing = left
    diff = nums[decreasing+1]-nums[decreasing]
    diff_index = decreasing+1
    for index in range(decreasing+2,n):
        local_diff = nums[index]-nums[decreasing]
        if local_diff<=diff and local_diff>0:
            diff = local_diff
            diff_index = index
    nums[decreasing],nums[diff_index] = nums[diff_index],nums[decreasing]
    reverse(nums,decreasing+1,n-1)
    return nums
 ```


 ---
 **`Reverse Nodes in k-Group (HARD)`** 🙀
>Given a linked list, reverse the nodes of a linked list k at a time and return its modified list. k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

1. there are 3 main parts to this problem 3️⃣
  - validate if we need to reverse by checking if the remaining nodes are greater than k 1️⃣
  - reverse the given k nodes as a group using the code. 2️⃣
    ```python
      def reverse(prev,curr, k):
            last_head = curr
            while  k:
                temp = curr.next
                curr.next = prev
                prev = curr 
                curr = temp
                k -=1 
            return last_head, curr,prev
    ```
  - update the pointers correctly. 3️⃣
    
    ```python
      #original ll : 1->2->3->4->5 and k=2
      new_tail,now,prev = reverse(None, now, k)
      #prev is always none. So each group returns 2->1->NONE
      new_tail.next = now    
      #new tail is the tail of reversed group and it should point to the head of next group
      prev_tail.next =  prev
      #prev tail earlier was pointing to head( now tail). so it is updated to point at new head
      prev_tail = new_tail
      #new tail becomes previous so that the connection is updated for the next group as new tail right now points at 3 where as it should be updated to point at 4 after reversing
    ```
      

---
 **`search in rotated sorted array`** ♻️
> Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand. (i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]). You are given a target value to search. If found in the array return its index, otherwise return -1

- use modified binary approach.
  + use l,m,h to store low, medium and high.
    + return m if `target==m` 
    + if `l < m`, that means its only increasing without dip. So if a target is not in between `l and m` then forget this prt of array.
    + similar check for `m and h` as this checking order matter before moving on to new condition.
    + if `l>m`, then there is a dip in this part of array and it needs to be checked. As the dip can be only in one part of array and we have checked both part every time for increasing sequence, we can be sure either the element is here or it is not in the array itself.
    + similar condition for `m<h`.
    + if it doesn't go in any loop, `return -1`

`Code`
```python
while l<=h:
            # print("{} {} {}".format(l,m,h))
  if nums[m] == target:
      return m
  
  if l==h and l != target:
      return -1
  
  if nums[l] < nums[m] and target <= nums[m] and target >= nums[l]:
      l = l
      h = m - 1
      m = (l + h)//2
      continue
  
  if nums[m] < nums[h] and target <= nums[h] and target >= nums[m]:
      h = h
      l = m + 1
      m = (l + h)//2
      continue
  
  if nums[l] > nums[m]:
      l = l
      h = m -1
      m = (l + h)//2
      continue
  
  if nums[m] > nums[h]:
      l = m + 1
      h = h
      m = (l + h)//2
      continue
  
  return -1
                        
return -1
```

---
 **`validate the sudoko or how to iterate a 2-d matrix in 3v3 grid`** 💮
 > given a 2-d matrix, validate the sudoko. That is, if rows columns and 3v3  grid contain unique elements between 1-9.
 
 - iterate over 3v3:
   + outer loop with steps of 3 in both x and y direction
   + inner loop starting at x, with steps of 1 and ending after 3 iterations in both x and y directions.

```python
  #loop in 3v3 grid
  for x in range(0,9,3):
    for y in range(0,9,3):
      storage = clearDict(storage)
      for i in range(x,x+3):
        for j in range(y,y+3):
          print("{} {} ".format(i,j))
          if board[i][j] == ".":
            continue
          if storage[int(board[i][j])] == 0:
            storage[int(board[i][j])] = 1
          else:
            print("{} {} {} {} ".format(i,j,board[i][j],storage))
            return False
```

---
 **`combination sum`** 📡
 > Given a set of candidate numbers (candidates) (without duplicates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

- two major functions required to solve the problem
  + sorting the array lets us go in one direction without worrying about combinations with previous elements
  + next we loop over every element and every possible combination with forward elements. If target == 0, then add to `result`otherwise, target > 0, try with same element and the next possible elements.

```python
def storeResults(candidates,target,index,current,result):
  # print("target {} index {}".format(target,index))

  target = target - candidates[index]
  if target == 0:
      current.append(candidates[index])
      result.append(current)
      print("{}".format(result))
      return
  
  if target < 0:
      return
  current = current + [candidates[index]]
  for index in range(index,len(candidates)):
      storeResults(candidates,target,index,current,result)
  # if index < len(candidates)-1:
  #     storeResults(candidates,target,index+1,current,result)
  # current = []
  # print("current {} final return {}".format(current,result))
  return result

result = []
current = []
index = 0
candidates = sorted(candidates)
for index in range(0,len(candidates)):
  final = storeResults(candidates,target,index,current,result)
return result

```
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

