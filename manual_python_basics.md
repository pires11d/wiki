# Python - Estruturas básicas
> Autor: Lucas Joshua Pires


Mudanças do Python 2 para Python 3:
- 1.0 		--> 1
- Tkinter 	--> tkinter
- print value --> print(value)

## 1. Tipos de variáveis
~~~py
	float = 3.14
	int = 2
	str = 'oi'
	bool = True or False
	list = [1, 2, 3] or [3.14, 2, 'oi'] or ['oi', 3.14, True]
~~~

## 2. Funções vs. Métodos
~~~py
	# function example:
		max(np_array1)

	# method example:
		np_array1.shape
		
	# index example:
		np_array1[1]
~~~	
		
## 3. Trabalhando com listas
~~~py
	# List indexing:
		list1 = [10, 20, 30, 40, 50]
				0	1	 2	 3	 4
		list1[0] = 10
		list1[1] = 20
		list1[-1] = 50
		list1[:2] = list1[0:2] = [10, 20]			excludes 2 --> [0,2[
		list1[2:] = list1[2:5] = [30, 40, 50]		includes 2 --> [2,4]	can also use	list1[2:1000]

	# Creating a new List:
	list2 = list(list1)
	
	# Removing items from a List:
	list.remove(item)
~~~

## 4. Operadores booleanos
- and

		True and True = True
		False and True = False
		True and False = False
		False and False = False
- or

		True or True = True
		False or True = True
		True or False = True
		False or False = False
- not

		not False = True
		not True = False

		
## 5. Operadores comparativos
	<, <=, >, >=, ==, !=
	
	
## 6. Operadores condicionais
~~~py
if (condition) :
	expression1
else :
	expression2
~~~

~~~py
if (condition1) :
	expression1
elif (condition2) :
	expression2
else :
	expression3
~~~

## 7. While loop
~~~py
while (condition) :
	expression
~~~
		
## 8. For loop
~~~py
for element in array :
	expression
~~~
		
~~~py
for index, element in enumerate(array) :
	expression
~~~
		
Mais exemplos com o uso do **for**:

~~~py
#List loop
	for value in list1:
	
#List loop with index (FUNCTION!)
	for i, value in enumerate(list1):

#Numpy array loop
	for value in np_array1:

#Numpy 2D-array loop (FUNCTION!)
	for value in np.nditer(np_array1):

#Dictionary loop (METHOD!)
	for key, value in dict1.items():

#Pandas DataFrame loop (METHOD!)
	for label, row in df.iterrows():
~~~
	
## 9. Dicionários
Basically a list indexed by unique keys, instead of integers!
~~~py
#Creating a dictionary:
	dict1 = {'key1':value1, 'key2':value2}

#Show keys only:
	dict1.keys()
dict_keys(['key1', 'key2'])

#Adding another pair of points:
	dict1['key3'] = value3

#Removing a pair of points:
	del(dict1['key3'])

#Creating a dictionary of dictionaries:
	dict01 = {'key01':dict1, 'key02':dict2, 'key03':dict3}	
~~~
	
## 10. Arrays com **numpy**

### Diferença entre LIST e ARRAY:
~~~py
import numpy as np

# list: can contain multiple types of elements
list1 = ['árvore', 4.1, False]  

# array: can only contain one type of element
array1 = np.array([1, 2, 3])
		
# Boolean operators for arrays:
	np.logical_and(array1, array2)
	np.logical_or(array1, array2)
	np.logical_not(array1, array2)
~~~

### Lidando com probabilidade:
~~~py	
# Random Numbers:
np.random.seed(123)
np.random.rand()
np.random.randint(0,2) --> 2 is excluded!

# Random Step
step = 0
dice = np.random.randint(1,7)
if dice<=2 :
	step = step - 1
elif dice<=5 :
	step = step + 1
else :
	step = step + np.random.randint(1,7)
print(step)

# Random Walk
random_walk = [0]
for x in range(10) :
	step = random_walk[-1]
	dice = np.random.randint(1,7)
	if dice<=2 :
		step = step - 1
	elif dice<=5 :
		step = step + 1
	else :
		step = step + np.random.randint(1,7)
	random_walk.append(step)
print(random_walk)

# Distribution
all_walks = []
for x in range(10) :
	random_walk = [0]
	for x in range(100) :
		step = random_walk[-1]
		dice = np.random.randint(1,7)
		if dice<=2 :
			step = step - 1
		elif dice<=5 :
			step = step + 1
		else :
			step = step + np.random.randint(1,7)
		random_walk.append(step)
	all_walks.append(random_walk[-1])
print(all_walks)		
~~~

### Cara ou Coroa
~~~py
# Random Step
outcomes = []
for x in range(10) :
	coin = np.random.randint(0,2)
	if coin == 0 :
		outcomes.append('heads')
	else :
		outcomes.append('tails')
print(outcomes)

# Random Walk
tails = [0]
for x in range(10) :
	coin = np.random.randint(0,2)
	tails.append(tails[x]+coin)
print(tails)
	
# Distribution
final_tails = []
for x in range(100) :
	tails = [0]
	for x in range(10) :
		coin = np.random.randint(0,2)
		tails.append(tails[x]+coin)
	final_tails.append(tails[-1])
print(final_tails)
~~~

## 11. Dataframes com **pandas**
~~~py
import pandas as pd

# Creating a dict:
dict1 = {'key1':[1, 2, 3],
			'key2':[4, 5, 6],
			'key3':[7, 8, 9]}
			
# Creating a DataFrame:
df = pd.DataFrame(dict1)
>df:
	key1 key2 key3
	0	1	2	3
	1	4	5	6
	2	7	8	9

# Changing index column:
df.index = ['index1', 'index2', 'index3']
>df:
	key1 key2 key3
	index1	1	2	3
	index2	4	5	6
	index3	7	8	9

# Reading data from a CSV:
df1 = pd.read_csv('path/data.csv', index_col = 0)

# Removing NaN values:
df2 = df1.dropna(axis=0, how='any')
df2 = df1.dropna(axis=0, how='all')
df2 = df1.dropna(axis=1, how='any')
df2 = df1.dropna(axis=1, how='all')

# Accessing lines:
df2[0]					--> one row by index
df2.loc['name1']			--> one row as series
df2.loc[['name1']] 			--> one row as DataFrame
df2.iloc[[0]]				--> one row as DataFrame

# Accessing columns:
df2['key1']				--> one column as series
df2[['key1']] 				--> one column as DataFrame
df2.loc[:,['key1']]			--> one column as DataFrame
df2.iloc[:,[0]]				--> one column as DataFrame

df2[['key1', 'key2']]			--> multiple columns as DataFrame
df2.loc[:,['key1','key2']]		--> multiple columns as DataFrame
df2.iloc[:,[0,1]]			--> multiple columns as DataFrame

# Accessing some part of the matrix:
df2.loc[['index2','index3'], ['key1','key3']]
df2.iloc[[1,2], [0,2]]
df2.values[i][j]
df2.ix['key1','key2']

# Operators with DataFrame:
subdf = df['key2']
between = np.logical_and(df > 100, df < 200)
result = df[between]

# Creating a pivot table:
df3 = df2.pivot_table(['key_value'], index=['key1','key2','key3'])
~~~

