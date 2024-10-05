### <span style="color:#c6554f">Numpy</span>

A numpy array or ND array is similar to a list. It's usually fixed in size and each element is of the same type

The array object in NumPy is called **ndarray**, it provides a lot of supporting functions that make working with ndarray very easy.

```python
import numpy as np

# Create a 1D array
arr_1d = np.array([3.1, 11.02, 6.2, 213.2, 5.2]) 
```

- `np.array()` --> used to create NumPy arrays

```python
# Print each element

print("a[0]:", a[0])
print("a[1]:", a[1])
print("a[2]:", a[2])
print("a[3]:", a[3])
print("a[4]:", a[4])
```

`print(np.__version__)` --> check the NumPy version

`type(a)` --> to obtain the type of an array

`a.dtype` --> attributed used to obtain the data type of the array’s elements

`c[4] = 0` --> assign the 5th element to 0

<strong style="color: #3588E9">Creating 2D array</strong>

```python
# Creating a 2D array
arr_2d = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
```

<h5><span style="color: #3588E9">Slicing</span></h5>
Like lists, we can slice the numpy array. Slicing in python means taking the elements from the given index to another given index.

Consider the following list:

```python
arr_1d = np.array([20, 1, 2, 3, 4])
```

```python
# Indexing and slicing
print(arr_1d[2])          # Accessing an element (3rd element)
```

Slice is passed like this: `[start:end]`. The element at end index is not being included in the output.

```python
# Slicing the numpy array
d = arr_1d[1:4] # Accessing an element (1st row, 4rd column)
```

Assign the corresponding indexes to new values as follows:

```python
# Set the fourth element and fifth element to 300 and 400
arr_1d[3:5] = 300, 400
```

It's also possible to define the steps in slicing: `[start:end:step]` 

```python
arr_1d = np.array([1, 2, 3, 4, 5, 6, 7])
print(arr_1d[1:5:2])
```

If start isn't passed its considered 0

```python
print(arr_1d[:4])
```

Slicing a 2D array: 

```python
print(arr_2d[1]) # Accessing a row (2nd row)
```

```python
print(arr_2d[:, 1]) # Accessing a column (2nd column)
```
<h5><span style="color: #3588E9">Assign Value with List</span></h5>
A list can be used to select more than one specific index. The list `select` contains several values:

```python
# Create the index list
select = [0, 2, 3, 4]
```

The list can be used as an argument in the brackets. The output is the elements corresponding to the particular indexes:

```python
# Use List to select elements
d = c[select]
```

The specified elements can be assigned to a new value:

```python
# Assign the specified elements to new value
c[select] = 100000
```

<h5><span style="color: #3588E9">Other Attributes</span></h5>

```python
# Create a numpy array
a = np.array([0, 1, 2, 3, 4, 5])
```

`size` --> Provides the total number of elements in the array.
- `a.size` --> get the size of numpy array

`ndim` --> Represents the number of dimensions or "rank" of the array.
- `a.ndim` --> get the number of dimensions of numpy array

`shape` --> Returns a tuple indicating the number of rows and columns in the array.
- `a.shape` --> get the shape/size of numpy array

<h5><span style="color: #3588E9">NumPy Statistical Functions</span></h5>

```python
# Create a numpy array
a = np.array([1, -1, 1, -1])
```

```python
# Get the mean of numpy array
mean = a.mean()
```

```python
# Get the standard deviation of numpy array
standard_deviation=a.std()
```

```python
# Create a numpy array
b = np.array([-1, 2, 3, 4, 5])
```

```python
# Get the biggest value in the numpy array
max_b = b.max()
```

```python
# Get the smallest value in the numpy array
min_b = b.min()
```

<h5><span style="color: #3588E9">Numpy Array Operations</span></h5>
Arithmetic operators could be used directly between NumPy arrays

<strong  style="color: #3588E9">Array Addition</strong>

```python
# Array addition
# Array addition
array1 = np.array([1, 2, 3])
array2 = np.array([4, 5, 6])
result = array1 + array2
print(result)  # [5 7 9]
```

Using the `add` method:

```python
# Numpy Array Addition
z = np.add(array1, array2)
```

<strong  style="color: #3588E9">Array Subtraction</strong>

```python
a = np.array([10, 20, 30])

b = np.array([5, 10, 15])
```

```python
c = np.subtract(a, b)
print(c)
```

<strong  style="color: #3588E9">Array Multiplication</strong>

```python
# Create a numpy array
x = np.array([1, 2])
```

```python
# Create a numpy array
y = np.array([2, 1])
```

```python
# Numpy Array Multiplication
z = np.multiply(x, y)
```

<strong  style="color: #3588E9">Array Division</strong>

```python
a = np.array([10, 20, 30])
```

```python
b = np.array([2, 10, 5])
```

```python
c = np.divide(a, b)
```

<strong  style="color: #3588E9">Scalar multiplication</strong>

```python
# Scalar multiplication
array = np.array([1, 2, 3])
result = array * 2 # each element of an array is multiplied by 2
print(result)  # [2 4 6]
```

<strong  style="color: #3588E9">Element-wise multiplication (Hadamard Product)</strong>

