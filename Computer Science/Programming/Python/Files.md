### <span style="color: #c6554f">Reading and Writing Files</span>

<strong style="color:#3588e9">Reading files</strong>

```python
File1 = open("/resources/data/Examples2.txt", "r") # r is the Mode
#  Common values used include 'r' for reading, 
# 'w' for writing, and 'a' for appending.
print(File1.readline())
File1.close() # always close the file object
```

```python
exmp2 = 'file.txt'
with open(exmp2, 'r') as file:
	print(file.read())
```

>[!note]
>The `with()` statement to open a file is better practice because it automatically closes the file. The code will run everything in the indent block, then closes the file.

```python
with open("Example1.txt") as File1: 
	file_stuff=File.read()
    print(file_stuff)
    
print(File1.closed)
print(file_stuff)
```

<strong style="color:#3588e9">Writing to a file</strong>

```python
# Create a new file Example1.txt for writing
with open("Example1.txt", 'w') as file1: 
	file1.write("This is line A\n")
	file1.write("This is line B\n")
	# file1 is automatically closed when the 'with' block exits
```

```python
# Write lines to file
with open(exmp2, 'w') as writefile:
	writefile.write("This is line A\n")
	writefile.write("This is line B\n")
```

The method `.write()` works similarly to the method `.readline()`, except instead of reading a new line it writes a new line.

The proper way to read files is using `r+` mode.
- Ex: `with open('test.txt', mode='r+') as myfile: `

When something is written to a file, the cursor resets. When a file is opened, the cursor goes to zero.

<strong style="color:#3588e9">Writing multiple lines to a file using a list and loop</strong>

```python
# List of lines to write to the file
Lines = ["This is line 1", "This is line 2", "This is line 3"]

# Create a new file Example3.txt for writing
with open('Example3.txt', 'w') as file2:
    for line in Lines:
        file2.write(line + "\n")
    # file2 is automatically closed when the 'with' block exits
```

<strong style="color:#3588e9">Appending data to an existing file</strong>

In Python, you can use the `'a'` mode when opening a file to append new data to an existing file without overwriting its contents. Here's an example code snippet that demonstrates this:

```python
# Data to append to the existing file
new_data = "This is line C"

# Open an existing file Example2.txt for appending
with open('Example2.txt', 'a') as file1:
    file1.write(new_data + "\n")
    # file1 is automatically closed when the 'with' block exits
```

<strong style="color:#3588e9">Appending data to an existing file</strong>

In Python, you can copy the contents of one file to another by reading from the source file and writing to the destination file. Here's an example code snippet that demonstrates this:

```python
# Open the source file for reading
with open('source.txt', 'r') as source_file:
    # Open the destination file for writing
    with open('destination.txt', 'w') as destination_file:
        # Read lines from the source file and copy them to the destination file
        for line in source_file:
            destination_file.write(line)
    # Destination file is automatically closed when the 'with' block exits
# Source file is automatically closed when the 'with' block exits
```

<strong strong style="color:#3588e9">Additional modes</strong>

It's fairly inefficient to open the file in **a** or **w** and then reopen it in **r** to read any lines. Luckily we can access the file in the following modes:

- **r+** : Reading and writing. Cannot truncate the file.
- **w+** : Writing and reading. Truncates the file.
- **a+** : Appending and Reading. Creates a new file, if none exists.

```python
with open('Example2.txt', 'a+') as testwritefile:
	testwritefile.write("This is line E\n")
	print(testwritefile.read())
```

It is often very useful to know where the 'cursor' is in a file and be able to control it. The following methods allow to do precisely this:
- `tell()` --> returns the current position in bytes
- `seek(offset,from)` --> changes the position by 'offset' bytes with respect to 'from'. From can take the value of 0,1,2 corresponding to the beginning, relative to current position and end

```python
with open('Example2.txt', 'a+') as testwritefile:
	print("Initial Location: {}".format(testwritefile.tell()))

	data = testwritefile.read()

	if (not data): #empty strings return false in python
		print('Read nothing')
	else:
		print(testwritefile.read())

	testwritefile.seek(0,0) # move 0 bytes from beginning.
	
	print("\nNew Location : {}".format(testwritefile.tell()))
	data = testwritefile.read()
	if (not data):
		print('Read nothing')
	else:
		print(data)
		
	print("Location after read: {}".format(testwritefile.tell()) )
```

