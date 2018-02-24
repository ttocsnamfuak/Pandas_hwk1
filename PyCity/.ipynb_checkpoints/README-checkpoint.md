

```python
#import dependencies
import pandas as pd
import numpy as np

```


```python
#file locations
student_csv = "raw_data/students_complete.csv"
schools_csv = "raw_data/schools_complete.csv"
```


```python
#read files into initial data frames
stu_df = pd.read_csv(student_csv)
sch_df = pd.read_csv(schools_csv)
```


```python
#stu_df.head()
```


```python
#sch_df.head()
```


```python
#stu_df.info(),sch_df.info()

```


```python
#stu_df.describe()
```


```python
#stu_df["name"].count()

```


```python
#sch_df["name"].count()
```


```python
#sch_df["budget"].sum()
```


```python
#stu_df["math_score"].mean()
```


```python
#stu_df["math_score"].count(math_score > 60)
nbr_passing = stu_df[stu_df["math_score"]>65].count()
       
#"math_score" > 60].count()
#df[df < 2.0 ].count()

```

**District Summary**

* Create a high level snapshot (in table form) of the district's key metrics, including:
  * Total Schools
  * Total Students
  * Total Budget
  * Average Math Score
  * Average Reading Score
  * % Passing Math
  * % Passing Reading
  * Overall Passing Rate (Average of the above two)


```python
#sch_df.head()
```


```python
# Calculate District Summary information

#nbr of schools
total_schools = sch_df["name"].count()

#nbr of students
total_students = stu_df["name"].count()

#total budget
total_budget = sch_df["budget"].sum()

#avg_math score
avg_math = stu_df["math_score"].mean()

#avg_reading score
avg_reading = stu_df["reading_score"].mean()

#Percent that are passing math
val = stu_df[stu_df["math_score"]>=65].count()
totMathPass = val["name"]
mathPass_percent = totMathPass/total_students

#mathPass_percent = stu_df[stu_df["math_score"]>65].count()/total_students

#Percent that are passing readingt
valHold = stu_df[stu_df["reading_score"]>=65].count()
totReadPass = valHold["name"]
readPass_percent = totReadPass/total_students

#readPass_percent = stu_df[stu_df["reading_score"]>65].count()/total_students

#Overall Pass rate
overallPass_rate = (mathPass_percent+readPass_percent)/2

```


```python
# Create a new table consolodating above calculations
district_breakdown = pd.DataFrame({"Total Schools": [total_schools],
                                   "Total Students": [total_students],
                                   "Total Budget": [total_budget],
                                   "Avg. Mathscore": [avg_math],
                                   "Avg. Reading Score": [avg_reading],
                                   "% Passing Math":[mathPass_percent],
                                   "% Passing Reading":[readPass_percent],
                                   "Overall Passing Rate": [overallPass_rate],
})
```


```python
#Print out district summary information
district_breakdown = district_breakdown[["Total Schools",
                                           "Total Students",
                                           "Total Budget",
                                           "Avg. Mathscore",
                                           "Avg. Reading Score",
                                           "% Passing Math",
                                           "% Passing Reading",
                                           "Overall Passing Rate"]]
district_breakdown = district_breakdown.round(2)
district_breakdown
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Avg. Mathscore</th>
      <th>Avg. Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39170</td>
      <td>24649428</td>
      <td>78.99</td>
      <td>81.88</td>
      <td>0.85</td>
      <td>0.96</td>
      <td>0.9</td>
    </tr>
  </tbody>
</table>
</div>



**School Summary**

* Create an overview table that summarizes key metrics about each school, including:
  * School Name
  * School Type
  * Total Students
  * Total School Budget
  * Per Student Budget
  * Average Math Score
  * Average Reading Score
  * % Passing Math
  * % Passing Reading
  * Overall Passing Rate (Average of the above two)


```python
#calculate the values and store in dictionaries

schSum_df = pd.DataFrame()         #create the school summary dataframe

schSum_df['school'] = sch_df["name"] #add the school names

schSum_df['type'] = sch_df["type"] #add the school types

schSum_df['size'] = sch_df["size"] #add the school sizes

schSum_df['budget'] = sch_df["budget"] #add the school budgets

