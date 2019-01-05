`Day 1 - strings`
---
- immutable - once created cannot be changes
- unlike java, python doesn't convert variable to string when used with `+` operator. Use `str` instead.
- A raw string can be specified `raw = r'this\t\n and that'  will print this\t\n and that`
- The slice `s[start:end]` is the elements beginning at start and extending up to but not including end.

` Day 2 - list,sorting,tuples`
---
- The "empty list" is just an empty pair of brackets [ ]. The '+' works to append two lists, so [1, 2] + [3, 4] yields [1, 2, 3, 4] (this is just like + with strings).
- `=` operator doesn't create two different lists but make a new pointer. Thus any updates are reflected in both variables.
- The `range(n)` function yields the numbers 0, 1, ... n-1, and range(a, b) returns a, a+1, ... b-1 -- up to but not including the last number.
- `Custom Sorting With key=` The key function takes one value and returns a proxy value. The sorting is based on this proxy value. Example : with a list of strings, specifying key=len (the built in len() function) sorts the strings by length, from shortest to longest
- `List Comprehensions` squares =  [ n * n for n in nums ] = [1, 4, 9, 16]
- `Tuples` are like but immutable. tuple = (1,'x','y') is a tuple and each element can be accesed as tuple[0] #1. But tuple[0]=2 is wrong. To update, we need to reassign the complete tuple i.e (2,'x',y').

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU4MTUzMjYxLDE0MjM2NDk4OTQsMzY5Nj
M1MjE2LDk0ODQ3MDkzNSw4Mjc2MzY3NzUsMTc0ODcyOTE5MCwz
MjU4NzUwMDJdfQ==
-->