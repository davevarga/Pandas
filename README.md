# Loading data into pandas

The first thing we are going to do is loadig the pandas library. The object type that pandas allow you to manipulate data is *dataframe*. We can import the data from a cvs file. It is recommended to save the file in the same folder as the Jupyter Notebook.

Pandas can also load excel files or txt files. In case of a .txt file, panda .read_csv() function accepts a delimiter parameter, with which you can get the formated dataframe.


```python
import pandas

dataframe = pandas.read_csv('pokemon_data.csv')

dataframe.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



# Reading data into pandas

While the print() function can be used, a much nicer way to visualize pandas dataframe is using naked functions. We can output the mentioned dataframe in multiple ways:
- We can output the head of the dataframe, specifying how many rows to be displayed.
- We can output the header of the dataframe. The output is the list of column names.
- Each row using as a lockup function, as we as list format.
- Find rows that satisfies a query formula.
- Find element at specific location

Furthermore we can arrange rows using the ascending parameter, along with the name of the column. If multiple column names are specified, the sorting order can be determined by the list of columns, while the method of sorting is given to the ascending parameter as a list. Data can be sorted numerically as well as alphabetically.


```python
## Read headers
print(dataframe.columns)

## Dataframe column projection
print(dataframe[['Name', 'Type 1', 'HP']])

## Read integer location interval (first 4 rows, first 7 columns)
print(dataframe.sort_values(['Type 1', 'HP'], ascending=[True, False]).iloc[0:4, 0:7])

## Access only the rows that satisfies a formula
print(dataframe.iloc[0:20, 0:7].loc[dataframe['Type 1'] == 'Fire'])
```

    Index(['#', 'Name', 'Type 1', 'Type 2', 'HP', 'Attack', 'Defense', 'Sp. Atk',
           'Sp. Def', 'Speed', 'Generation', 'Legendary'],
          dtype='object')
                          Name   Type 1  HP
    0                Bulbasaur    Grass  45
    1                  Ivysaur    Grass  60
    2                 Venusaur    Grass  80
    3    VenusaurMega Venusaur    Grass  80
    4               Charmander     Fire  39
    ..                     ...      ...  ..
    795                Diancie     Rock  50
    796    DiancieMega Diancie     Rock  50
    797    HoopaHoopa Confined  Psychic  80
    798     HoopaHoopa Unbound  Psychic  80
    799              Volcanion     Fire  80
    
    [800 rows x 3 columns]
           #                     Name Type 1    Type 2  HP  Attack  Defense
    520  469                  Yanmega    Bug    Flying  86      76       86
    698  637                Volcarona    Bug      Fire  85      60       65
    231  214                Heracross    Bug  Fighting  80     125       75
    232  214  HeracrossMega Heracross    Bug  Fighting  80     185      115
       #                       Name Type 1  Type 2  HP  Attack  Defense
    4  4                 Charmander   Fire     NaN  39      52       43
    5  5                 Charmeleon   Fire     NaN  58      64       58
    6  6                  Charizard   Fire  Flying  78      84       78
    7  6  CharizardMega Charizard X   Fire  Dragon  78     130      111
    8  6  CharizardMega Charizard Y   Fire  Flying  78     104       78
    

# Making changes to the data

We can define new data to the dataframe. It is common practice to define new columns to the data, such that it reflects certain aspects of the information. Such variables are coled **indexes**.


```python
## Creating new column
dataframe['Points'] = dataframe['HP'] + dataframe['Attack'] + dataframe['Defense'] + dataframe['Speed']

## Print changes
dataframe.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
      <th>Points</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
      <td>188</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
      <td>245</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>325</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>383</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
      <td>199</td>
    </tr>
  </tbody>
</table>
</div>



The following solution is specific to Jupyter Notebook. Because variables are stored in memory in between runs, we can drop columns and then reference them again. If we want to make a permanent change in the dataframe, then we must use the *del* operation. This is not a python operator, but unique to Jupyter Notebook.

Python encourages less but more functional code. By using the *iloc()* function we can manipulate the dataframe more easily. Furthermore lets elegantly rearrange the columns at the end.

