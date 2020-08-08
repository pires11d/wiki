# Python - Abrindo arquivos (I/O)
> Autor: Lucas Joshua Pires

## 1. Flat files
- opening with Python's original function
~~~python
filename = 'file.txt'
file = open(filename,mode='r')
text = file.read()
file.close()
~~~

- opening with **numpy**
~~~python
import numpy as np

filename = 'MNIST.txt'
data = np.loadtxt(filename,delimiter=',') #comma
data = np.loadtxt(filename,delimiter='\t',dtype=str) #tab
data = np.genfromtxt(filename,delimiter=',',names=True,dtype=None)
data = np.recfromcsv(filename)
~~~

- opening with **pandas**
~~~python
import pandas as pd

filename = 'file.csv'
data = pd.read_csv(filename)
data = pd.read_csv(file, sep='\t', comment='#', na_values='Nothing')
~~~

- opening from URL with **pandas**
~~~python
import pandas as pd

url = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1606/datasets/winequality-red.csv'
df_csv = pd.read_csv(url,";")
~~~

## 2. Excel files with **pandas**
- opening local file
~~~python
import pandas as pd

filename = 'sheet.xlsx'
data = pd.ExcelFile(filename)
df = data.sheet_names
df1 = data.parse('Sheet1') 
df2 = data.parse(1)
~~~
- opening from URL
~~~python
import pandas as pd

url = 'http://s3.amazonaws.com/assets.datacamp.com/course/importing_data_into_r/latitude.xls'
df_xl = pd.read_excel(url,sheetname=None)
print(df_xl.keys())
print(df_xl['1700'].head())
~~~

## 3. Pickle files (.pkl) with **pickle**
~~~python
import pickle

with open('data.pkl','rb') as file:
    d = pickle.load(file)
#creating pickle file
dump()
#loading pickle file
load()
~~~

## 4. SAS files ("Statistical Analysis System") with **pandas**
~~~python
import pandas as pd

from sas7bdat import SAS7BDAT
with SAS7BDAT('data.sas7bdat') as file:
    df = file.to_data_frame()
~~~

## 5. Stata files ("Statistics + Data") with **pandas**
~~~python
import pandas as pd

data = pd.read_stata('data.dta')
~~~

## 6. HDF5 files with **h5py**
~~~python
import h5py

filename = 'data.hdf5'
data = h5py.File(filename,'r')
~~~

## 7. MATLAB files with **scipy**
~~~python
import scipy.io

filename = 'workspace.mat'
mat = scipy.io.loadmat(filename)
~~~

## 8. SQL databases with **sqlalchemy** and **pandas**
~~~python
from sqlalchemy import create_engine
import pandas as pd

engine = create_engine('sqlite:///Northwind.sqlite')
table_names = engine.table_names()

#first option
con = engine.connect()
rs = con.execute("SELECT * FROM Orders")
df = pd.DataFrame(rs.fetchall())
df.columns = rs.keys()
con.close()

#second option
df = pd.read_sql_query("SELECT * FROM Orders",engine)
~~~

## 9. Online flat files with **urllib** or **requests**

- opening with urllib.request.**urlretrieve**
~~~python
from urllib.request import urlretrieve

url = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1606/datasets/winequality-red.csv'
urlretrieve(url,'winequality-red.csv')
~~~

- opening with urllib.request.**urlopen** and urllib.request.**Request**
~~~python
from urllib.request import urlopen,Request

url = "https://www.wikipedia.org"
request = Request(url)
response = urlopen(request)
html = response.read()
response.close()
~~~
- opening from URL with **requests**
~~~python
import requests

url = "https://www.wikipedia.org"
r = requests.get(url)
text = r.text
~~~

## 11. Scraping the web with **BeautifulSoup**
~~~python
from bs4 import BeautifulSoup
import requests

url = "https://www.crummy.com/software/BeautifulSoup/"
r = requests.get(url)
html_doc = r.text
soup = BeautifulSoup(html_doc)
soup.prettify()
text = soup.get_text()
title = soup.title
links = soup.find_all('a')
for link in links:
    print(link.get('href'))
~~~

# Opening JSON file
- local file with **json**
~~~python
import json

with open('data.json') as json_file:
    json_data = json.load(json_file)
for k in json_data.keys():
    print(k + ': ', json_data[k])
~~~

- from URL with **requests**
~~~python
import requests

url = "http://www.ombdapi.com/?apikey=ff21610b&t=the+social+network"
r = requests.get(url)
json_data = r.json()
~~~

## Using Tweepy
~~~python
import tweepy, json

access_token = "..."
access_token_secret = "..."
consumer_key = "..."
consumer_secret = "..."

auth = tweepy.OAuthHandler(consumer_key,consumer_secret)
auth.set_access_token(access_token,access_token_secret)

l = MyStreamListener()
stream = tweepy.Stream(auth,l)
stream.filter(track=['apples','bananas'])
~~~

- Searching word in text
~~~python
import re

def word_in_text(word, text):
    word = word.lower()
    text = tweet.lower()
    match = re.search(word, text)

    if match:
        return True
    return False
~~~
