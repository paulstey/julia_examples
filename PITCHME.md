## 1 Using Julia
There are at least 4 ways of using Julia
- Interactive session (i.e., REPL)
    * fast, simple
    * not particularly featureful

+++
- Atom text editor with Juno plug-ins
    * plot window  
    * workspace viewer
    * more like an IDE     

+++
- Running scripts as "executables"
    * Useful for log-running jobs
    * Also advantages for reproducibility

+++
- Using Julia kernel in Jupyter
    * Nice integrated workbook view
    * In line plots
    * Support for Markdown and LaTeX
    * All the advantages of Jupyter



## 2 Vectors Matrices and N-Dimensional Arrays
- All of these are native to Julia
- Behave much like their counterparts in Python (NumPy), R, and Matlab

---
### 2.1 Vectors
- Vectors just are 1-dimensional `Array`s
- Arrays are simply containers
- Therefore, vectors (and arrays) can store any type of object; for example:
    * Int, Float64, String
    * Array, Dict, Function
    * user-defined types

+++

Consider some simple vector objects:
```Julia
v = [4, 5, 6]

u = [4.2, 5.6, 7.6]

w = ["dog", "cat", "shoe"]
```

---

### 2.1.1 Initializing and Growing Vectors
```Julia
a = Int[]               # initialize empty vector of Ints

a2 = Vector{Int}()      # identical to above

a3 = Array{Int, 1}()    # also identical
```

+++


```julia
push!(a, 999)

push!(a, 1000)

append!(a, [4, 8, 15, 16, 23, 42])  # append new vector to tail
```


### 2.1.2 Types Matter
Julia has a very explicit type system (more on this later), so some caution is required
```julia
v = [4, 5, 6]

push!(v, 3.14)          # Fails (Matlab casts all elements)
```

---

### 2.1.3 Pre-Allocating Vectors
- In general, it's preferable to pre-allocate your arrays
- Has performance implications
- Growing a vector in place is usually 2 operations versus 1 for assignment only
- Also has the advantage of forcing you to think more about your code
    * In a sense, it's self documenting your code

+++

```julia
x1 = zeros(4)               # default is Float64

x2 = zeros(Int, 10)

x3 = falses(5)

x4 = trues(4)
```

### 2.1.4 Indexing a Vector
- Identical to R's behavior
- Nearly identical to Matlab, but use `[` instead of `(`
- Note that Julia uses 1-based indexing

```julia
s = ["this", "is", "a string vector"]

s[2]                # gets second element

s[3] = "shoe"       # set third element to "shoe"
```
