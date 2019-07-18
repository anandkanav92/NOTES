

Sort Colors
---

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
 
Simplify Path
---

> Given an **absolute path** for a file (Unix-style), simplify it. Or in other words, convert it to the **canonical path**.

1. Use stack to store the directories.
2. If `..` found pop the directory from stack.
3. Ignore everything else.
 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY2NjMwNjc1NiwtMjUxOTgzMDQ3LDIwND
AyOTc2MjJdfQ==
-->