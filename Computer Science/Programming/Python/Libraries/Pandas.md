### <span style="color:#c6554f">Pandas</span>
<h5><strong style="color: #3588e9">Data Loading:</strong></h5>

```python
import pandas as pad

# Read data from CSV file
df = pd.read_csv('my_file.csv') # df is short for dataframe
```

A `csv` is a typical file type used to store data.

<strong style="color: #3588e9">Download a csv file</strong>

```python
from pyodide.http import pyfetch
import pandas as pd

filename = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/labs/Module%204/data/TopSellingAlbums.csv"

async def download(url, filename):
    response = await pyfetch(url)
    if response.status == 200:
        with open(filename, "wb") as f:
            f.write(await response.bytes())

await download(filename, "TopSellingAlbums.csv")
df = pd.read_csv("TopSellingAlbums.csv")
```

<h5><span style="color: #3588e9">What is a DataFrame?</span></h5>
A <span>DataFrame</span> is a two-dimensional labeled data structure with rows and columns of potentially different data types. Data Frames are suitable for a wide range of data, including structured data from CSV files, Excel spreadsheets, SQL databases, and more.

```python
#dataframe
csv_path = 'TopSellingAlbums.csv'
df = pd.read_csv(csv_path) 
```

- `head()` --> method to examine the first five rows of a data frame

```python
# Print first five rows of the dataframe
df.head()
```

To read an excel file: 

```python
xlsx_path = 'file1.xlsx'
df = pd.read_excel(xlsx_path)
```

Is possible to access the a certain column and assign it a new dataframe x:

```python
# Access to the column Length

x = df[['Length']]
x
```

<h5><strong style="color: #3588e9">Series</strong></h5>
A <span style="color:#d65d0e">Series</span> is a one-dimensional labeled array in Pandas. It can be thought of as a single column of data with labels or indices for each element. It can be created from various data sources, such as lists, NumPy arrays, or dictionaries.

```python
import pandas as pd

# Create a Series from a list
data = [10, 20, 30, 40, 50]
s = pd.Series(data)

print(s)
```

```python
# Get the column as a series

x = df['Length']
x
```

```python
# Get the column as a dataframe

x = df[['Artist']] 
type(x)
```

```python
# Access to multiple columns

y = df[['Artist','Length','Genre']]
y
```
<h5><span style="color: #3588e9">Accessing Elements in a Series</span></h5>
<strong style="color: #3588e9">Accessing by label</strong>

```python
print(s[2])     # Access the element with label 2 (value 30)
```

<strong style="color: #3588e9">Accessing by position</strong>

```python
print(s.iloc[3]) # Access the element at position 3 (value 40)
```

<strong style="color: #3588e9">Accessing multiple elements</strong>

```python
print(s[1:4])   # Access a range of elements by label
```

- `iloc` --> method that allows to o access unique elements

```python
# Access the value on the second row and the third column
df.iloc[1,2]
```

The column can be accessed using the name as well:

```python
# Access the column using the name
df.loc[1, 'Artist']
```

<h5><span style="color: #3588e9">Series Attributes and Methods</span></h5>
Pandas Series come with various attributes and methods that helps to manipulate  and analyze data effectively.

- **values**: Returns the Series data as a NumPy array.
- **index**: Returns the index (labels) of the Series.
- **shape**: Returns a tuple representing the dimensions of the Series.
- **size**: Returns the number of elements in the Series.
- **mean(), sum(), min(), max()**: Calculate summary statistics of the data.
- **unique(), nunique()**: Get unique values or the number of unique values.
- **sort_values(), sort_index()**: Sort the Series by values or index labels.
- **isnull(), notnull()**: Check for missing (NaN) or non-missing values.
- **apply()**: Apply a custom function to each element of the Series.


>[!note]
>Data Frame can be created out of a dictionary. The keys correspond to the column labels. The values or lists corresponding to the rows.

```python
songs = {'Album': 'Thriller', 'Back in Black', 'The Dark Side of the Moon',\
'The Bodyguard', 'Bat Out of Hell',
'Released': [1982,1980,1973,1992,1977],
'Length': ['00:42:19','00:42:11','00:42:49','00:57:44','00:46:33']}

# Cast the dictionary to a dataframe
df = pd.DataFrame(songs)

#display the result df
df
```

`unique()` --> to get the unique elements of a column

```python
df['Released'].unique()
```

<h5><span style="color: #3588e9">Column Selection:</span></h5>
Retrieve the data present in the `Album` column

```python
#Retrieving the "ID" column and assigning it to a variable x
x = df[['Album']]
x
```

To select the corresponding columns using inequality operators for the entire data frame in Pandas: 