<strong strong style="color:#3588e9">Copy a file</strong>

```python
# Copy file to another
with open('Example2.txt','r') as readfile:
	with open('Example3.txt','w') as writefile:
		for line in readfile:
			writefile.write(line)
```

After reading files, we can also write data into files and save them in different file formats like **.txt, .csv, .xls (for excel files) etc**

One of the common patterns when working with files it to put them in a <strong style="color:#b16286">try-except</strong> block.

Writing JSON to a file

This is usually called **serialization**. It is the process of converting an object into a special format which is suitable for transmitting over the network or storing in file or database.

To handle the data flow in a file, the JSON library in Python uses the **dump()** or **dumps()** function to convert the Python objects into their respective JSON object. This makes it easy to write data to files.

```python
import json
person = {
    'first_name' : 'Mark',
    'last_name' : 'abc',
    'age' : 27,
    'address': {
        "streetAddress": "21 2nd Street",
        "city": "New York",
        "state": "NY",
        "postalCode": "10021-3100"
    }
}
```

serialization using dump() function[](https://cf-courses-data.static.labs.skills.network/jupyterlite/2.5.5/lab/index.html?mode=learn&env_type=jupyterlite&notebook_url=https%3A%2F%2Fcf-courses-data.static.labs.skills.network%2FIBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork%2Flabs%2Fjupyterlite%2Ffiles%2FModule_5%2FPY0101EN-5.4_WorkingWithDifferentFileTypes-20230719-1689724800.jupyterlite.ipynb&file_path=PY0101EN%2Fjupyterlite%2Ffiles%2FModule+5%2FPY0101EN-5+4_WorkingWithDifferent.ipynb#serialization-using-dump()-function)

**json.dump()** method can be used for writing to JSON file.

Syntax: json.dump(dict, file_pointer)

Parameters:

1. **dictionary** – name of the dictionary which should be converted to JSON object.
2. **file pointer** – pointer of the file opened in write or append mode.

```python
with open('person.json', 'w') as f:  # writing JSON object
    json.dump(person, f)
```

serialization using dumps() function[](https://cf-courses-data.static.labs.skills.network/jupyterlite/2.5.5/lab/index.html?mode=learn&env_type=jupyterlite&notebook_url=https%3A%2F%2Fcf-courses-data.static.labs.skills.network%2FIBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork%2Flabs%2Fjupyterlite%2Ffiles%2FModule_5%2FPY0101EN-5.4_WorkingWithDifferentFileTypes-20230719-1689724800.jupyterlite.ipynb&file_path=PY0101EN%2Fjupyterlite%2Ffiles%2FModule+5%2FPY0101EN-5+4_WorkingWithDifferent.ipynb#serialization-using-dumps()-function)

**json.dumps()** that helps in converting a dictionary to a JSON object.

It takes two parameters:

1. **dictionary** – name of the dictionary which should be converted to JSON object.
2. **indent** – defines the number of units for indentation

```python
# Serializing json  
json_object = json.dumps(person, indent = 4) 
  
# Writing to sample.json 
with open("sample.json", "w") as outfile: 
    outfile.write(json_object) 

print(json_object)
```

For deserialize it back to the Python object, we use the load() function

<strong strong style="color:#3588e9">Reading JSON files</strong>

The JSON package has json.load() function that loads the json content from a json file into a dictionary.

It takes one parameter:

**File pointer** : A file pointer that points to a JSON file.

```python
import json

# Opening JSON file 
with open('sample.json', 'r') as openfile:

	# Reading from json file 
    json_object = json.load(openfile) 

print(json_object)
print(type(json_object)) 
```

Reading data from CSV files

Each line in CSV file represents an observation, or commonly called a record. Each record may contain one or more fields which are separated by a comma.

```python
import piplite
await piplite.install(['seaborn', 'lxml', 'openpyxl'])
import pandas as pd
```

```python
from pyodide.http import pyfetch

filename = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/labs/Module%205/data/addresses.csv"

async def download(url, filename):
    response = await pyfetch(url)
    if response.status == 200:
        with open(filename, "wb") as f:
            f.write(await response.bytes())

await download(filename, "addresses.csv")

# call read_csv function output the data to the screen.
df = pd.read_csv("addresses.csv", header=None)
df
```

Adding column name (header) to the DataFrame

```python
df.columns =['First Name', 'Last Name', 'Location ', 'City','State','Area Code']
df
```

Selecting a single column

```python
df["First Name"]
```

Selecting multiple columns

```python
df = df[['First Name', 'Last Name', 'Location ', 'City','State','Area Code']]
df
```

Selecting rows using `.iloc` and `.loc` 

```python
# To select the first row
df.loc[0]

# To select the 0th,1st and 2nd row of "First Name" column only
df.loc[[0,1,2], "First Name" ]

# To select the 0th,1st and 2nd row of "First Name" column only
df.iloc[[0,1,2], 0]
```

Tranform Functions in Pandas

Python's Transform function returns a self-produced dataframe with transformed values after applying the function specified in its parameter.

```python
#import library
import pandas as pd
import numpy as np
```

```python
#creating a dataframe
df=pd.DataFrame(np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), columns=['a', 'b', 'c'])
df

#applying the transform function
df = df.transform(func = lambda x : x + 10)
df
```

use DataFrame.transform() function to find the square root to each element of the dataframe.

```python
result = df.transform(func = ['sqrt'])
result
```

Reading the data from XML file

```python
import pandas as pd
import xml.etree.ElementTree as etree
tree = etree.parse("fileExample.xml") 
root = tree.getroot()

columns = ["Name", "Phone Number", "Birthday"]
df = pd.DataFrame(columns = columns)

# loop to go through the document to collect the necessary data
for node in root:
	name = node.find("name").text
	phonenumber = node.find("phonenumber").text
	birthday = node.find("birthday".text)

# append the data to a dataframe.
df = df.append(pd.Series([name, phonenumber, birthdat], index = columns))..., ignore_index = True
```

Reading the data from XLSX file

```python
import pandas as pd

# Not needed unless you're running locally
# import urllib.request
# urllib.request.urlretrieve("https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/labs/Module%205/data/file_example_XLSX_10.xlsx", "sample.xlsx")

filename = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/labs/Module%205/data/file_example_XLSX_10.xlsx"

async def download(url, filename):
    response = await pyfetch(url)
    if response.status == 200:
        with open(filename, "wb") as f:
            f.write(await response.bytes())

await download(filename, "file_example_XLSX_10.xlsx")

df = pd.read_excel("file_example_XLSX_10.xlsx")
df
```

Pandas does not include any methods to read and write XML files.

Writing with xml.etree.ElementTree

The **xml.etree.ElementTree** module comes built-in with Python. It provides functionality for parsing and creating XML documents. **ElementTree** represents the XML document as a tree. We can move across the document using nodes which are elements and sub-elements of the XML file.

```python
import xml.etree.ElementTree as ET

# create the file structure
employee = ET.Element('employee')
details = ET.SubElement(employee, 'details')
first = ET.SubElement(details, 'firstname')
second = ET.SubElement(details, 'lastname')
third = ET.SubElement(details, 'age')
first.text = 'Shiv'
second.text = 'Mishra'
third.text = '23'

# create a new XML file with the results
mydata1 = ET.ElementTree(employee)
# myfile = open("items2.xml", "wb")
# myfile.write(mydata)
with open("new_sample.xml", "wb") as files:
    mydata1.write(files)
```

Reading with xml.etree.ElementTree

```python
# Not needed unless running locally
# !wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/labs/Module%205/data/Sample-employee-XML-file.xml

import xml.etree.ElementTree as etree

filename = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/labs/Module%205/data/Sample-employee-XML-file.xml"

async def download(url, filename):
    response = await pyfetch(url)
    if response.status == 200:
        with open(filename, "wb") as f:
            f.write(await response.bytes())

await download(filename, "Sample-employee-XML-file.xml")
```

You would need to firstly parse an XML file and create a list of columns for data frame, then extract useful information from the XML file and add to a pandas data frame.

Example:

```python
# Parse the XML file
tree = etree.parse("Sample-employee-XML-file.xml")

# Get the root of the XML tree
root = tree.getroot()

# Define the columns for the DataFrame
columns = ["firstname", "lastname", "title", "division", "building", "room"]

# Initialize an empty DataFrame
datatframe = pd.DataFrame(columns=columns)

# Iterate through each node in the XML root
for node in root:
    # Extract text from each element
    firstname = node.find("firstname").text
    lastname = node.find("lastname").text
    title = node.find("title").text
    division = node.find("division").text
    building = node.find("building").text
    room = node.find("room").text
    
    # Create a DataFrame for the current row
    row_df = pd.DataFrame([[firstname, lastname, title, division, building, room]], columns=columns)
    
    # Concatenate with the existing DataFrame
    datatframe = pd.concat([datatframe, row_df], ignore_index=True)
    datatframe
```

Reading xml file using pandas.read_xml function

We can also read the downloaded xml file using the read_xml function present in the pandas library which returns a Dataframe object.

```python
# Herein xpath we mention the set of xml nodes to be considered for migrating  to the dataframe which in this case is details node under employees.
df=pd.read_xml("Sample-employee-XML-file.xml", xpath="/employees/details") 
```

Save Data

Correspondingly, Pandas enables us to save the dataset to csv by using the **dataframe.to_csv()** method, you can add the file path and name along with quotation marks in the parentheses.

For example, if you would save the dataframe df as **employee.csv** to your local machine, you may use the syntax below:

```python
datatframe.to_csv("employee.csv", index=False)
```

We can also read and save other file formats, we can use similar functions to **`pd.read_csv()`** and **`df.to_csv()`** for other data formats. The functions are listed in the following table:

Read/Save Other Data Formats

csv --> pd.read_sv()          df.to_csv() --> to read
json --> pd.read_json()     df.to_json()
excel --> pd.read_excel()  df.to_excel()
hdf --> pd.read_hdf()        df.to_hdf()
sql --> pd.read_sql()         df.to_sql()

Reading the Image file

**PIL** is the Python Imaging Library which provides the python interpreter with image editing capabilities.

```python
# importing PIL 
from PIL import Image 

# Uncomment if running locally
# import urllib.request
# urllib.request.urlretrieve("https://hips.hearstapps.com/hmg-prod.s3.amazonaws.com/images/dog-puppy-on-garden-royalty-free-image-1586966191.jpg", "dog.jpg")

filename = "https://hips.hearstapps.com/hmg-prod.s3.amazonaws.com/images/dog-puppy-on-garden-royalty-free-image-1586966191.jpg"

async def download(url, filename):
    response = await pyfetch(url)
    if response.status == 200:
        with open(filename, "wb") as f:
            f.write(await response.bytes())

await download(filename, "./dog.jpg")

# Read image 
img = Image.open('./dog.jpg','r') 
  
# Output Images 
img.show()
```

Data Analysis

**Diabetes Dataset** is an online source and it is in CSV

**Context:** This dataset is originally from the **National Institute of Diabetes and Digestive and Kidney Diseases**. The objective of the dataset is to diagnostically predict whether or not a patient has diabetes, based on certain diagnostic measurements included in the dataset. Several constraints were placed on the selection of these instances from a larger database. In particular, all patients here are females at least 21 years of age of Pima Indian heritage.

**Content:** The datasets consists of several medical predictor variables and one target variable, Outcome. Predictor variables includes the number of pregnancies the patient has had, their BMI, insulin level, age, and so on.

```python
# Import pandas library
import pandas as pd
```

```python
filename = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/labs/Module%205/data/diabetes.csv"

async def download(url, filename):
    response = await pyfetch(url)
    if response.status == 200:
        with open(filename, "wb") as f:
            f.write(await response.bytes())

await download(filename, "diabetes.csv")
df = pd.read_csv("diabetes.csv")
```

use the **dataframe.head(n)** method to check the top n rows of the dataframe, where n is an integer. Contrary to **dataframe.head(n)**, **dataframe.tail(n)** will show you the bottom n rows of the dataframe.

```python
# show the first 5 rows using dataframe.head() method
print("The first 5 rows of the dataframe") 
df.head(5)
```

o view the dimensions of the dataframe, we use the **`.shape`** parameter.

```python
df.shape
```

Statistical Overview of dataset


```python
df.info() # prints information about a DataFrame including the index dtype and columns, non-null values and memory usage.
```

```python
df.describe() 
```

Pandas **describe()** is used to view some basic statistical details like percentile, mean, standard deviation, etc. of a data frame or a series of numeric values. When this method is applied to a series of strings, it returns a different output

Identify and handle missing values

We use Python's built-in functions to identify these missing values. There are two methods to detect missing data:

**isnull()**

**.notnull()**

The output is a boolean value indicating whether the value that is passed into the argument is in fact missing data.

```python
missing_data = df.isnull()
missing_data.head(5)
```

True" stands for missing value, while "False" stands for not missing value.

Count missing values in each column[](https://cf-courses-data.static.labs.skills.network/jupyterlite/2.5.5/lab/index.html?mode=learn&env_type=jupyterlite&notebook_url=https%3A%2F%2Fcf-courses-data.static.labs.skills.network%2FIBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork%2Flabs%2Fjupyterlite%2Ffiles%2FModule_5%2FPY0101EN-5.4_WorkingWithDifferentFileTypes-20230719-1689724800.jupyterlite.ipynb&file_path=PY0101EN%2Fjupyterlite%2Ffiles%2FModule+5%2FPY0101EN-5+4_WorkingWithDifferent.ipynb#Count-missing-values-in-each-column)

Using a for loop in Python, we can quickly figure out the number of missing values in each column. As mentioned above, "True" represents a missing value, "False" means the value is present in the dataset. In the body of the for loop the method ".value_counts()" counts the number of "True" values.

```python
for column in missing_data.columns.values.tolist():
    print(column)
    print (missing_data[column].value_counts())
    print("") 
```

Correct data format

Check all data is in the correct format (int, float, text or other).

In Pandas, we use

**.dtype()** to check the data type

**.astype()** to change the data type

Numerical variables should have type **'float'** or **'int'**.

```python
df.dtypes
```

Visualization

**Visualization** is one of the best way to get insights from the dataset. **Seaborn** and **Matplotlib** are two of Python's most powerful visualization libraries.


```python
# import libraries
import matplotlib.pyplot as plt
import seaborn as sns
```

```python
labels= 'Not Diabetic','Diabetic'
plt.pie(df['Outcome'].value_counts(),labels=labels,autopct='%0.02f%%')
plt.legend()
plt.show()
```

##### <strong style="color:#3588e9">File modes in Python</strong>

| Mode | Syntax | Description                                                                                                                  |
| ---- | ------ | ---------------------------------------------------------------------------------------------------------------------------- |
| 'r'  | `'r'`  | Read mode. Opens an existing file for reading. Raises an error if the file doesn't exist.                                    |
| 'w'  | `'w'`  | Write mode. Creates a new file for writing. Overwrites the file if it already exists                                         |
| 'a'  | `'a'`  | Append mode. Opens a file for appending data. Creates the file if it doesn't exist.                                          |
| 'x'  | `'x'`  | Exclusive creation mode. Creates a new file for writing but raises an error if the file already exists.                      |
| 'rb' | `'rb'` | Exclusive creation mode. Creates a new file for writing but raises an error if the file already exists.                      |
| 'wb' | `'wb'` | Write binary mode. Creates a new binary file for writing.                                                                    |
| 'ab' | `'ab'` | Append binary mode. Opens a binary file for appending data.                                                                  |
| 'xb' | `'xb'` | Exclusive binary creation mode. Creates a new binary file for writing but raises an error if it already exists.              |
| 'rt' | `'rt'` | Read text mode. Opens an existing text file for reading. (Default for text files)                                            |
| 'wt' | `'wt'` | Write text mode. Creates a new text file for writing. (Default for text files)                                               |
| 'wa' | `'wa'` | Append text mode. Opens a text file for appending data. (Default for text files)                                             |
| 'at' | `'at'` | Exclusive text creation mode. Creates a new text file for writing but raises an error if it already exists.                  |
| 'xt' | `'xt'` | Read and write mode. Opens an existing file for both reading and writing.                                                    |
| 'w+' | `'w+'` | Write and read mode. Creates a new file for reading and writing. Overwrites the file if it already exists.                   |
| 'a+' | `'a+'` | Append and read mode. Opens a file for both appending and reading. Creates the file if it doesn't exist.                     |
| 'x+' | `'x+'` | Exclusive creation and read/write mode. Creates a new file for reading and writing but raises an error if it already exists. |