schSum_df['perStu_budget'] = sch_df['budget']/sch_df['size'] #calc and add budget per student

schSum_df

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>perStu_budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
    </tr>
  </tbody>
</table>
</div>




```python

#Calculate school averages in math and reading
#create a school average dataframe
schAvg_df = pd.DataFrame()

#group by the schools
schGroup_df = stu_df.groupby(['school'])

#calculate the averages for math and reading by school group also get the count for the % calc

schAvg_df['math_avg'] = schGroup_df['math_score'].mean()
schAvg_df['math_count'] = schGroup_df['math_score'].count()
schAvg_df['reading_avg'] = schGroup_df['reading_score'].mean()
schAvg_df['reading_count'] = schGroup_df['reading_score'].count()

```


```python
#print(schAvg_df)
```


```python
#group by the schools in the passing math dataframe
#schMathValGroup = schMathVal_df.groupby(['school'])
#schMathValGroup['school']
```


```python
#Percent that are passing math >+ 65% into its own data frame
schMathVal_df = stu_df[stu_df["math_score"]>=65]

#group by the schools in the passing math dataframe
schMathValGroup = schMathVal_df.groupby(['school'])

#count the students per school >= 65
schAvg_df['Nbr Passing Math']=schMathValGroup['math_score'].count()


#Percent that are passing reading >= 65% into its own data frame
schReadVal_df = stu_df[stu_df["reading_score"]>=65]

#group by the schools in the passing math dataframe
schReadValGroup = schReadVal_df.groupby(['school'])

#count the students per school >= 65
schAvg_df['Nbr Passing Reading']=schReadValGroup['reading_score'].count()



#Calc %passing math
schAvg_df['%Passing Math']= (schAvg_df['Nbr Passing Math'] / schAvg_df['math_count'])

#calc %passing reading
schAvg_df['%Passing Reading']= (schAvg_df['Nbr Passing Reading'] / schAvg_df['reading_count'])


#calc overall passing rate

schAvg_df['Overall Passing Rate']= (schAvg_df['%Passing Reading'] + schAvg_df['%Passing Math']) / 2




```


```python
#cleab up the data figures
schAvg_df = schAvg_df.round(2)
schAvg_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>math_avg</th>
      <th>math_count</th>
      <th>reading_avg</th>
      <th>reading_count</th>
      <th>Nbr Passing Math</th>
      <th>Nbr Passing Reading</th>
      <th>%Passing Math</th>
      <th>%Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
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
      <th>Bailey High School</th>
      <td>77.05</td>
      <td>4976</td>
      <td>81.03</td>
      <td>4976</td>
      <td>3877</td>
      <td>4705</td>
      <td>0.78</td>
      <td>0.95</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.06</td>
      <td>1858</td>
      <td>83.98</td>
      <td>1858</td>
      <td>1858</td>
      <td>1858</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.71</td>
      <td>2949</td>
      <td>81.16</td>
      <td>2949</td>
      <td>2276</td>
      <td>2788</td>
      <td>0.77</td>
      <td>0.95</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.10</td>
      <td>2739</td>
      <td>80.75</td>
      <td>2739</td>
      <td>2142</td>
      <td>2571</td>
      <td>0.78</td>
      <td>0.94</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.35</td>
      <td>1468</td>
      <td>83.82</td>
      <td>1468</td>
      <td>1468</td>
      <td>1468</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.29</td>
      <td>4635</td>
      <td>80.93</td>
      <td>4635</td>
      <td>3603</td>
      <td>4385</td>
      <td>0.78</td>
      <td>0.95</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.80</td>
      <td>427</td>
      <td>83.81</td>
      <td>427</td>
      <td>427</td>
      <td>427</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>76.63</td>
      <td>2917</td>
      <td>81.18</td>
      <td>2917</td>
      <td>2267</td>
      <td>2756</td>
      <td>0.78</td>
      <td>0.94</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>77.07</td>
      <td>4761</td>
      <td>80.97</td>
      <td>4761</td>
      <td>3712</td>
      <td>4498</td>
      <td>0.78</td>
      <td>0.94</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.84</td>
      <td>962</td>
      <td>84.04</td>
      <td>962</td>
      <td>962</td>
      <td>962</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.84</td>
      <td>3999</td>
      <td>80.74</td>
      <td>3999</td>
      <td>3117</td>
      <td>3784</td>
      <td>0.78</td>
      <td>0.95</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.36</td>
      <td>1761</td>
      <td>83.73</td>
      <td>1761</td>
      <td>1761</td>
      <td>1761</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.42</td>
      <td>1635</td>
      <td>83.85</td>
      <td>1635</td>
      <td>1635</td>
      <td>1635</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.27</td>
      <td>2283</td>
      <td>83.99</td>
      <td>2283</td>
      <td>2283</td>
      <td>2283</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.68</td>
      <td>1800</td>
      <td>83.96</td>
      <td>1800</td>
      <td>1800</td>
      <td>1800</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
  </tbody>
</table>
</div>




```python
#to merge the data frames I need to make the schAvg index a column to equal the same column in schSum