Note: If we leave out the brackets when referencing cols[-1], then python interpreter will try in vain, to concatanate a list with a string type variable.


```python
## Drop the new column
dataframe = dataframe.drop(columns=['Points'])

## Solving the problem again
dataframe['Total'] = dataframe.iloc[:, 4:10].sum(axis=1)

## Rearrange the columns
cols = list(dataframe.columns.values)
dataframe = dataframe[cols[0:4] + [cols[-1]] + cols[4:12]]

## Output
dataframe.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



Because the data structure can change over time, I advise against hardcoding numbers in the program. Columns should instead be referred by name not coordinates.

# Saving data with pandas

The saving of the data is straight forward. The saving in itself can be done by a single line of code. There is the option to save to other file formats as well.

The default saving method will write the indexes of the rows as well. We can change this behaviour using the *index* parameter. Writing into .txt file might be tricky, so the *sep* parameter might come in handy, mirroring the same function as the loading method.


```python
# Exporting data structure into csv
dataframe.to_csv("modified.csv", index=False)

# Exporting data structure into excel
dataframe.to_excel('modified.xlsx', index=False)

# Exporting data structure int text file
dataframe.to_csv('modified.txt', index=False, sep='\t')
```

# Filtering Data

Now moving forward with more complex methods, where the pandas library proves to be a useful. The most common way to filter data is using the *loc* method.


```python
new_df = dataframe.loc[(dataframe['Type 1'] == 'Grass') 
                       & (dataframe['Type 2'] == 'Poison') 
                       & (dataframe['HP'] > 70)]
new_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>50</th>
      <td>45</td>
      <td>Vileplume</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>490</td>
      <td>75</td>
      <td>80</td>
      <td>85</td>
      <td>110</td>
      <td>90</td>
      <td>50</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>77</th>
      <td>71</td>
      <td>Victreebel</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>490</td>
      <td>80</td>
      <td>105</td>
      <td>65</td>
      <td>100</td>
      <td>70</td>
      <td>70</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>652</th>
      <td>591</td>
      <td>Amoonguss</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>464</td>
      <td>114</td>
      <td>85</td>
      <td>70</td>
      <td>85</td>
      <td>80</td>
      <td>30</td>
      <td>5</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



Although very useful, the method might have some shortcomings. First, the index of the filtered dataframe references the previous index of the row. This can be fixed, by reseting the index, using the *reset_index()* function:
- *drop* parameter deletes the previous indexes, otherwise these will appear next to the new indexes
- *inplace* parameter conserves the overriding operator, saving it in place.

Note: The hash mark column might appear to be the index column, it does not correspond to the index column syntax of pandas library. It instead is a pseudo index column injected while loading the data from .csv file.


```python
new_df.reset_index(drop=True, inplace=True)
new_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>45</td>
      <td>Vileplume</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>490</td>
      <td>75</td>
      <td>80</td>
      <td>85</td>
      <td>110</td>
      <td>90</td>
      <td>50</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>71</td>
      <td>Victreebel</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>490</td>
      <td>80</td>
      <td>105</td>
      <td>65</td>
      <td>100</td>
      <td>70</td>
      <td>70</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>591</td>
      <td>Amoonguss</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>464</td>
      <td>114</td>
      <td>85</td>
      <td>70</td>
      <td>85</td>
      <td>80</td>
      <td>30</td>
      <td>5</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



 There are other types of conditions as well. Let's say we want to filter out all the names that contains *Mega*. We can get the corresponding inverted table of the query by simply negating the statement.


```python
dataframe.loc[dataframe['Name'].str.contains('Mega')].head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Fire</td>
      <td>Dragon</td>
      <td>634</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
      <td>CharizardMega Charizard Y</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>634</td>
      <td>78</td>
      <td>104</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>12</th>
      <td>9</td>
      <td>BlastoiseMega Blastoise</td>
      <td>Water</td>
      <td>NaN</td>
      <td>630</td>
      <td>79</td>
      <td>103</td>
      <td>120</td>
      <td>135</td>
      <td>115</td>
      <td>78</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>19</th>
      <td>15</td>
      <td>BeedrillMega Beedrill</td>
      <td>Bug</td>
      <td>Poison</td>
      <td>495</td>
      <td>65</td>
      <td>150</td>
      <td>40</td>
      <td>15</td>
      <td>80</td>
      <td>145</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



