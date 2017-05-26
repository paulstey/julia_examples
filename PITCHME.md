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

---

## 2 Vectors (1-D `Array`s)
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

append!(a, [4, 8, 15])  # appends vector to tail
```

---

### 2.1.2 Types Matter
Julia has a very explicit type system (more on this later), so some caution is required
```julia
v = [4, 5, 6]

push!(v, 3.14)     # Fails (Matlab casts all elements)
```

---

### 2.1.3 Pre-Allocating Vectors
- In general, it's preferable to pre-allocate your arrays
- Has performance implications
- Growing a vector in place is usually 2 operations versus 1 for assignment only
- Also has the advantage of forcing you to think more about your code
    * In a sense, it's self-documenting code

+++

```julia
x1 = zeros(4)               # default is Float64

x2 = zeros(Int, 10)

x3 = falses(5)

x4 = trues(4)
```

---

### 2.1.4 Indexing a Vector
- Identical to R's behavior
- Nearly identical to Matlab, but use `[` instead of `(`
- Note that Julia uses 1-based indexing

```julia
s = ["this", "is", "a string vector"]

s[2]                # gets second element

s[3] = "shoe"       # set third element to "shoe"

s[end]              # gets last element

s[end - 1]          # gets 2nd to last element
```

+++

Can also index with boolean values

```julia
v1 = [4, 5, 6]

v[[true, false, true]]      # gets first and third element
```

+++

This has advantages for doing equality and inequality comparisons
```julia
v2 = [5, 6, 7, 8]

keep_elem = v2 .> 6

v2[keep_elem]               # returns [7, 8]
```

---

### 2.1.5 Slicing and Subsetting Vectors
```julia
v = [5, 6, 7, 8]

v[1:2]              # gets first 2 elements

v[3:end]            # gets elements 3 and 4
```

+++

```julia
x = ["dog", "cat", "bird", "potato"]

animal_indcs = [1, 2, 3]

animals = x[animal_indcs]
```

---


### 2.1.6 Concatenating Vectors
```julia
x1 = [4, 5, 6]

x2 = [55, 66, 77]

x3 = [x1; x2]               # x3 is concatenation of x1 and x2

x3b = vcat(x1, x2)          # exactly the same as above
```

---


### 2.2.1 Element-Wise Operations
Element-wise operations in Julia are performed using the `.` operator, which is often called the "broadcasting" operator.

```julia
a = [3, 4, 3, 6]

a .== 3             # returns [true, false, true, false]

a .> 4              # return [false, false, false, true]
```

---

## 3 Matrices (2-D `Array`s)
Matrices in Julia are just 2-dimensional arrays, and have many of the same behaviors as vectors (i.e., 1-dimensional arrays)
```julia
a = zeros(5, 3)              # 5-by-3 matrix

a2 = Array{Float64}(5, 3)    # same as above

b = [2 3 4;
     5 6 7;
     4 9 1]                  # semi-colon denotes end of row  
```

---

### 3.1.1 Indexing and Slicing Matrices
```julia
a = randn(3, 3)       # matrix of random values from standard normal dist'n

a[3, 1]               # gets element in third row first column

a[2, :]               # gets all of second row

a[:, 1]               # gets all of first column

a[:, 2] = 999.0       # assigns 999 to all of 2nd column
```

---

## 4 Reading and Writing Data to Files
The `readdlm()` and `writedlm()` function are used for reading and writing plain-text files in a delimited format. They are easy to use and flexible.


### 4.1.1 Using `readdlm()` and `writedlm()` for Plaintext
```julia
a = randn(100, 100)

writedlm("gaussian_mat.csv", a, ',')

a2 = readdlm("gaussian_mat.csv", ',')
```

---

### 4.1.2 JLD.jl Package for Binary Data Format
The JLD package can be used for saving objects from your Julia session in to binary objects, similar to HDF5.
```julia

using JLD

a = rand(10, 10)

b = [1,3]

save("myfile.jld", "a_mat", a)

d = load("myfile.jld")
```

+++

The JLD package can also save multiple objects in one call to `save()`
```julia
a = rand(10, 10)

b = [1,3]

save("myfile.jld", "a_mat", a, "b_vec", b)

d = load("myfile.jld")
```

---

### 5 Functions