schAvg_df['school'] = schAvg_df.index
schAvg_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>math_avg</th>
      <th>math_count</th>
      <th>reading_avg</th>
      <th>reading_count</th>
      <th>Nbr Passing Math</th>
      <th>Nbr Passing Reading</th>
      <th>%Passing Math</th>
      <th>%Passing Reading</th>
      <th>Overall Passing Rate</th>
      <th>school</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
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
      <th>Bailey High School</th>
      <td>77.05</td>
      <td>4976</td>
      <td>81.03</td>
      <td>4976</td>
      <td>3877</td>
      <td>4705</td>
      <td>0.78</td>
      <td>0.95</td>
      <td>0.86</td>
      <td>Bailey High School</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.06</td>
      <td>1858</td>
      <td>83.98</td>
      <td>1858</td>
      <td>1858</td>
      <td>1858</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>Cabrera High School</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.71</td>
      <td>2949</td>
      <td>81.16</td>
      <td>2949</td>
      <td>2276</td>
      <td>2788</td>
      <td>0.77</td>
      <td>0.95</td>
      <td>0.86</td>
      <td>Figueroa High School</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.10</td>
      <td>2739</td>
      <td>80.75</td>
      <td>2739</td>
      <td>2142</td>
      <td>2571</td>
      <td>0.78</td>
      <td>0.94</td>
      <td>0.86</td>
      <td>Ford High School</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.35</td>
      <td>1468</td>
      <td>83.82</td>
      <td>1468</td>
      <td>1468</td>
      <td>1468</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>Griffin High School</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Merge the dataframes into a new df
merged_df = pd.merge(schSum_df, schAvg_df)
```


```python
#Sort the merged df and print it out
school_sumStat_df = merged_df.sort_values('school')
school_sumStat_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>perStu_budget</th>
      <th>math_avg</th>
      <th>math_count</th>
      <th>reading_avg</th>
      <th>reading_count</th>
      <th>Nbr Passing Math</th>
      <th>Nbr Passing Reading</th>
      <th>%Passing Math</th>
      <th>%Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7</th>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>77.05</td>
      <td>4976</td>
      <td>81.03</td>
      <td>4976</td>
      <td>3877</td>
      <td>4705</td>
      <td>0.78</td>
      <td>0.95</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.06</td>
      <td>1858</td>
      <td>83.98</td>
      <td>1858</td>
      <td>1858</td>
      <td>1858</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.71</td>
      <td>2949</td>
      <td>81.16</td>
      <td>2949</td>
      <td>2276</td>
      <td>2788</td>
      <td>0.77</td>
      <td>0.95</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.10</td>
      <td>2739</td>
      <td>80.75</td>
      <td>2739</td>
      <td>2142</td>
      <td>2571</td>
      <td>0.78</td>
      <td>0.94</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.35</td>
      <td>1468</td>
      <td>83.82</td>
      <td>1468</td>
      <td>1468</td>
      <td>1468</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>77.29</td>
      <td>4635</td>
      <td>80.93</td>
      <td>4635</td>
      <td>3603</td>
      <td>4385</td>
      <td>0.78</td>
      <td>0.95</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.80</td>
      <td>427</td>
      <td>83.81</td>
      <td>427</td>
      <td>427</td>
      <td>427</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>76.63</td>
      <td>2917</td>
      <td>81.18</td>
      <td>2917</td>
      <td>2267</td>
      <td>2756</td>
      <td>0.78</td>
      <td>0.94</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.07</td>
      <td>4761</td>
      <td>80.97</td>
      <td>4761</td>
      <td>3712</td>
      <td>4498</td>
      <td>0.78</td>
      <td>0.94</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>83.84</td>
      <td>962</td>
      <td>84.04</td>
      <td>962</td>
      <td>962</td>
      <td>962</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.84</td>
      <td>3999</td>
      <td>80.74</td>
      <td>3999</td>
      <td>3117</td>
      <td>3784</td>
      <td>0.78</td>
      <td>0.95</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.36</td>
      <td>1761</td>
      <td>83.73</td>
      <td>1761</td>
      <td>1761</td>
      <td>1761</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.42</td>
      <td>1635</td>
      <td>83.85</td>
      <td>1635</td>
      <td>1635</td>
      <td>1635</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.27</td>
      <td>2283</td>
      <td>83.99</td>
      <td>2283</td>
      <td>2283</td>
      <td>2283</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>83.68</td>
      <td>1800</td>
      <td>83.96</td>
      <td>1800</td>
      <td>1800</td>
      <td>1800</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
  </tbody>
