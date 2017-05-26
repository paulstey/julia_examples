# 1 Vectors Matrices and N-Dimensional Arrays
- All of these are native to Julia
- Behave much like their counterparts in Python (NumPy), R, and Matlab

---
## 1.1 Vectors
- Vectors in Julia are 1-dimensional Arrays
- Arrays are simply containers
- Therefore, vectors (and arrays) can store any type of object; for example:
    * Int, Float64, String
    * Array, Dict, Function
    * user-defined types
---
Consider some simple vector objects:
```Julia
v = [4, 5, 6]

u = [4.2, 5.6, 7.6]

w = ["dog", "cat", "shoe"]
```

---
### 1.1.1 Initializing and Growing Vectors
```Julia
a = Int[]               # initialize empty vector of Ints

a2 = Vector{Int}()      # identical to above

a3 = Array{Int, 1}()    # also identical
```
---
### 1.1.2 Growing a vector "in place"
```julia
push!(a, 999)

push!(a, 1000)

append!(a, [4, 8, 15, 16, 23, 42])
```
