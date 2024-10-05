### <span style="color:#c6554f">Exception Handling</span>

An exception is an error that occurs during the execution of code. This error causes the code to raise an exception and if not prepared to handle it will halt the execution of the code.

<strong style="color: white">Examples:</strong>

```python
1/0
```

`ZeroDivisionError` occurs when you try to divide by zero.


```python
y = a + 5
```

`NameError` -- in this case, it means that you tried to use the variable a when it was not defined.


```python
a = [1, 2, 3]
a[10]
```

`IndexError` -- in this case, it occurred because you tried to access data from a list using an index that does not exist for this list.
##### <span style="color: #3588e9">Exception Handling</span>

<strong style="color: white">Syntax</strong>

```python
# potential code before try catch

try:
    # code to try to execute
except ZeroDivisionError:
    # code to execute if there is a ZeroDivisionError
except NameError:
    # code to execute if there is a NameError
except:
    # code to execute if ther is any exception
else:
    # code to execute if there is no exception
finally:
    # code to execute at the end of the try except no matter what
    
# code that will execute if there is no exception or a one that we are handling
```

<strong style="color: white">Example</strong>

```python
while True:
    try:
        age = int(input("what is your age?"))
        print(age)
    # execute the exception
	except ValueError: # error type
        print("Please enter a number!!") # show the error message
        continue
    except ZeroDivisionError:
        print('Please, enter an age higher then 0!')
        break
    else: # will execute if there's no error
        print("Thank you")
        break
    finally: # runs regardless the end result
        print("Ok, I am finally done!")
   	print() # só é executado se o break não estiver no bloco else 
```

<strong style="color: white">Example 2</strong>

```python
a = 1

try:
    b = int(input("Please enter a number to divide a"))
    a = a/b
except ZeroDivisionError:
    print("The number you provided cant divide 1 because it is 0")
except ValueError:
    print("You did not provide a number")
except:
    print("Something went wrong")
else:
    print("success a=",a)
finally:
    print("Processing Complete")
```

The `finally` block is very useful when we to log the activity of a user.

The `raise ValueError()` or `raise Exception()` line allow to throw custom errors. Useful if a library or a tool is being created and to let the user know that an error happened.

```python
try:
    age = int(input("what is your age?"))
    10/age
	raise Exception('hey, cut it out')
```

<strong style="color:#689d6a">Exception in a function</strong>

```python
# Error Handling
def sum (num1, num2):
    try:
        return num1 + num2
    except TypeError as err:
        print('please enter number {err}') # err returns a descriptive error
```

<strong style="color:#689d6a">Wrapping erros</strong>

```python
# Error Handling
def sum (num1, num2):
    try:
        return num1/num2
    		# combine different errors
    except (TypeError, ZeroDivisionError) as err:
        print(err) 
        
print(sum(1, '2'))
```

<strong style="color:#689d6a">Exception with files</strong>

```python
try:
    getfile = open("myfile", "r")
    getfile.write("My file for exception handling.")
except IOError: # erro type
    print("Unable to open or read the data in the file.")
else:
    print("The file was sritten successfully")
finally: # execute no matter the end result
    getfile.close() # close the file 
    print("File is now closed")
```