```python
# specify one column -> The result is a series of Boolean values.
df['Released']>=1980

# select the specified columns in one line
df1=df[df['Released']>=1980] # new data frame

# Save the new data frame using the method to_csv
df1.to_csv('new_songs.csv') # The argument is the name of the csv file
```

<strong style="color: #3588e9">Access to multiple columns</strong>

Retrieve the data for ==Album== and ==Released== columns

```python
#Retrieving the Album, Released columns and assigning it to a variable z

z = df[['Album','Released']]
z
```

<strong style="color: #3588e9">Accessing Rows</strong>

Rows can be access by their index using `.iloc[]` or by label using `.loc[]`.

- `loc()` --> label-based data selecting method which means that we have to pass the name of the row or column that we want to select. This method includes the last element of the range passed in it.
<br>
- `iloc()` --> indexed-based selecting method which means that we have to pass an integer index in the method to select a specific row/column. This method does not include the last element of the range passed in it.

```python
# Access the value on the first row and the third column
df.iloc[0,2]
```

```python
# Access the column using the name
df.loc[0, 'Released']
```

Create a new dataframe called 'df2' and assign 'df' to it:

```python
df2 = df
df2 = df2.set_index("Album")
```

```python
# Access the column using the name
df2.loc['Thriller', 'The Bodyguard']
```

<strong style="color: #3588e9">Slicing:</strong>

- syntax: `data[start:stop]`

Data Frames can be sliced to select specific data values using a row and column location.

```python
# slicing using old dataframe df
df.iloc[0:2, 0:3]
```

- using both the index and the name of the column: 

```python
# Slicing the dataframe using name
df.loc[0:2, 'Artist':'Released']
```
<h5><span style="color: #3588e9">Conditional Filtering:</span></h5>

```python
high_above_102 = df[df['Age'] > 25]
```
<h5><span style="color: #3588e9">Saving DataFrames:</span></h5>
To save a DataFrame to a CSV file, use the to_csv method and specify the filename with a “.csv” extension. Pandas provides other functions for saving DataFrames in different formats.

```python
df.to_csv('trading_data.csv', index=False)
```

<h5><span style="color: #3588e9">DataFrame Attributes and Method</span></h5>
DataFrames provide numerous attributes and methods for data manipulation and analysis, including:

- **shape**: Returns the dimensions (number of rows and columns) of the DataFrame.
- **info()**: Provides a summary of the DataFrame, including data types and non-null counts.
- **describe()**: Generates summary statistics for numerical columns.
- **head(), tail()**: Displays the first or last n rows of the DataFrame.
- **mean(), sum(), min(), max()**: Calculate summary statistics for columns.
- **sort_values()**: Sort the DataFrame by one or more columns.
- **groupby()**: Group data based on specific columns for aggregation.
- **fillna(), drop(), rename()**: Handle missing values, drop columns, or rename columns.
- **apply()**: Apply a function to each element, row, or column of the DataFrame.

