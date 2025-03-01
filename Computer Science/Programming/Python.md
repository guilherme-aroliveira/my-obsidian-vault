###### **Introduction**

A Python module is a `.py` file containing Python definitions, statements, functions, and classes. It can be imported to other scripts and notebooks.

```python
# module.py

def square(number):
  return number ** 2
  
def doubler(number):
  return number ** 2
```

```python
from module import square, doubler
print("4^2=", square(4))
print("4*2=", doubler(4))
```

A package is a collection of python modules into a directory with a `__init__.py` Example: `myproject/__init__.py,  myproject/module1.py`

<strong>To create a Python package</strong>

To make myproject folder into a package, it must have `__init__.py` as a file in the myproject folder.

`from . import module 1` --> The contents of the `__init__.py` file must be from dot import module one.

<strong style="color: white">Steps:</strong>
- create a folder with the package name.
- create an empty `__init__.py` file
- Create the required modules.
- Finally, in the `__init__.py` file, add code to reference the modules needed in the package

<strong>Vefiry the package</strong>

`import <projectName>`

<strong>The general structure for testing a package:</strong>

`{package_name}.{module_name}.{function_name}{parameters}`

<strong style="color: white">Example:</strong> `myprojetc.basic.square(2)`

<strong>Using the package</strong>

`from myproject.module import square, doubler` --> imports the functions in the package.

When a module or a packages is imported, the corresponding object created by Python is always of type module. 

>[!note ]
>The distinction between module and package is only at the file system level.

A library is a collection of packages or can be a single package. Examples: Numpy, pytorch, pandas. 

Terms package and library are often used interchangeably. Therefore, numpy, pytorch, and Pandas are also referred to as packages.
###### <strong style="color: red">Setup</strong> 
1. Install python on linux
	1. <code>sudo apt install python3</code>
	2. <code>python3 --version</code> or <code>python3 -V</code> --> check the python version
2. Install pip
	1. <code>sudo apt install python3-pip</code>
	2. <code>pip3 --version</code> --> check the pip version
3. Create a virtual environment
	1. `cd /path/to/project`
	2. `python3 -m venv .venv`
	3. `source .venv/bin/activate` --> ativar o ambiente virtual
	4. `pip install package_name` --> install a library in the virtual environment
	5. `deactivate` --> desativar um ambiente virtual
###### <strong style="color: red">Workflow</strong>
- Run the program
	- `python3 main.py`
###### <strong style="color: #d79921">Tools</strong>

- <span  style="color:#98971a">Pip</span> <span style="color: #3588E9">--></span> package manager for python
	- <code style="color: #689d6a">pip install [package]</code> <span style="color: #3588E9">--></span> install a python package
	- <code style="color: #689d6a">pip install [package] --upgrade</code> <span style="color: #3588E9">--></span> to upgrade a package
	- <code style="color: #689d6a">pip show [package]</code> <span style="color: #3588E9">--></span> shows where a package is installed
	- <code style="color: #689d6a">pip uninstall [package]</code> <span style="color: #3588E9">--></span> to remove a package
	- <code style="color: #689d6a">python3 -c "import sys; print(sys.path)"</code> <span style="color: #3588E9">--></span> list of paths for packages
	- packages can be passed to a file called `requirements.txt`
		- <code style="color: #689d6a">pip install -r requiements.txt</code> <span style="color: #3588E9">--></span> install all packages
		- A best practice is to specify the version of a package. Ex: `Flask==0.10.1`
		- Obs: If the version is not specified, Python will always install the latest stable version of a package


One of the most popular frameworks is PyLint. PyLint basically evaluates the code against compliance with the PEP8 coding style guide and generates comments wherever it finds an issue.
<span style="color:#98971a">PyLint</span> <span style="color: #3588E9">--></span> check (evaluates) Python code
- <code style="color: #689d6a">$ pylint sample.py</code>
###### <strong style="color: #d79921">Libraries</strong>

