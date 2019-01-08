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

`Day 3 - Dictionary, files`
---
- `Dict` are the hashmap of python. The keys can be of type string, numbers, tuples as they are immutable. 
	- .keys()
	- .values()
	- .items() : returns list of items [{},{},{},{}]
- `Dict formatting`
```python
hash =  {} 
hash['word']  =  'garfield' 
hash['count']  =  42 
s =  'I want %(count)d copies of %(word)s'  % hash # %d 		    
for int, %s for string  # 'I want 42 copies of garfield'
del var
del list[0]  ## Delete first element
```
- `del` deletes the definition of the variable as if the variable was never defined.
- `Files` 
	- open returns the handle to the file.
	- f.close to close the connection
	- text file can be read using for loop. Good option as not all the content is loaded into memory.
	- f.write writes the content to file.

`Day 4 - Regular expressions`
---
- `match = re.search(pat,str)`
- `match.group()` contains the matched string else None.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA0ODU3MDg0NiwzNjU5ODg0NDMsNzYzMT
QxMDg4LDE1ODg3NDMxOTgsMTU4MTUzMjYxLDE0MjM2NDk4OTQs
MzY5NjM1MjE2LDk0ODQ3MDkzNSw4Mjc2MzY3NzUsMTc0ODcyOT
E5MCwzMjU4NzUwMDJdfQ==
-->