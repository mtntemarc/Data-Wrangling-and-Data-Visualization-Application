## Metante_ProgrammingAssignment_4
# EXPERIMENT 4 - Data Wrangling and Data Visualization - Metante

# I. Intended Learning Outcomes:
1. To identify the codes and functions needed in cleaning and visualizing data
   
2. To be able to apply and use the different codes and functions in creating a Python program that will be used in data wrangling and data visualization

# II. Instructions:
Download the ECE Board Exam 2 dataset found on this link: bit.ly/ECEBoardExamDataset and write a Python script/code in the Jupyter Notebook to do the given problems. You may submit your Jupyter notebook in the dedicated submission bin.

# ECE BOARD EXAM PROBLEM: Using data wrangling and data visualization technique with storytelling, analyze the data and present different (i) data frames; and (ii) visuals using the dataset given.

## 1. Create the following data frames based on the format provided: Example: Vis = [“Name”, “Gender”, “Track”, “Math<70”]; hometown is constant as Visayas
   
   A. Filename: Instru = [“Name”, “GEAS”, “Electronics >70”]; where track is constant as Instrumentation and hometown Luzon
   
   B. Filename: Mindy = [ “Name”, “Track”, “Electronics”, “Average >=55”]; where hometown is constant as Mindanao and gender Female


# Problem #1 – Creating Required DataFrames

## We will filter the dataset based on the conditions given and construct two new DataFrames: Instru and Mindy.

A. Instru = [“Name”, “GEAS”, “Electronics >70”]

Condition: Track = Instrumentation, Hometown = Luzon

a. Import pandas and read the dataset.
```
import pandas as pd
board = pd.read_csv('board2.csv')
```

b. Filter rows where Hometown = Luzon and Track = Instrumentation.
```
data = board.loc[(board['Hometown']=='Luzon') & (board['Track']=='Instrumentation')]

```
c. Add condition Electronics > 70.
```
data = data.loc[data['Electronics'] > 70]

```
d. Select required columns.
```
Instru = data[['Name','GEAS','Electronics']]
```

Full Code – Instru
```
import pandas as pd
board = pd.read_csv('board2.csv')

data = board.loc[(board['Hometown']=='Luzon') & 
                 (board['Track']=='Instrumentation') & 
                 (board['Electronics'] > 70)]

Instru = data[['Name','GEAS','Electronics']]
Instru
```
<img width="467" height="170" alt="image" src="https://github.com/user-attachments/assets/01737ae4-215f-442a-bcdb-b882679de3f1" />


B. Mindy = [“Name”, “Track”, “Electronics”, “Average >=55”]

Condition: Hometown = Mindanao, Gender = Female

a. Filter rows where Hometown = Mindanao and Gender = Female.
```
data2 = board.loc[(board['Hometown']=='Mindanao') & (board['Gender']=='Female')].copy()
```

b. Compute the Average column.
```
data2['Average'] = data2[['Math', 'Electronics', 'Communication','GEAS']].mean(axis=1)
```

c. Filter only those entries with Average ≥ 55.
```
Mindy = data2.loc[data2['Average'] >= 55]

```
d. Select required columns.
```
Mindy[['Name','Track','Electronics','Average']]
```

Full Code – Mindy
```
data2 = board.loc[(board['Hometown']=='Mindanao') & (board['Gender']=='Female')].copy()

data2['Average'] = data2[['Math', 'Electronics', 'Communication','GEAS']].mean(axis=1)

Mindy = data2.loc[data2['Average'] >= 55]
Mindy[['Name','Track','Electronics','Average']]
```

<img width="597" height="243" alt="image" src="https://github.com/user-attachments/assets/d3c68e52-c959-41cb-ab4a-89f5095b5fa5" />

# Problem #2 – Visualization of Features vs. Average Grade

We now check how Track, Gender, and Hometown affect the Average grade.

a. Import visualization libraries.
```
import matplotlib.pyplot as plt
import seaborn as sns
```

b. Add an Average column.
```
board['Average'] = board[['Math','Electronics','Communication','GEAS']].mean(axis=1)
```

c. Create a figure with three subplots (Track, Gender, Hometown).
```
plt.figure(figsize=(20,10))

```
d. Plot 1: Average Grade by Track.
```
plt.subplot(1,3,1)
sns.boxplot(x='Track', y='Average', data=board, hue='Track', palette='Set2')
plt.title('Average Grade by Track')
plt.xticks(rotation=45)
```

e. Plot 2: Average Grade by Gender.
```
plt.subplot(1,3,2)
sns.boxplot(x='Gender', y='Average', data=board, hue='Gender', palette='Set1')
plt.title('Average Grade by Gender')

```
f. Plot 3: Average Grade by Hometown.
```
plt.subplot(1,3,3)
sns.boxplot(x='Hometown', y='Average', data=board, hue='Hometown', palette='Set3')
plt.title('Average Grade by Hometown')
```

g. Adjust layout and show.
```
plt.tight_layout()
plt.show()
```

Full Code – Visualization
```
import matplotlib.pyplot as plt
import seaborn as sns

board['Average'] = board[['Math','Electronics','Communication','GEAS']].mean(axis=1)

plt.figure(figsize=(20,10))

plt.subplot(1,3,1)
sns.boxplot(x='Track', y='Average', data=board, hue='Track', palette='Set2')
plt.title('Average Grade by Track')
plt.xticks(rotation=45)

plt.subplot(1,3,2)
sns.boxplot(x='Gender', y='Average', data=board, hue='Gender', palette='Set1')
plt.title('Average Grade by Gender')

plt.subplot(1,3,3)
sns.boxplot(x='Hometown', y='Average', data=board, hue='Hometown', palette='Set3')
plt.title('Average Grade by Hometown')

plt.tight_layout()
plt.show()

```
Output: 

<img width="1371" height="677" alt="image" src="https://github.com/user-attachments/assets/fad80746-e19f-47f2-b748-9c8198378edd" />

## Marc Gabriel G. Metante UST-ECE