Python libraries are like toolkits. Each library has specific tools to simplify and expedite certain programming tasks.

A Python library is a set of packages that perform only specific functionality.

To import a library in Python: `import <library>`

<span style="color:#d65d0e">SciPy</span> <span style="color: #3588E9">--></span> library for mathematics, science, and engineering. scientific and numeric computing

<span style="color:#d65d0e">Pandas</span> <span style="color: #3588E9">--></span>  library for data analysis.
- The pandas API is used to process the data by communicating with the other Software Components
- offer data manipulation and analysis capabilities
- `import pandas` <span style="color: #3588E9">--></span> import pandas
- `import pandas as pd` <span style="color: #3588E9">--></span> use `as` statement to shorten the name of the library

<span style="color:#d65d0e">NumPy</span> <span style="color: #3588E9">--></span> library for numerical and scientific computing, which is also the basis for pandas. 
- It's used for working with arrays, linear algebra, fourier transform, and matrices. 
- It provides support for large, multi-dimensional arrays and matrices, along with a collection of high-level mathematical functions to operate on these arrays
- NumPy stands for <span style="color:#d65d0e">Numerical Python</span> and it is an open source project.
- `import numpy as np` <span style="color: #3588E9">--></span> usually imported under the `np` alias.
- To create an array:
	- Syntax --> `array_1d = np.array([list1 values])` 
	- Example: 
		- `array_1d = np.array([1, 2, 3])` --> 1 dimension Array
		- `array_2d = np.array([[1, 2], [3, 4]])` --> 2 dimension Array
- NumPy Array Attributes
	- `np.mean(array)` --> Calculates the mean of array elements
	- `np.sum(array)` --> Calculates the sum of array elements
	- `np.min(array)` --> Finds the minimum value in the array
	- `np.max(array)` --> Finds the maximum value in the array
	- `np.dot(array_1, array_2)` --> Computes dot product of two arrays

<span style="color:#d65d0e">Pyplot</span> <span style="color: #3588E9">--></span> library that allows to plots a graph
- `import the library pyplot as plt` 
- the first input corresponds to the values for the horizontal or x-axis. 
- the second input corresponds to the values for the vertical or y-axis

<span style="color:#d65d0e">Requests</span> <span style="color: #3588E9">--></span> python Library that allows to send HTTP/1.1 requests easily.
- it's a popular method for dealing with the HTTP protocol in Python
- `import requests`
###### <strong style="color: #d79921">Syntax</strong>

There can't be more than one instruction on a line in Python

`\` <span style="color: #3588E9">--></span> tells Python that the next character has a special meaning

`\n` <span style="color: #3588E9">--></span> new line character
- to print a long sentence separated with new lines

`end=""` <span style="color: #3588E9">--></span> keyword argument
- determines the characters that the print function sends to the output once it reaches the end of its positional arguments
- print("Hello!", end="") 
  print("Python is a great language") --> both lines are printed on the same line
- the end argument accepts any value to be passed

`sep=""` <span style="color: #3588E9">--></span> allows to control how Python separates the outputted argument
- the default value is just a space

`**` <span style="color: #3588E9">--></span> Exponential

`//` <span style="color: #3588E9">--></span> Floor Division for round values

`#` <span style="color: #3588E9">--></span> comment for single or multi-line

<span style="color:#d65d0e">If-Elif-Else</span> <span style="color: #3588E9">--></span> Executes the first code block if condition1 is `True`, otherwise checks condition2, and so on. If no condition is `True`, the else block is executed. All code must be indented

```python
if condition1:
	# Code if condition1 is True
elif condition2:
	# Code if condition2 is True
else:
	# Code if condition3 is True
```

<strong style="color: white">Example:</strong>
```python
score = 85  # Example score
if score >= 90:
    print("You got an A!")
elif score >= 80:
    print("You got a B.")
else:
    print("You need to work harder.")

# Output = You got a B.
```

