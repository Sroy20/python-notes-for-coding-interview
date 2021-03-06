If you are planning to give a coding interview in Python, remembering the information presented below will be beneficial.

## Mutable, Hashable, and Iterable

**Mutable/Immutable**: In Python, some objects are mutable, meaning they can be altered.  Others are immutable; they cannot be changed but rather return new objects when attempting to update. 

The following are some immutable objects: int, float, decimal, complex, bool, string, tuple, range, frozenset, bytes

The following are some mutable objects: list, dict, set, array.array, bytearray, user-defined classes (unless specifically made immutable)

The way I like to remember which types are mutable and which are not is that containers and user-defined types tend to be mutable while scalar types are almost always immutable. Then remember some notable exceptions: tuple is an immutable container, frozenset by definition is an immutable version of set. Strings are immutable. 

It is important to understand Mutability for writing efficient codes. For example, concatenating two strings or adding a new elemnent to a tuple creates a new object and hence is memory inefficient.

**Hashable**: An object is hashable if it has a hash value which never changes during its lifetime (it needs a __hash__() method), and can be compared to other objects (it needs an __eq__() or __cmp__() method). In addition, hashable objects which compare equal must have the same hash value.

Hashability makes an object usable as a dictionary key and a set member, because these data structures use the hash value internally.

All of Python’s immutable built-in objects are hashable, while no mutable containers (such as lists or dictionaries) are. Objects which are instances of user-defined classes are hashable by default; they all compare unequal, and their hash value is their id().

## Python Data Structures

### List

General comments: The list data structure in Python is implemented as a dynamic array.

| Operation     | Example      | Time Complexity         | Notes |
| -------------- | -------------- | --------------- | ------------------------------- |
| Index         | l[i]         | O(1)	     | |
Store         | l[i] = 0     | O(1)	     |
Length        | len(l)       | O(1)	     |
Append        | l.append(5)  | O(1)	     |
Pop	      | l.pop()      | O(1)	     | same as l.pop(-1), popping at end
Clear         | l.clear()    | O(1)	     | similar to l = []

Slice         | l[a:b]       | O(b-a)	     | l[1:5]:O(l)/l[:]:O(len(l)-0)=O(N)
Extend        | l.extend(...)| O(len(...))   | depends only on len of extension
Construction  | list(...)    | O(len(...))   | depends on length of argument

check ==, !=  | l1 == l2     | O(N)          |
Insert        | l[a:b] = ... | O(N)	     |
Delete        | del l[i]     | O(N)	     | 
Remove        | l.remove(...)| O(N)	     | 
Containment   | x in/not in l| O(N)	     | searches list
Copy          | l.copy()     | O(N)	     | Same as l[:] which is O(N)
Pop	      | l.pop(0)     | O(N)	     | 
Extreme value | min(l)/max(l)| O(N)	     |
Reverse	      | l.reverse()  | O(N)	     |
Iteration     | for v in l:  | O(N)          |

Sort          | l.sort()     | O(N Log N)    | key/reverse doesn't change this
Multiply      | k*l          | O(k N)        | 5*l is O(N): len(l)*l is O(N**2)

Note that for i in range(...) is O(len(...)); so for i in range(1,10) is O(1).
If len(alist) is N, then

  for i in range(len(alist)):