The possibility of using **RegEx** formulas are also implemented in pandas. Regular expressions are supper useful while using data with textual patterns. We have to modify the query the following way.


```python
dataframe.loc[dataframe['Type 1'].str.contains('Fire|Grass', regex=True)]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>735</th>
      <td>667</td>
      <td>Litleo</td>
      <td>Fire</td>
      <td>Normal</td>
      <td>369</td>
      <td>62</td>
      <td>50</td>
      <td>58</td>
      <td>73</td>
      <td>54</td>
      <td>72</td>
      <td>6</td>
      <td>False</td>
    </tr>
    <tr>
      <th>736</th>
      <td>668</td>
      <td>Pyroar</td>
      <td>Fire</td>
      <td>Normal</td>
      <td>507</td>
      <td>86</td>
      <td>68</td>
      <td>72</td>
      <td>109</td>
      <td>66</td>
      <td>106</td>
      <td>6</td>
      <td>False</td>
    </tr>
    <tr>
      <th>740</th>
      <td>672</td>
      <td>Skiddo</td>
      <td>Grass</td>
      <td>NaN</td>
      <td>350</td>
      <td>66</td>
      <td>65</td>
      <td>48</td>
      <td>62</td>
      <td>57</td>
      <td>52</td>
      <td>6</td>
      <td>False</td>
    </tr>
    <tr>
      <th>741</th>
      <td>673</td>
      <td>Gogoat</td>
      <td>Grass</td>
      <td>NaN</td>
      <td>531</td>
      <td>123</td>
      <td>100</td>
      <td>62</td>
      <td>97</td>
      <td>81</td>
      <td>68</td>
      <td>6</td>
      <td>False</td>
    </tr>
    <tr>
      <th>799</th>
      <td>721</td>
      <td>Volcanion</td>
      <td>Fire</td>
      <td>Water</td>
      <td>600</td>
      <td>80</td>
      <td>110</td>
      <td>120</td>
      <td>130</td>
      <td>90</td>
      <td>70</td>
      <td>6</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
<p>122 rows × 13 columns</p>
</div>



Accordingly, getting all pokemons names that starts with *pi* can be requested in the following way:


```python
import re
dataframe.loc[dataframe['Name'].str.contains('^pi[a-z]*', flags=re.I, regex=True)]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20</th>
      <td>16</td>
      <td>Pidgey</td>
      <td>Normal</td>
      <td>Flying</td>
      <td>251</td>
      <td>40</td>
      <td>45</td>
      <td>40</td>
      <td>35</td>
      <td>35</td>
      <td>56</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>21</th>
      <td>17</td>
      <td>Pidgeotto</td>
      <td>Normal</td>
      <td>Flying</td>
      <td>349</td>
      <td>63</td>
      <td>60</td>
      <td>55</td>
      <td>50</td>
      <td>50</td>
      <td>71</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>22</th>
      <td>18</td>
      <td>Pidgeot</td>
      <td>Normal</td>
      <td>Flying</td>
      <td>479</td>
      <td>83</td>
      <td>80</td>
      <td>75</td>
      <td>70</td>
      <td>70</td>
      <td>101</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>23</th>
      <td>18</td>
      <td>PidgeotMega Pidgeot</td>
      <td>Normal</td>
      <td>Flying</td>
      <td>579</td>
      <td>83</td>
      <td>80</td>
      <td>80</td>
      <td>135</td>
      <td>80</td>
      <td>121</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>30</th>
      <td>25</td>
      <td>Pikachu</td>
      <td>Electric</td>
      <td>NaN</td>
      <td>320</td>
      <td>35</td>
      <td>55</td>
      <td>40</td>
      <td>50</td>
      <td>50</td>
      <td>90</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>136</th>
      <td>127</td>
      <td>Pinsir</td>
      <td>Bug</td>
      <td>NaN</td>
      <td>500</td>
      <td>65</td>
      <td>125</td>
      <td>100</td>
      <td>55</td>
      <td>70</td>
      <td>85</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>137</th>
      <td>127</td>
      <td>PinsirMega Pinsir</td>
      <td>Bug</td>
      <td>Flying</td>
      <td>600</td>
      <td>65</td>
      <td>155</td>
      <td>120</td>
      <td>65</td>
      <td>90</td>
      <td>105</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>186</th>
      <td>172</td>
      <td>Pichu</td>
      <td>Electric</td>
      <td>NaN</td>
      <td>205</td>
      <td>20</td>
      <td>40</td>
      <td>15</td>
      <td>35</td>
      <td>35</td>
      <td>60</td>
      <td>2</td>
      <td>False</td>
    </tr>
    <tr>
      <th>219</th>
      <td>204</td>
      <td>Pineco</td>
      <td>Bug</td>
      <td>NaN</td>
      <td>290</td>
      <td>50</td>
      <td>65</td>
      <td>90</td>
      <td>35</td>
      <td>35</td>
      <td>15</td>
      <td>2</td>
      <td>False</td>
    </tr>
    <tr>
      <th>239</th>
      <td>221</td>
      <td>Piloswine</td>
      <td>Ice</td>
      <td>Ground</td>
      <td>450</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>60</td>
      <td>60</td>
      <td>50</td>
      <td>2</td>
      <td>False</td>
    </tr>
    <tr>
      <th>438</th>
      <td>393</td>
      <td>Piplup</td>
      <td>Water</td>
      <td>NaN</td>
      <td>314</td>
      <td>53</td>
      <td>51</td>
      <td>53</td>
      <td>61</td>
      <td>56</td>
      <td>40</td>
      <td>4</td>
      <td>False</td>
    </tr>
    <tr>
      <th>558</th>
      <td>499</td>
      <td>Pignite</td>
      <td>Fire</td>
      <td>Fighting</td>
      <td>418</td>
      <td>90</td>
      <td>93</td>
      <td>55</td>
      <td>70</td>
      <td>55</td>
      <td>55</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>578</th>
      <td>519</td>
      <td>Pidove</td>
      <td>Normal</td>
      <td>Flying</td>
      <td>264</td>
      <td>50</td>
      <td>55</td>
      <td>50</td>
      <td>36</td>
      <td>30</td>
      <td>43</td>
      <td>5</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