<span style="color:#d65d0e">logical operators</span> <span style="color: #3588E9">--></span> `or`, `and`, `not`. 
- Ex: `if(not is_hungry):`

<span style="color:#d65d0e">For loops</span> <span style="color: #3588E9">--></span> repeatedly executes a block of code for a specified number of iterations or over a sequence of elements (list, range, string, etc.).
- syntax <span style="color: #3588E9">--></span> `for variable in sequence: # Code to repeat`

<strong style="color: white">Example 1:</strong>
```python
for num in range(1, 10): 
    print(num) 
```

<strong style="color: white">Example 2:</strong>
```python
fruits = ["apple", "banana", "orange", "grape", "kiwi"] 
for fruit in fruits:
    print(fruit)
```

<span style="color:#d65d0e">Loop Controls</span> <span style="color: #3588E9">--></span> `break` exits the loop prematurely, while `continue` skips the rest of the current iteration and moves to the next iteration.

<strong style="color: white">Syntax</strong>
```python
for: # Code to repeat 
    if # boolean statement
        break 

for: # Code to repeat  
    if # boolean statement
        continue
```

<strong style="color: white">Example 1:</strong>
```python
for num in range(1, 6):
    if num == 3:
        break
    print(num)
```

<strong style="color: white">Example 2:</strong>
```python
for num in range(1, 6):
    if num == 3:
        continue
    print(num)
```

<span style="color:#d65d0e">While Loop</span> <span style="color: #3588E9">--></span> A `while` loop repeatedly executes a block of code as long as a specified condition remains `True`.
- syntax <span style="color: #3588E9">--></span>  `while condition: # Code to repeat ` 

<strong style="color: white">Example:</strong>
```python
count = 0 while count < 5: 
    print(count) count += 1
```

<span style="color:#d65d0e">bitwise operators</span> <span style="color: #3588E9">--></span> manipulate single bits of data
- `&` <span style="color: #3588E9">--></span> conjunction. Only returns one if both bits are one. Ex: `15 & 22 = 6`
- `|` <span style="color: #3588E9">--></span> disjunction. Ex: `15 | 22 = 31` returns 1 if either both bits are one or if only one of the bits is one
- `~` <span style="color: #3588E9">--></span> negation. Ex: `~22 = -23` returns one for every zero and zero for every one
- `^` <span style="color: #3588E9">--></span> exclusive. Ex: `15 ^ 22 = 25` returns one if only one of the bits is one

<span style="color:#d65d0e">bit shifting</span> <span style="color: #3588E9">--></span> move bits a certain amount of places
- `>>` or `<<`

<span style="color:#d65d0e">Class definition</span> <span style="color: #3588E9">--></span> Defines a blueprint for creating objects and defining their attributes and behaviors.
- `class ClassName: # Class attributes and methods`
```python
class Person:
	def __init__(self, name, age):
	self.name = name
	self.age = age
```

<span style="color:#d65d0e">Function Call</span> <span style="color: #3588E9">--></span> the act of executing the code within the function using the provided arguments.
- syntax <span style="color: #3588E9">--></span> `function_name(arguments)`
- Example: `greet("Alice")`

<span style="color:#d65d0e">Try-Except-Else</span> <span style="color: #3588E9">--></span> blocks used to prevent a program from crashing due to exceptions.
- exceptions <span style="color: #3588E9">--></span> an error that occurs during the execution of code
- The except block defines how to handle the exception gracefully, like displaying an error message or taking alternative actions.
- After the except block, the program continues executing the remaining code

<strong style="color: white">Syntax:</strong>
```python
try: # Code that might raise an exception except 
ExceptionType: # Code to handle the exception 
else: # Code to execute if no exception occurs 
```

<strong style="color: white">Example:</strong>
```python
try: 
    num = int(input("Enter a number: ")) 
except ValueError: 
    print("Invalid input. Please enter a valid number") 
else: 
    print("You entered:", num)
```

<span style="color:#d65d0e">Try-Except with Finally Block</span> <span style="color: #3588E9">--></span> Code in the `finally` block always executes, regardless of whether an exception occurred.