is O(N) because it loops N times. Of course even 

  for i in range (len(alist)//2):

is O(N) because it loops N/2 times, and dropping the constant 1/2 makes
it O(N).

Finally, when comparing two lists for equality, the complexity class above shows as O(N), but in reality we would need to multiply this complexity by O(==) where O(==) is the complexity class for checking whether two values in the list are ==. If they are ints, O(==) would be O(1); if they are strings, O(==) in the worst case it would be O(len(string)). This issue applies any time an == check is done.

### Tuples
Tuples support all operations that do not mutate the data structure (and with
the same complexity classes).


### Sets
                              
Operation     | Example      | Time Complexity         | Notes
--------------+--------------+---------------+-------------------------------
Length        | len(s)       | O(1)	     |
Add           | s.add(5)     | O(1)	     |
Containment   | x in/not in s| O(1)	     | compare to list/tuple - O(N)
Remove        | s.remove(5)  | O(1)	     | compare to list/tuple - O(N)
Discard       | s.discard(5) | O(1)	     | 
Pop           | s.pop()      | O(1)	     | compare to list - O(N)
Clear         | s.clear()    | O(1)	     | similar to s = set()

Construction  | set(...)     | len(...)      |
check ==, !=  | s != t       | O(min(len(s),lent(t))
<=/<          | s <= t       | O(len(s1))    | issubset
>=/>          | s >= t       | O(len(s2))    | issuperset s <= t == t >= s
Union         | s | t        | O(len(s)+len(t))
Intersection  | s & t        | O(min(len(s),lent(t))
Difference    | s - t        | O(len(t))     |
Symmetric Diff| s ^ t        | O(len(s))     |

Iteration     | for v in s:  | O(N)          |
Copy          | s.copy()     | O(N)	     |

Sets have many more operations that are O(1) compared with lists and tuples. Not needing to keep values in a specific order (which lists/tuples require) allows for faster operations.

Frozen sets support all operations that do not mutate the data structure (and with the same complexity classes).


### Dictionaries: dict and defaultdict
                            
Operation     | Example      | Time Complexity         | Notes
--------------+--------------+---------------+-------------------------------
Index         | d[k]         | O(1)	     |
Store         | d[k] = v     | O(1)	     |
Length        | len(d)       | O(1)	     |
Delete        | del d[k]     | O(1)	     |
get/setdefault| d.method     | O(1)	     |
Pop           | d.pop(k)     | O(1)	     |
Pop item      | d.popitem()  | O(1)	     |
Clear         | d.clear()    | O(1)	     | similar to s = {} or = dict()
Views         | d.keys()     | O(1)	     |

Construction  | dict(...)    | len(...)      |

Iteration     | for k in d:  | O(N)          | all forms: keys, values, items

So, most dict operations are O(1).

defaultdicts support all operations that dicts support, with the same complexity classes (because it inherits all the operations); this assumes that calling the constructor when a values isn't found in the defaultdict is O(1) - which is true for int(), list(), set(), ... (the things commonly used)

## Important Functions

1. Enumerate:

https://docs.python.org/3/library/functions.html#enumerate

1. Zip

1. Filter, map, and reduce

https://www.python-course.eu/python3_lambda.php



## Numpy - Functions to remember for Machine Learning

1. [np.multiply](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.multiply.html): Does element-wise multiplication operations of two multi-dimensional numpy arrays.
1. [np.pad](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.pad.html): For padding multi-dimensional arrays
1. [np.dot](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.dot.html)
1. [np.exp](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.exp.html)
1. [np.abs](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.absolute.html)
1. [np.log](https://docs.scipy.org/doc/numpy-1.10.4/reference/generated/numpy.log.html)
1. [np.maximum](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.maximum.html)
1. [np.shape](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.ndarray.shape.html)
1. [np.reshape](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.reshape.html)

## Function calling in Python

There are essentially three kinds of 'function calls':

Pass by value
Pass by reference
Pass by object reference

Python is a PASS-BY-OBJECT-REFERENCE programming language.

Firstly, it is important to understand that a variable, and the value of the variable (the object) are two seperate things. The variable 'points to' the object. The variable is not the object. Again:

THE VARIABLE IS NOT THE OBJECT

Example: in the following line of code:

>>> x = \[]
\[] is the empty list, x is a variable that points to the empty list, but x itself is not the empty list

Consider the variable (x, in the above case) as a box, and 'the value' of the variable ( [ ] ) as the object inside the box.

PASS BY OBJECT REFERENCE (Case in python):

Here, "Object references are passed by value."

def append_one(li):
    li.append(1)
x = \[0]
append_one(x)
print x
Here, the statement x = [0] makes a variable x (box) that points towards the object [0]

On the function being called, a new box li is created. The contents of li is the SAME as the contents of box x. Both the boxes contain the same object. That is, both the variables point to the same object in memory. Hence, any change to the object pointed at by li will also be reflected by the object pointed at by x.

In conclusion, the output of the above program will be:

\[0, 1]

Note:

If the variable li is reassigned in the function, then li will point to a seperate object in memory. x however, will continue pointing to the same object in memory it was pointing to earlier.

Example:

def append_one(li):
    li = \[0, 1]
x = \[0]
append_one(x)
print x
The output of the program will be:

\[0]

PASS BY REFERENCE:

The box from the calling function is passed on to the called function. Implicitly, the contents of the box (the value of the variable) is passed on to the called function. Hence, any change to the contents of the box in the called function will be reflected in the calling function.

PASS BY VALUE:

A new box is created in the called function, and copies of contents of the box from the calling function is stored into the new boxes.

List comprehension with only if statement or if/else statement:

[ expression for item in list if conditional ] 
but that's actually not what you do in this case. (I was trying to do it that way)

In this case, it's more like this:

[ expression if conditional else other thing for this many times ] 


