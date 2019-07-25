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
	9. Elgantly fix your bug.
	10. Comment on run and space complexity.
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
`TREES`

```
1. Node with no children -> Leaves.
2. Nodes with same parents -> Siblings.
3. Number of edges from root to node -> Depth of node.
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbOTIxNTQ0MjksLTQxMDQ1MTIwNiwtMTY0Mj
M5MzkxOCwxMjUyNzMxOTY3LDE2NDczNzgzMDYsNTIyMjkxNTEs
MTA2ODYzNDU3MywxODUzNzAxNzMwLC0zOTc5MzUyNzksLTE5ND
kyMzYzODUsLTIxMDcxNTgzNjgsMTgwNTYyMTMzMCwyMDMxNjA0
NDY5LC0xNDA3NDIwMTI4LC0xMTE0NTkwODk4LC0xNDk0NzkxMz
QsLTY2NjMwNjc1NiwtMjUxOTgzMDQ3LDIwNDAyOTc2MjJdfQ==

-->