</table>
</div>



**Top Performing Schools (By Passing Rate)**

* Create a table that highlights the top 5 performing schools based on Overall Passing Rate. Include:
  * School Name
  * School Type
  * Total Students
  * Total School Budget
  * Per Student Budget
  * Average Math Score
  * Average Reading Score
  * % Passing Math
  * % Passing Reading
  * Overall Passing Rate (Average of the above two)




```python
#Sort the merged df and print it out
school_sumStat_df = merged_df.sort_values('Overall Passing Rate', ascending=False)
school_sumStat_df.head(5)

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>perStu_budget</th>
      <th>math_avg</th>
      <th>math_count</th>
      <th>reading_avg</th>
      <th>reading_count</th>
      <th>Nbr Passing Math</th>
      <th>Nbr Passing Reading</th>
      <th>%Passing Math</th>
      <th>%Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.36</td>
      <td>1761</td>
      <td>83.73</td>
      <td>1761</td>
      <td>1761</td>
      <td>1761</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.35</td>
      <td>1468</td>
      <td>83.82</td>
      <td>1468</td>
      <td>1468</td>
      <td>1468</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.27</td>
      <td>2283</td>
      <td>83.99</td>
      <td>2283</td>
      <td>2283</td>
      <td>2283</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.06</td>
      <td>1858</td>
      <td>83.98</td>
      <td>1858</td>
      <td>1858</td>
      <td>1858</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.80</td>
      <td>427</td>
      <td>83.81</td>
      <td>427</td>
      <td>427</td>
      <td>427</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>



**Top Performing Schools (By Passing Rate)**

* Create a table that highlights the bottom 5 performing schools based on Overall Passing Rate. Include all of the same metrics as above.


```python
school_sumStat_df.tail(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>perStu_budget</th>
      <th>math_avg</th>
      <th>math_count</th>
      <th>reading_avg</th>
      <th>reading_count</th>
      <th>Nbr Passing Math</th>
      <th>Nbr Passing Reading</th>
      <th>%Passing Math</th>
      <th>%Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>77.29</td>
      <td>4635</td>
      <td>80.93</td>
      <td>4635</td>
      <td>3603</td>
      <td>4385</td>
      <td>0.78</td>
      <td>0.95</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>77.05</td>
      <td>4976</td>
      <td>81.03</td>
      <td>4976</td>
      <td>3877</td>
      <td>4705</td>
      <td>0.78</td>
      <td>0.95</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.84</td>
      <td>3999</td>
      <td>80.74</td>
      <td>3999</td>
      <td>3117</td>
      <td>3784</td>
      <td>0.78</td>
      <td>0.95</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.07</td>
      <td>4761</td>
      <td>80.97</td>
      <td>4761</td>
      <td>3712</td>
      <td>4498</td>
      <td>0.78</td>
      <td>0.94</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.10</td>
      <td>2739</td>
      <td>80.75</td>
      <td>2739</td>
      <td>2142</td>
      <td>2571</td>
      <td>0.78</td>
      <td>0.94</td>
      <td>0.86</td>
    </tr>
  </tbody>
</table>
</div>



**Math Scores by Grade**

* Create a table that lists the average Math Score for students of each grade level (9th, 10th, 11th, 12th) at each school.




```python
# Math scores average by grade level - group_by
scoreGradeAvg_df = pd.DataFrame()

mathScoreAvgGroup = stu_df.groupby(['grade'])

scoreGradeAvg_df['math_score'] = mathScoreAvgGroup['math_score'].mean()

```


```python
scoreGradeAvg_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>math_score</th>
    </tr>
    <tr>
      <th>grade</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10th</th>
      <td>78.941483</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>79.083548</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>78.993164</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>78.935659</td>
    </tr>
  </tbody>
</table>
</div>



**Reading Scores by Grade**

* Create a table that lists the average Reading Score for students of each grade level (9th, 10th, 11th, 12th) at each school.




```python
# Reading scores average by grade level - group_by

readingScoreAvgGroup = stu_df.groupby(['grade'])

scoreGradeAvg_df['reading_score'] = readingScoreAvgGroup['reading_score'].mean()


```


```python
scoreGradeAvg_df['reading_score']
```




    grade
    10th    81.874410
    11th    81.885714
    12th    81.819851
    9th     81.914358
    Name: reading_score, dtype: float64



**Scores by School Spending**

* Create a table that breaks down school performances based on average Spending Ranges (Per Student). Use 4 reasonable bins to group school spending. Include in the table each of the following:
  * Average Math Score
  * Average Reading Score
  * % Passing Math
  * % Passing Reading
  * Overall Passing Rate (Average of the above two)


```python
# school performance based on average spending ranges per student school_sumStat_df
schoolSpend_df = sch_df
# Create the bins in which Data will be held
bins = [0, 1000000, 2000000, 3000000, 4000000]

# Create the names for the four bins
group_names = ['First', 'Second', 'Third', 'Fourth']

# Cut school_df and place the budgets amts into bins
pd.cut(school_sumStat_df["budget"], bins, labels=group_names)

school_sumStat_df["School % Spend"] = pd.cut(school_sumStat_df["budget"], bins, labels=group_names)
#school_sumStat_df.columns

sch_groups = school_sumStat_df.groupby("School % Spend")
av_df = sch_groups.mean()
#print(av_df['math_avg'], av_df['reading_avg'], av_df['%Passing Math'], av_df['%Passing Reading'], av_df['Overall Passing Rate'])
print_df = pd.DataFrame()
print_df['Math Avg']=av_df['math_avg']
print_df['Read Avg']=av_df['reading_avg']
print_df['% Passing Math']=av_df['%Passing Math']
print_df['% Passing Reading']=av_df['%Passing Reading']
print_df['Overall Passing']=av_df['Overall Passing Rate']

print("\n Breakdown - schools based approximation of school spending \n(first 0-100K, second 100K-200K, third 200K-300K, fourth 300K-400K)\n")
print_df

```

    
     Breakdown - schools based approximation of school spending 
    (first 0-100K, second 100K-200K, third 200K-300K, fourth 300K-400K)
    





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Math Avg</th>
      <th>Read Avg</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing</th>
    </tr>
    <tr>
      <th>School % Spend</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>First</th>
      <td>83.663333</td>
      <td>83.890000</td>
      <td>1.00000</td>
      <td>1.000000</td>
      <td>1.0000</td>
    </tr>
    <tr>
      <th>Second</th>
      <td>80.903750</td>
      <td>82.825000</td>
      <td>0.91625</td>
      <td>0.978750</td>
      <td>0.9475</td>
    </tr>
    <tr>
      <th>Third</th>
      <td>76.840000</td>
      <td>80.740000</td>
      <td>0.78000</td>
      <td>0.950000</td>
      <td>0.8600</td>
    </tr>
    <tr>
      <th>Fourth</th>
      <td>77.136667</td>
      <td>80.976667</td>
      <td>0.78000</td>
      <td>0.946667</td>
      <td>0.8600</td>
    </tr>
  </tbody>
</table>
</div>



*Scores by School Size**

* Repeat the above breakdown, but this time group schools based on a reasonable approximation of school size (Small, Medium, Large).




```python
# school performance based on average spending ranges per student school_sumStat_df
schoolSize_df = sch_df
# Create the bins in which Data will be held
bins_size = [0, 500, 2000, 5000]

# Create the names for the four bins
size_names = ['small', 'medium', 'large']

# Cut school_df and place the budgets amts into bins
pd.cut(school_sumStat_df["budget"], bins_size, labels=size_names)

school_sumStat_df["School % size"] = pd.cut(school_sumStat_df["size"], bins_size, labels=size_names)
#school_sumStat_df.max()

sch_size = school_sumStat_df.groupby("School % size")
avSize_df = sch_size.mean()
#print(avSize_df['math_avg'], avSize_df['reading_avg'], avSize_df['%Passing Math'], avSize_df['%Passing Reading'], avSize_df['Overall Passing Rate'])

print2_df = pd.DataFrame()

print("\n Breakdown - schools based approximation of school size \n(Small 0-500, Medium 500-2000, Large >2000\n")
print2_df['Math Avg']=avSize_df['math_avg']
print2_df['Read Avg']=avSize_df['reading_avg']
print2_df['% Passing Math']=avSize_df['%Passing Math']
print2_df['% Passing Reading']=avSize_df['%Passing Reading']
print2_df['Overall Passing']=avSize_df['Overall Passing Rate']
print2_df

```

    
     Breakdown - schools based approximation of school size 
    (Small 0-500, Medium 500-2000, Large >2000
    





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Math Avg</th>
      <th>Read Avg</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing</th>
    </tr>
    <tr>
      <th>School % size</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>small</th>
      <td>83.800000</td>
      <td>83.810000</td>
      <td>1.00000</td>
      <td>1.0000</td>
      <td>1.0000</td>
    </tr>
    <tr>
      <th>medium</th>
      <td>83.451667</td>
      <td>83.896667</td>
      <td>1.00000</td>
      <td>1.0000</td>
      <td>1.0000</td>
    </tr>
    <tr>
      <th>large</th>
      <td>77.745000</td>
      <td>81.343750</td>
      <td>0.80625</td>
      <td>0.9525</td>
      <td>0.8775</td>
    </tr>
  </tbody>
</table>
</div>



**Scores by School Type**

* Repeat the above breakdown, but this time group schools based on school type (Charter vs. District).




```python
# school performance based on average spending ranges per student school_sumStat_df
schoolType_df = sch_df
# Create the bins in which Data will be held
#bins_size = [0, 500, 2000, 5000]

# Create the names for the four bins
#size_names = ['small', 'medium', 'large']

# Cut school_df and place the budgets amts into bins
#pd.cut(school_sumStat_df["budget"], bins_size, labels=size_names)

#school_sumStat_df["School % size"] = pd.cut(school_sumStat_df["size"], bins_size, labels=size_names)
#school_sumStat_df.max()

sch_type = school_sumStat_df.groupby("type")
avType_df = sch_type.mean()
#print(avSize_df['math_avg'], avSize_df['reading_avg'], avSize_df['%Passing Math'], avSize_df['%Passing Reading'], avSize_df['Overall Passing Rate'])

print3_df = pd.DataFrame()

print("\n Breakdown - schools based on type of school Charter or District \n")
print3_df['Math Avg']=avType_df['math_avg']
print3_df['Read Avg']=avType_df['reading_avg']
print3_df['% Passing Math']=avType_df['%Passing Math']
print3_df['% Passing Reading']=avType_df['%Passing Reading']
print3_df['Overall Passing']=avType_df['Overall Passing Rate']
print3_df


```

    
     Breakdown - schools based on type of school Charter or District 
    





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Math Avg</th>
      <th>Read Avg</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.472500</td>
      <td>83.897500</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>District</th>
      <td>76.955714</td>
      <td>80.965714</td>
      <td>0.778571</td>
      <td>0.945714</td>
      <td>0.86</td>
    </tr>
  </tbody>
</table>
</div>