# Conditional changes

Not that different from data filtering, we can modify certain data cells, that satisfies a condition.

Consequently, let's change all fire type pokemons to Flamer type.


```python
dataframe.loc[dataframe['Type 1'] == 'Fire', 'Type 1'] = 'Flamer'
dataframe.loc[dataframe['Type 1'] == 'Flamer'].head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Flamer</td>
      <td>NaN</td>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Charmeleon</td>
      <td>Flamer</td>
      <td>NaN</td>
      <td>405</td>
      <td>58</td>
      <td>64</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Charizard</td>
      <td>Flamer</td>
      <td>Flying</td>
      <td>534</td>
      <td>78</td>
      <td>84</td>
      <td>78</td>
      <td>109</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Flamer</td>
      <td>Dragon</td>
      <td>634</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
      <td>CharizardMega Charizard Y</td>
      <td>Flamer</td>
      <td>Flying</td>
      <td>634</td>
      <td>78</td>
      <td>104</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



We, of course, can change multiple parameters at the same time, as shown in the example bellow: 


```python
dataframe.loc[dataframe['Total'] > 500,
              ['Generation', 'Legendary']] = ['Test 1', 'Test 2']
dataframe.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>Test 1</td>
      <td>Test 2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>Test 1</td>
      <td>Test 2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Flamer</td>
      <td>NaN</td>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



# Aggregate Statistics

Aggregate statistics refers to groupings of certain type of data, in order to extract and visualize statistical information in case of numerical values, or quantify metrics such as the group size.


