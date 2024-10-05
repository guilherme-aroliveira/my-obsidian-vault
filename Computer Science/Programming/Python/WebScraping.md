### <span style="color:#c6554f">Web Scraping</span>

Web scraping involves extracting information from web pages using Python. It can save time and automate data collection.

It requires Python code and two essential modules: Requests and Beautiful Soup.

<h5><strong style="color: #3588e9">Fetching and parsing HTML</strong></h5>
To start web scraping, you need to fetch the HTML content of a web page and parse it using Beautiful Soup. Here's a step-by-step example:

```python
import requests
from bs4 import BeautifulSoup

# Specify the URL of the webpage you want to scrape
url = 'https://en.wikipedia.org/wiki/IBM'

# Send an HTTP GET request to the webpage
response = requests.get(url)

# Store the HTML content in a variable
html_content = response.text

# Create a BeautifulSoup object to parse the HTML
soup = BeautifulSoup(html_content, 'html.parser')

# Display a snippet of the HTML content
print(html_content[:500])
```

BeautifulSoup represents HTML content as a tree-like structure, allowing for easy navigation. You can use methods like find_all to filter and extract specific HTML elements. For example, to find all anchor tags () and print their text:

```python
# Find all <a> tags (anchor tags) in the HTML
links = soup.find_all('a')

# Iterate through the list of links and print their text
for the link in links:
    print(link.text)
```

<h5><strong style="color: #3588e9">Beautiful Soup Object</strong></h5>

```python
from bs4 import BeautifulSoup

# Store the HTML content as a string in a variable:
html ="<!DOCTYPE html><html><head><title>Page Title</title></head><body><h3> \
<b id='boldest'>Lebron James</b></h3><p> Salary: $ 92,000,000 </p> \
<h3>Stephen Curry</h3><p> Salary: $85,000,000</p> \
<h3>Kevin Durant</h3><p> Salary: $73,200,000</p></body></html>"

# Parse the document into the constructor
soup = BeautifulSoup(html, 'html5lib')
```

The BeautifulSoup object represents the document as a nested data structure:

The document is converted to Unicode (similar to ASCII) and HTML entities are converted to Unicode characters. Beautiful Soup transforms a complex HTML document into a complex tree of Python objects. The `BeautifulSoup` object can create other types of objects

The method `prettify()` can be used to display the HTML in the nested structure:

```python
print(soup.prettify())
```

<strong>Tags</strong>

BeautifulSoup represents HTML as a set of Tree like objects with methods used to parse the HTML.

```python
# The tag object corresponds to an HTML tag in the original document
tag_pobject=soup.title
print("tag object:", tag_object)
print("tag object type:", type(tag_object))

tag_object = soup.h3
tag_object
```

<strong>Children, Parents and Siblings</strong>

```python
# HTML tree - child object
tag_child=tag_object.b

# Parent attribute
parent_tag=tag_child.parent
tag_object.parent # paragraph element

# Next-sibling attribute
siblint_1=tag_object.next_sibling
sibling_2 = sibling_1.next_sibling # header element
```

<strong>HTML Attributes</strong>

```python
# access a tag's attributes by treating the tag like a dictionary
tag_child['id']

# access the value and name as a key value pair in a dictionary
tag_child.attrs

# obtain the content of the attribute of the `tag`
tag_child.get('id')
```

<strong>Navigable String</strong>

Beautiful Soup uses the `NavigableString` class to contain this text

```python
# extract the string of the Tag object 
tag_string = tag_child.string # to access the content
tag_string

# verify the type
type(tag_string)

# convert NavigableString to string object in Python
unicode_string = str(tag_string)
unicode_string
```

<h5><strong style="color: #3588e9">Filter</strong></h5>
Filters allow you to find complex patterns, the simplest filter is a string.

Store an HTML as a string in the variable `table`:

```python
table = "<table><tr><td id='flight'>Flight No</td><td>Launch site</td> \
<td>Payload mass</td></tr><tr> <td>1</td> \
<td><a href='https://en.wikipedia.org/wiki/Florida'>Florida<a></td> \
<td>300 kg</td></tr><tr><td>2</td> \
<td><a href='https://en.wikipedia.org/wiki/Texas'>Texas</a></td> \
<td>94 kg</td></tr><tr><td>3</td> \
<td><a href='https://en.wikipedia.org/wiki/Florida'>Florida<a> </td> \
<td>80 kg</td></tr></table>"

table_bs = BeautifulSoup(table, 'html5lib')
```

The method `find_all()` is a filter, that can use filters to filter based on a tag’s name, it’s attributes, the text of a string, or on some combination of these.

It looks through a tag’s descendants and retrieves all descendants that match the filters.

The Method signature for `find_all(name, attrs, recursive, string, limit, **kwargs)`

<strong>Name</strong>

