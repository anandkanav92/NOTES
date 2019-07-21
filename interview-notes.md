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

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM5NzkzNTI3OSwtMTk0OTIzNjM4NSwtMj
EwNzE1ODM2OCwxODA1NjIxMzMwLDIwMzE2MDQ0NjksLTE0MDc0
MjAxMjgsLTExMTQ1OTA4OTgsLTE0OTQ3OTEzNCwtNjY2MzA2Nz
U2LC0yNTE5ODMwNDcsMjA0MDI5NzYyMl19
-->