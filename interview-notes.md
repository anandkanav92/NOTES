

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
                nums[j] = 1 #white
                j += 1
            if v == 0:
                nums[i] = 0
                i += 1

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQwNTQ1NzI2NSwyMDQwMjk3NjIyXX0=
-->