<strong style="color: white">Syntax:</strong>
```python
try: # Code that might raise an exception except 
ExceptionType: # Code to handle the exception 
finally: # Code that always executes 
```

<strong style="color: white">Example:</strong>
```python
try: 
    file = open("data.txt", "r") 
    data = file.read() 
except FileNotFoundError: 
    print("File not found.") 
finally: 
    file.close()
```

List of exceptions that are built into Python --> https://docs.python.org/3/library/exceptions.html
###### <strong style="color: #d79921">Data Types & Structs</strong>

<span style="color:#d65d0e">Strings</span> <span style="color: #3588E9">--></span> represent text
- Python uses "double" or 'single' quotes in strings
- `"Hello! 'Python' is cool"` <span style="color: #3588E9">--></span> quotes within strings
- `'Hi \'hi\''` <span style="color: #3588E9">--></span> escape quotes as special characters

Lists -->  container that allows you to store and access data. Each element is associated with an index
- to access an element of a list: `a[3]`

<span style="color:#d65d0e">Function</span> <span style="color: #3588E9">--></span> part of the code that's use to cause an effect or evaluate a value. Is a reusable block of code that performs a specific task or set of tasks when called
- `def` <span style="color: #3588E9">--></span> keyword to define a function 
- `def function_name(parameters):` <span style="color: #3588E9">--></span> syntax
- Example: `def greet(name): print("Hello,", name)`

Keyword arguments <span style="color: #3588E9">--></span> special arguments
###### <strong style="color: #d79921">Functions</strong>

<span style="color:#d65d0e">Built-in functions</span> <span style="color: #3588E9">--></span> can be used without importing it

- `print()` <span style="color: #3588E9">--></span> to print values to the console. 
	- Ex: `print(""Hello Python programmer!")`
- `input()` <span style="color: #3588E9">--></span> to input some data from the console
	- the value of an input function is always a string
	- Ex: `color = input("What is your favorite color?")`
- `str()` <span style="color: #3588E9">--></span> to type-cast a number into a string
- `len()` <span style="color: #3588E9">--></span> to get the length of a list.
	- Ex: `len(countries_list)`
- `range()` <span style="color: #3588E9">--></span> Generates a sequence of numbers within a specified range.
	- `range(start, stop, step)` --> syntax
	- Example: `range(1, 11, 2) #generates odd integers from 1 to 9`
- `open()` <span style="color: #3588E9">--></span> to create a file object
	- Ex: `open("/resouces/data/Example2.txt", r)`
		- takes two main arguments: the file path (including the file name) and the mode parameter
		- mode parameter <span style="color: #3588E9">--></span> specifies the operation to be performed on the file.
		- the second parameter `r` is the mode. Common values used include 'r' for reading, 'w' for writing, and 'a' for appending.
- `readline()` --> reads only one line.
- `write()` <span style="color: #3588E9">--></span> function that allows to write in a file
	- Ex: `File1.write("This is line 1")`
- `close()` <span style="color: #3588E9">--></span> to close the file object 
- `seek(` --> moves the cursor to the specified index.
	- Ex: `my_file.seek(0)`


Modules
###### <strong style="color: #d79921">HTTP Requests</strong>

<span style="color:#d65d0e">Request Module</span> <span style="color: #3588e9">--></span> one of several libraries including: httplib, urllib, that can work with the HTTP protocol.

```python
import request 
url='https://www.ibm.com/'

r = requests.get(url) # GET request
r.status_code:200
r.request.headers
r.resquest.body:None # to view the request body

# to view HTTP response header
header=r.headers 
print(r.headers)

# obtain the date the request
header['date']:'Thu, 19 Nov 2020 15:21:47 GMT'
header['Content-Type']:'text/html; charset=UTF-8'

# check the encoding
r.enconding:'UTF-8'

# attribute text to display the HTML in the body
r.text[0:100] 
```