```python
# First load the original data
df = pandas.read_csv('pokemon_data.csv')

# Projecting only to numerical values
df = df[['Type 1', 'HP', 'Attack', 'Defense', 'Sp. Atk', 'Sp. Def', 'Speed']]

# Look at the average stats of certain type of pokemon
df.groupby(['Type 1']).mean().sort_values('Defense', ascending=True).head(6)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
    </tr>
    <tr>
      <th>Type 1</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Normal</th>
      <td>77.275510</td>
      <td>73.469388</td>
      <td>59.846939</td>
      <td>55.816327</td>
      <td>63.724490</td>
      <td>71.551020</td>
    </tr>
    <tr>
      <th>Fairy</th>
      <td>74.117647</td>
      <td>61.529412</td>
      <td>65.705882</td>
      <td>78.529412</td>
      <td>84.705882</td>
      <td>48.588235</td>
    </tr>
    <tr>
      <th>Fighting</th>
      <td>69.851852</td>
      <td>96.777778</td>
      <td>65.925926</td>
      <td>53.111111</td>
      <td>64.703704</td>
      <td>66.074074</td>
    </tr>
    <tr>
      <th>Flying</th>
      <td>70.750000</td>
      <td>78.750000</td>
      <td>66.250000</td>
      <td>94.250000</td>
      <td>72.500000</td>
      <td>102.500000</td>
    </tr>
    <tr>
      <th>Electric</th>
      <td>59.795455</td>
      <td>69.090909</td>
      <td>66.295455</td>
      <td>90.022727</td>
      <td>73.704545</td>
      <td>84.500000</td>
    </tr>
    <tr>
      <th>Psychic</th>
      <td>70.631579</td>
      <td>71.456140</td>
      <td>67.684211</td>
      <td>98.403509</td>
      <td>86.280702</td>
      <td>81.491228</td>
    </tr>
  </tbody>
</table>
</div>



Other aggregate statistics include:
- *mean()* gives the average of the numerical values in a group
- *sum()* returns the total value within a group
- *min()* expresses the smallest values
- *max()* the inverse of *min*
- *count()* quantifies the number of elements within a group

Let's try to express how many pokemons fall within each element:


```python
# Run the query
df.groupby(['Type 1']).count().head(3)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
    </tr>
    <tr>
      <th>Type 1</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bug</th>
      <td>69</td>
      <td>69</td>
      <td>69</td>
      <td>69</td>
      <td>69</td>
      <td>69</td>
    </tr>
    <tr>
      <th>Dark</th>
      <td>31</td>
      <td>31</td>
      <td>31</td>
      <td>31</td>
      <td>31</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Dragon</th>
      <td>32</td>
      <td>32</td>
      <td>32</td>
      <td>32</td>
      <td>32</td>
      <td>32</td>
    </tr>
  </tbody>
</table>
</div>



Note: Here we know that the dataset is a statistical analysis of each pokemon, thereafter each pokemon appears just one. In other case, we should clean the data beforehand, by filtering unique fields.

# Working with large amounts of data

Interesting fact about pandas library is that, in case of large amounts of data, instead of importing all of it into the memory, works with one chunk at a time.


```python
# Defining an empty, but matching dataframe
new_dataframe = pandas.DataFrame(columns=df.columns)

# Read 5 rows at a time
for df in pandas.read_csv('pokemon_data.csv', chunksize=5):
    results = df.groupby(['Type 1']).count()
    new_dataframe = pandas.concat([new_dataframe, results])
    
# Print the result
new_dataframe
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Fire</th>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Grass</th>
      <td>4</td>
      <td>4</td>
      <td>NaN</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Fire</th>
      <td>4</td>
      <td>4</td>
      <td>NaN</td>
      <td>3</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Water</th>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Bug</th>
      <td>2</td>
      <td>2</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Fairy</th>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Flying</th>
      <td>2</td>
      <td>2</td>
      <td>NaN</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Fire</th>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Psychic</th>
      <td>2</td>
      <td>2</td>
      <td>NaN</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Rock</th>
      <td>2</td>
      <td>2</td>
      <td>NaN</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
<p>433 rows × 12 columns</p>
</div>