```python
# Element-wise multiplication (Hadamard product)
array1 = np.array([1, 2, 3])
array2 = np.array([4, 5, 6])
result = array1 * array2
print(result)  # [4 10 18]
```

<strong  style="color: #3588E9">Matrix multiplication</strong>

```python
# Matrix multiplication
matrix1 = np.array([[1, 2], [3, 4]])
matrix2 = np.array([[5, 6], [7, 8]])
result = np.dot(matrix1, matrix2)
print(result)
# [[19 22]
#  [43 50]]
```

<strong  style="color: #3588E9">Dot Product</strong>

The dot product is a single number given by the following term and represents how similar two vectors are.

```python
X = np.array([1, 2])
Y = np.array([3, 2])
```

```python
# Calculate the dot product
result = np.dot(X, Y) # matrix multiplication
```

```python
#Elements of X
print(X[0])
print(X[1])
```

```python
#Elements of Y
print(Y[0])
print(Y[1])
```

`reshaped_arr = arr.reshape(2, 3)` --> Reshaping
- Changing the shape of an array.

Element-Wise Functions
result = np.sqrt(arr) --> Applying functions to each element.

Transposition
transposed_arr = arr.T --> Transposing a multi-dimensional array.
<h5><span style="color: #3588E9">Adding Constant to a Numpy Array</span></h5>

```python
# Create a constant to numpy array
u = np.array([1, 2, 3, -1]) 
```

```python
# Add the constant to array
u + 1
```

The process is like this: `1+1,  2+1, 3+1, -1+1`

<h5><span style="color: #3588E9">Mathematical Functions</span></h5>
NumPy can be used to create functions that map numpy arrays to new numpy arrays.

To access the value of `pi`:

```python
# The value of pi
np.pi
```

Create the following numpy array in Radians:

```python
# Create the numpy array in radians
x = np.array([0, np.pi/2 , np.pi])
```

To apply the function `sin` to the array `x` and assign the values to the array `y`; this applies the sine function to each element in the array:

```python
# Calculate the sin of each elements
y = np.sin(x) #  map the array x to a new array y
```

<h5><span style="color: #3588E9">Linspace</span></h5>

`linspace()` --> useful function for plotting mathematical functions. It returns evenly spaced numbers over a specified interval.

`np.linspace(start, stop, num = int value)` --> syntax
- start : start of interval range
- stop : end of interval range
* num : Number of samples to generate.

```python
# Makeup a numpy array within [-2, 2] and 5 elements
np.linspace(-2, 2, num=5)
```

```python
# Make a numpy array within [-2, 2] and 9 elements
np.linspace(-2, 2, num=9)
```

The `lincspace` function, can be used to generate 100 evenly spaced samples from the interval zero to two pie

```python
# Make a numpy array within [0, 2π] and 100 elements 
x = np.linspace(0, 2*np.pi, num=100)
```

The sine function can be applied to each element in the array `x` and assign it to the array `y`:

```python
# Calculate the sine of x list
y = np.sin(x)
```

```python
# Plot the result
plt.plot(x, y)
```

<h5><span style="color: #3588E9">Operations</span></h5>
Context of Euclidean vectors:

- `u = [1 0], v = [0 1], z = u + v = [(1+0) (0+1)] = [1 1]`

Use the tip to tail method when adding vectors:

```python
u = [1, 0]
v = [0, 1]
z = []

for n, m in zip(u,v):
  z.append(n+m)
  
# one line of NumPy code
u = np.array([1,0])
v = np.array([0,1])
z = u + v
z:array([1,1]) # numpy code will run much faster. important if you have lots of data
```

<strong style="color: #3588E9">Vector multiplication with a scalar</strong>

Multiplying a numpy array by a scalar is identical to multiplying a matrix by a scalar.

- `y = [1 2]`
- `z = 2y = [2(1) 2(2)] = [2 4]`

```python
y = np.array([1.2])
z = 2 * y
z:array([2,4])
```

<strong style="color: #3588E9">Product of two numpy arrays</strong>

* `u = [1 2] v = [3 2]`
* `z = u * v = [1 * 3   2 * 2] = [3 4]`

```python
u = np.array([1,2])
v = np.array([1,2])
z = u * v
```

```python
u = [1,2]
v = [3,2]
z = []

for n, m in zip(u,v):
	z.append(n * m)
```

<span style="color:#d65d0e">broadcasting</span> --> add a scalar value to the array, numpy will add that value to each element.

<h5><span style="color: #3588E9">Universal Functions</span></h5>
A <span style="color:#d65d0e">universal function</span> is a function that operates on ND arrays. We can apply a universal function to a numpy array

```python
 a = np.array([1, -1, 1, -1])
 mean_a = a.mean() # corresponds to the average of all the elements
```

`max()` --> find the maximum value

```python
b = np.array([1,-2,3,4,5])
max_b = b.max()
max_b
```

<h5><span style="color: #3588E9">Numpy Array Operations</span></h5>
If we iterate on a 1-D array it will go through each element one by one.

```python
arr1 = np.array([1, 2, 3])
print(arr1)
```

To get the result in the form of the list:

```python
for x in arr1:
  print(x)
```