<strong style="color: #3588e9">Requests</strong>

```python
import os 
from PIL import Image
from IPython.display import IFrame

## Load other types of data for non-text requests
# Use single quotation marks for defining string
url='https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/IDSNlogo.png'

r = requests.get(url)
print(r.headers)

# Save an image using a file object
path = os.path.join(os.getcwd(),'image.png')

# Access the body of the response
with open(path,'wb') as f:
    f.write(r.content)

# View the image
Image.open(path)
```

<strong style="color: #3588e9">Get Request with URL Parameters</strong>

```python
url_get='http://httpbin.org/get'

# use the dictionary payload to create a Query string
payload={"name":"Joseph";"ID":"123"}

# Requests
r.requests.get(url_get,params=payload)
r.url # print the URL

print("request body:", r.request.body)
print(r.status_code) # the status code
print(r.text) # to see the reponse as text

r.headers['Content-Type'] # To look the content type
r.json() # format the content type, returns a Python dict
r.json()['args'] # to show the names and values of a query string
```

<strong style="color: #3588e9">POST Requests</strong>

```python
url_post='http://httpbin.org/post'

# payload dict
payload={"name":"Joseph";"ID":"123"}

# make a POST request
r_post = request.post(url_post,data=payload)

# Comparing the URL
print("POST request URL: ", r_post.url)
print("GET request URL: ", r.url)

# Comparing the request body
print("POST request body: ", r_post.request.body)
print("GET request body: ", r.request.body)

r_post.json()['form'] # get the payload
```

<strong style="color: white">Retrieve data from the FishWatch API</strong>

```python
# Import the requests and json modules for making HTTP requests and handling JSON data, respectively.
import requests
import json

# Specify the URL of the API endpoint for retrieving information about fish species.
url = "https://www.fishwatch.gov/api/species"

# Make an HTTP GET request to the specified URL and store the response in the data variable.
data = requests.get(url)

# Parse the JSON data received from the API response using json.loads() and store it in the results variable.
results = json.loads(data.text)
```

<strong style="color: white">Example: Fruityvice API</strong>

```python
import requests
import json

data = requests.get("https://fruityvice.com/api/fruit/all")

results = json.loads(data.text)

pd.DataFrame(results)

df2 = pd.json_normalize(results)
df2

# Extract some information from the dataframe
cherry = df2.loc[df2["name"] == 'Cherry']
(cherry.iloc[0]['family']) , (cherry.iloc[0]['genus'])
```
###### <strong style="color: white">Conventions</strong>

Use spaces instead of tabs - <strong style="color: #689d6a">(4 spaces for indentation)</strong>

Use blank line to separate functions and classes
- helps to establish the begging and end of code parts

Use spaces around operators and after commas <strong style="color: #689d6a">(readability)</strong>
- make commands looks spacious and discrete

Create separate functions for functionalities <strong style="color: #689d6a">(blockes of codes)</strong>
- increases the execution speed of the code

Use lowercase with underscores for functions and files <strong style="color: #689d6a">(naming)</strong>
- Example: my_package or package

Naming classe using CamelCase
- condign convention well-accepted in the coding community
- Helps to distinguish between classes and functions
- Ex: `class LamSquirrelCage:` 
 
Naming constants
- capitalize all words and separate them with underscores
- separeate the wods with underscores
- Ex: `MAX_FILE_UPLOAD_SIZE`

Write self-documenting code instead of unnecessary comments

Static code analysis
- commonly used to manage compliance
- evaluates style compliance without executing the code
- use PyLint to check the Python code compliance with PEP8 guidelines
###### <strong style="color: white">Tips</strong>

I/O --> stands for input and ouput

variables in Python can be re-declared (dynamically typed)

<span style="color:#d65d0e">deaf program</span> <span style="color: #3588E9">--></span> program that doesn't use any input function

The <strong style="color:#b16286">IOError</strong> usually happens when the computer or machine has some issues reading or writing any sort of I-O operation.