> Pandas offers a wide range of methods beyond these examples. For more detailed information, please refer to the official documentation available on the [Pandas official website](https://pandas.pydata.org/docs/ "Pandas official website").

<h5><span style="color: #3588e9">Reading XML files</span></h5>

```python
import pandas as pd
import xmk.etree.ElementTree as etree

# Use etree attribute to parse 'xml' file
tree = etree.parse("fileExample.txt")
root = treee.getroot()

# Add the column headers and assign then to the dataframe
columns = ["Name", "Phone Number", "Birthday"]
df = pad.DataFrame(columns = columns)
```

```python
# Collect the necessary data and append the data to a dataframe

for node in root:
	name = node.find("name").text
	phonenumber = node.find("phonenumber").text
	birthday = node.find("birthday").text

df = df.append(pd.Series([name, phonenumber, birthday], index = columns)..., ignore_index = True)
```
#### <span style="color:#c6554f">API Library</span>

When a Pandas object is created with the data frame constructor, in API lingo (instance). The data in the dictionary is passed along to the pandas API, and then the data frame is used to communicate with the API.

`head()` --> when it's called, the data frame communicates with the API displaying the first few rows of the data frame.

`mean()` --> the API will calculate the mean and return the values

```python
import pandas as pd
import matplotlib.pyplot as plt

dict_={'a':[11,21,31],'b':[12,22,32]}
df = pd.DataFrame(dict_)

df.head()
df.mean()
```
###### <span style="color: #3588e9">REST APIS - NBA</span>

```python
!pip install nba_api
from nba_api.stats.static import teams
import matplotlib.pyplot as plt

def one_dict(list_dict):
    keys=list_dict[0].keys()
    out_dict={key:[] for key in keys}
    for dict_ in list_dict:
        for key, value in dict_.items():
            out_dict[key].append(value)
    return out_dict
```

```python
nba_teams = teams.get_teams() # returns a list of dictionaries
nba_teams[0:3]
```

Convert the dictionary to a table:

```python
dict_nba_team=one_dict(nba_teams)
df_teams=pd.DataFrame(dict_nba_team)
df_teams.head()
```

```python
df_warriors=df_teams[df_teams['nickname']=='Warriors']
df_warriors
```

Access the first column of the DataFrame:

```python
id_warriors=df_warriors[['id']].values[0][0]
# integer that can be used to request the Warriors information
id_warriors
```

The function "League Game Finder " will make an API call, it's in the module `stats.endpoints`.

```python
from nba_api.stats.endpoints import leaguegamefinder
```

The parameter `team_id_nullable` is the unique ID for the warriors. Under the hood, the NBA API is making a HTTP request. The information requested is provided and is transmitted via an HTTP response this is assigned to the object `game finder`.

```python
gamefinder = leaguegamefinder.LeagueGameFinder(team_id_nullable=id_warriors)
```

To see the json file by running the following line of code:

```python
gamefinder.get_json()
```

The game finder object has a method `get_data_frames()`, that returns a dataframe. The `PLUS_MINUS` column contains information on the score, if the value is negative, the Warriors lost by that many points, if the value is positive, the warriors won by that amount of points. The column `MATCHUP` has the team the Warriors were playing, GSW stands for Golden State Warriors and TOR means Toronto Raptors. `vs` signifies it was a home game and the `@` symbol means an away game.

```python
games = gamefinder.get_data_frames()[0]
games.head()
```

Download the dataframe from the API call for Golden State and run the rest like a video.

```python
import requests

filename = "https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/PY0101EN/Chapter%205/Labs/Golden_State.pkl"

def download(url, filename):
    response = requests.get(url)
    if response.status_code == 200:
        with open(filename, "wb") as f:
            f.write(response.content)

download(filename, "Golden_State.pkl")
```

```python
file_name = "Golden_State.pkl"
games = pd.read_pickle(file_name)
games.head()
```

Create two dataframes, one for the games that the Warriors faced the raptors at home, and the second for away games.

```python
games_home=games[games['MATCHUP']=='GSW vs. TOR']
games_away=games[games['MATCHUP']=='GSW @ TOR']
```

Calculate the mean for the column `PLUS_MINUS` for the data frames `games_home` and  `games_away`:

```python
games_home['PLUS_MINUS'].mean()
games_away['PLUS_MINUS'].mean()
```

Plot out the `PLUS MINUS` column for the data frames `games_home` and  `games_away`. We see the warriors played better at home.

```python
fig, ax = plt.subplots()

games_away.plot(x='GAME_DATE',y='PLUS_MINUS', ax=ax)
games_home.plot(x='GAME_DATE',y='PLUS_MINUS', ax=ax)
ax.legend(["away", "home"])
plt.show()
```

###### <span style="color: #3588e9">Randomuser</span>

```python
!pip install randomuser

# Load the necessary libraries.
from randomuser import RandomUser
import pandas as pd

# Create a random user object
r = RandomUser()

some_list = r.generate_users(10)
some_list

name = r.get_full_name()

for user in some_list:
    print (user.get_full_name()," ",user.get_email())
```
###### <span style="color: #3588e9">Crypto Currency</span>

Crypto Currency data is excellent to be used in an API because it is being constantly updated and it is vital to CryptoCurrency Trading

Py-Coin-Gecko Python Client/Wrapper for the Coin Gecko API, updated every minute by Coin-Gecko
easy to use so you can focus on the task of collecting data

Usage:

```python
!pip install pycoingecko
from pycoingecko import CoinGeckoAPI

cg = CoinGeckoAPI() # Coin Gecko object

# Use a fucntion to request the data
bitcoin_data = cg.get_coin_market_by_id(id='bitcoin', vs_currency='usd', days=30) # python dictionary of nested lists
```

Convert the nested list to a DataFrame:

```python
data = pd.DataFrame(bitcoin_price_data, cloumns=['TimeStamp', 'Price'])
```

Convert it to a more readable format using the pandas function `to_datetime`:

```python
data['Date'] = pd.to_datetime(data['TimeStemp'], unit='ms')
```

To create a candle stick plot:

```python
candlestick_data = data.groupby(data.Date.dt.date).agg({'Price': ['min', 'max', 'first', 'last']})
```

Use `plotly` to create the candlestick chart and plot it:

```python
fig = go.Figure(data = [go.Candlestick(x = candlestick_data.index, open = candlestick_data['Price']['first'],
high = candlestick_data['Price']['max'],
low = candlestick_data['Price']['min'],
close = candlestick_data['Price']['last'])
])

fig.update_layout(xaxis_rangeslider_visible=False, xaxis_title='Date', yaxis_title='Price (USD $)', title='Bitcoin CandleStick Chart Over Past 30 days' )
```