```python
# extract all the tags with that name and its children
table_rows = table_bs.find_all('tr')
table_rows

# Result - Python iterable
first_row = table_rows[0]
first_row

print(type(first_row))

first_row.td # obtain the child

# iterate through the list - each element corresponds to a row in the table
for i, row in enumerate(table_rows):
    print("row", i)
    # row is cell object
    cells = row.find_all('td')
    # extract table cells
    for j, cell in enumerate(cells):
        print('colunm', j, "cell", cell)

# use a list to match against any item in that list.
list_input = table_bs.find_all(name=["tr", "td"])
list_input
```

<strong>Attributes</strong>

If the argument is not recognized it will be turned into a filter on the tag's attributes.

```python
# filter based on the id value.
table_bs.find_all(id="flight")

# find all the elements that have links to the Florida Wikipedia page:
list_input=table_bs.find_all(href="https://en.wikipedia.org/wiki/Florida")
list_input

# finds all anchor tags with `href` value:
table_bs.find_all('a', href=True)
```

<strong>String</strong>

With string you can search for strings instead of tags, where we find all the elements with Florida:

```python
table_bs.find_all(string="Florida")
```

<strong>Find</strong>

The `find_all()` method scans the entire document looking for results. It’s useful if you are looking for one element, as you can use the `find()` method to find the first element in the document.

Consider the following two tables:

```python
from bs4 import BeautifulSoup

two_tables="<h3>Rocket Launch </h3> \
<p><table class='rocket'> \
<tr><td>Flight No</td><td>Launch site</td><td>Payload mass</td></tr> \
<tr><td>1</td><td>Florida</td><td>300 kg</td></tr> \
<tr><td>2</td><td>Texas</td><td>94 kg</td></tr> \
<tr><td>3</td><td>Florida </td><td>80 kg</td></tr></table></p>\
<p><h3>Pizza Party</h3> \
<table class='pizza'> \
<tr><td>Pizza Place</td><td>Orders</td><td>Slices </td></tr> \
<tr><td>Domino's Pizza</td><td>10</td><td>100</td></tr> \
<tr><td>Little Caesars</td><td>12</td><td >144 </td></tr> \
<tr><td>Papa John's</td><td>15 </td><td>165</td></tr>"

# create a `BeautifulSoup` object `two_tables_bs`
two_tables_bs = BeautifulSoup(two_tables, 'html.parser')

# find the first table using the tag name table
two_tables_bs.find("table")

# filter on the class attribute to find the second table
two_tables_bs.find("table", class_='pizza') # add an underscore to differentiate them
```

<h5><strong style="color: #3588e9">Downloading And Scraping The Contents Of A Web Page</strong></h5>

```python
# Download the web page - use GET
url = "http://www.ibm.com"

# Download the contents of the webpage in text format
data = requests.get(url).text

soup = BeautifulSoup(data, "html5lib")  # create a soup object using the variable 'data'

# Scrape all links
for link in soup.find_all('a', href=True):  # in html anchor/link is represented by the tag <a>
    print(link.get('href'))

# Scrape all image Tags
for link in soup.find_all('img'):  # in html image is represented by the tag <img>
    print(link)
    print(link.get('src'))
```

<strong>Scrape data from HTML Tables</strong>

```python
# The below url contains an html table with data about colors and color codes.
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DA0321EN-SkillsNetwork/labs/datasets/HTMLColorCodes.html"
```

Before proceeding to scrape a web site, it's important to examine the contents and the way data is organized on the website.

```python
# get the contents of the webpage in text format and store in a variable called data
data = requests.get(url).text

soup = BeautifulSoup(data, "html5lib")

# find a html table in the web page
table = soup.find('table')  # in html table is represented by the tag <table>

# Get all rows from the table
for row in table.find_all('tr'):  # in html table row represented by tag <tr>
    # Get all columns in each row.
    cols = row.find_all('td')  # in html a column is represented by tag <td>
    color_name = cols[2].string  # store the value in column 3 as color_name
    color_code = cols[3].text  # store the value in column 4 as color_code
    print("{}--->{}".format(color_name, color_code))
```

Apply BeautifulSoup to a web page --> to scrape a web page the `request` library it's needed.

```python
import request
from bs4 import BeautifulSoup

# Download the web page - use GET
## the .text attribute is used to ge the text
page = request.get("http://EnterWebSiteURL...").text

# Create a BeautifulSoup object
soup = BeautifulSoup(page, "html.parser")

# Pulls all instance of <a> tag
artist = souo,find_all('a')

# Clears data of all tags
for artist in artists:
	name= artist.contents[0]
	fullLink = artist.get('href')
	print(names)
	print(fullLink)
```

<h5><strong style="color: #3588e9">Scraping Tables from a Web Page using Pandas</strong></h5>

Particularly for extracting tabular data from a web page, you may also use the `read_html()` method of the Pandas library.

```python
# The below url contains an html table with data about colors and color codes.
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DA0321EN-SkillsNetwork/labs/datasets/HTMLColorCodes.html"

# extract all the tables from the given webpage
import pandas as pd

tables = pd.read_html(url)
tables

# list of dataframes representing the tables from the web page
tables[0]
```
