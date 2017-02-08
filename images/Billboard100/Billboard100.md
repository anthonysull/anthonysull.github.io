
## Import Modules


```python
# import modules

import pandas as pd
import numpy as np
import scipy.stats as stats
import seaborn as sns
import matplotlib.pyplot as plt
%matplotlib inline
```

## Read in csv


```python
# Load the csv and save to a DataFrame
bb = pd.read_csv('assets/billboard.csv')

# View the first 5 rows
bb.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>x1st.week</th>
      <th>x2nd.week</th>
      <th>x3rd.week</th>
      <th>...</th>
      <th>x67th.week</th>
      <th>x68th.week</th>
      <th>x69th.week</th>
      <th>x70th.week</th>
      <th>x71st.week</th>
      <th>x72nd.week</th>
      <th>x73rd.week</th>
      <th>x74th.week</th>
      <th>x75th.week</th>
      <th>x76th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000</td>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>3,38,00 AM</td>
      <td>Rock</td>
      <td>September 23, 2000</td>
      <td>November 18, 2000</td>
      <td>78</td>
      <td>63</td>
      <td>49</td>
      <td>...</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000</td>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>4,18,00 AM</td>
      <td>Rock</td>
      <td>February 12, 2000</td>
      <td>April 8, 2000</td>
      <td>15</td>
      <td>8</td>
      <td>6</td>
      <td>...</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000</td>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>4,07,00 AM</td>
      <td>Rock</td>
      <td>October 23, 1999</td>
      <td>January 29, 2000</td>
      <td>71</td>
      <td>48</td>
      <td>43</td>
      <td>...</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000</td>
      <td>Madonna</td>
      <td>Music</td>
      <td>3,45,00 AM</td>
      <td>Rock</td>
      <td>August 12, 2000</td>
      <td>September 16, 2000</td>
      <td>41</td>
      <td>23</td>
      <td>18</td>
      <td>...</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000</td>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>3,38,00 AM</td>
      <td>Rock</td>
      <td>August 5, 2000</td>
      <td>October 14, 2000</td>
      <td>57</td>
      <td>47</td>
      <td>45</td>
      <td>...</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
      <td>*</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 83 columns</p>
</div>



## Cleaning Data

### Replace null values


```python
# Define a function 'null' to replace '*' with Nan / missing values
def null(value):
    if value == '*':
        return np.nan
    else:
        return value
    
#Apply null to data using applymap
bb = bb.applymap(null)
bb.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>x1st.week</th>
      <th>x2nd.week</th>
      <th>x3rd.week</th>
      <th>...</th>
      <th>x67th.week</th>
      <th>x68th.week</th>
      <th>x69th.week</th>
      <th>x70th.week</th>
      <th>x71st.week</th>
      <th>x72nd.week</th>
      <th>x73rd.week</th>
      <th>x74th.week</th>
      <th>x75th.week</th>
      <th>x76th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000</td>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>3,38,00 AM</td>
      <td>Rock</td>
      <td>September 23, 2000</td>
      <td>November 18, 2000</td>
      <td>78</td>
      <td>63</td>
      <td>49</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000</td>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>4,18,00 AM</td>
      <td>Rock</td>
      <td>February 12, 2000</td>
      <td>April 8, 2000</td>
      <td>15</td>
      <td>8</td>
      <td>6</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000</td>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>4,07,00 AM</td>
      <td>Rock</td>
      <td>October 23, 1999</td>
      <td>January 29, 2000</td>
      <td>71</td>
      <td>48</td>
      <td>43</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000</td>
      <td>Madonna</td>
      <td>Music</td>
      <td>3,45,00 AM</td>
      <td>Rock</td>
      <td>August 12, 2000</td>
      <td>September 16, 2000</td>
      <td>41</td>
      <td>23</td>
      <td>18</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000</td>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>3,38,00 AM</td>
      <td>Rock</td>
      <td>August 5, 2000</td>
      <td>October 14, 2000</td>
      <td>57</td>
      <td>47</td>
      <td>45</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 83 columns</p>
</div>




```python
bb.describe()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>x1st.week</th>
      <th>x66th.week</th>
      <th>x67th.week</th>
      <th>x68th.week</th>
      <th>x69th.week</th>
      <th>x70th.week</th>
      <th>x71st.week</th>
      <th>x72nd.week</th>
      <th>x73rd.week</th>
      <th>x74th.week</th>
      <th>x75th.week</th>
      <th>x76th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>317.0</td>
      <td>317.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>2000.0</td>
      <td>79.958991</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.0</td>
      <td>14.686865</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>min</th>
      <td>2000.0</td>
      <td>15.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>2000.0</td>
      <td>74.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>2000.0</td>
      <td>81.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2000.0</td>
      <td>91.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2000.0</td>
      <td>100.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Drop empty columns and eliminate
bb.dropna(how='all', axis=1, inplace=True)
bb.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>x1st.week</th>
      <th>x2nd.week</th>
      <th>x3rd.week</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000</td>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>3,38,00 AM</td>
      <td>Rock</td>
      <td>September 23, 2000</td>
      <td>November 18, 2000</td>
      <td>78</td>
      <td>63</td>
      <td>49</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000</td>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>4,18,00 AM</td>
      <td>Rock</td>
      <td>February 12, 2000</td>
      <td>April 8, 2000</td>
      <td>15</td>
      <td>8</td>
      <td>6</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000</td>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>4,07,00 AM</td>
      <td>Rock</td>
      <td>October 23, 1999</td>
      <td>January 29, 2000</td>
      <td>71</td>
      <td>48</td>
      <td>43</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000</td>
      <td>Madonna</td>
      <td>Music</td>
      <td>3,45,00 AM</td>
      <td>Rock</td>
      <td>August 12, 2000</td>
      <td>September 16, 2000</td>
      <td>41</td>
      <td>23</td>
      <td>18</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000</td>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>3,38,00 AM</td>
      <td>Rock</td>
      <td>August 5, 2000</td>
      <td>October 14, 2000</td>
      <td>57</td>
      <td>47</td>
      <td>45</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 72 columns</p>
</div>



### Cleaning Artists


```python
# Check each column using describe, unique, for repeating or mislabelled
bb['artist.inverted'].describe()
```




    count       317
    unique      228
    top       Jay-Z
    freq          5
    Name: artist.inverted, dtype: object




```python
# Check artist names
artists = bb['artist.inverted'].unique()
artists.sort()
print artists
# Artist names look fine - no repeats - and need no cleaning.
```

    ['2 Pac' '2Ge+her' '3 Doors Down' '504 Boyz' '98\xa1' 'A*Teens' 'Aaliyah'
     'Adams, Yolanda' 'Adkins, Trace' 'Aguilera, Christina' 'Alice Deejay'
     'Allan, Gary' 'Amber' 'Anastacia' 'Anthony, Marc' 'Avant' 'BBMak'
     'Backstreet Boys, The' 'Badu, Erkyah' 'Baha Men' 'Barenaked Ladies'
     'Beenie Man' 'Before Dark' 'Bega, Lou' 'Big Punisher' 'Black Rob'
     'Black, Clint' 'Blaque' 'Blige, Mary J.' 'Blink-182' 'Bloodhound Gang'
     'Bon Jovi' 'Braxton, Toni' 'Brock, Chad' 'Brooks & Dunn' 'Brooks, Garth'
     'Byrd, Tracy' 'Cagle, Chris' "Cam'ron" 'Carey, Mariah' 'Carter, Aaron'
     'Carter, Torrey' 'Changing Faces' 'Chesney, Kenny'
     'Clark Family Experience' 'Clark, Terri' 'Common' 'Counting Crows' 'Creed'
     'Cyrus, Billy Ray' "D'Angelo" 'DMX' 'Da Brat' 'Davidson, Clay'
     'De La Soul' "Destiny's Child" 'Diffie, Joe' 'Dion, Celine'
     'Dixie Chicks, The' 'Dr. Dre' 'Drama' 'Dream' 'Eastsidaz, The' 'Eiffel 65'
     'Elliott, Missy "Misdemeanor"' 'Eminem' 'En Vogue' 'Estefan, Gloria'
     'Evans, Sara' 'Eve' 'Everclear' 'Fabian, Lara' 'Fatboy Slim' 'Filter'
     'Foo Fighters' 'Fragma' 'Funkmaster Flex' 'Ghostface Killah' 'Gill, Vince'
     'Gilman, Billy' 'Ginuwine' 'Goo Goo Dolls' 'Gray, Macy' 'Griggs, Andy'
     'Guy' 'Hanson' 'Hart, Beth' 'Heatherly, Eric' 'Henley, Don' 'Herndon, Ty'
     'Hill, Faith' 'Hoku' 'Hollister, Dave' 'Hot Boys' 'Houston, Whitney' 'IMx'
     'Ice Cube' 'Ideal' 'Iglesias, Enrique' 'J-Shin' 'Ja Rule' 'Jackson, Alan'
     'Jagged Edge' 'Janet' 'Jay-Z' 'Jean, Wyclef' 'Joe' 'John, Elton'
     'Jones, Donell' 'Jordan, Montell' 'Juvenile' 'Kandi' 'Keith, Toby' 'Kelis'
     'Kenny G' 'Kid Rock' 'Kravitz, Lenny' 'Kumbia Kings' 'LFO' 'LL Cool J'
     'Larrieux, Amel' 'Lawrence, Tracy' 'Levert, Gerald' 'Lil Bow Wow'
     'Lil Wayne' "Lil' Kim" "Lil' Mo" "Lil' Zane" 'Limp Bizkit' 'Lonestar'
     'Lopez, Jennifer' 'Loveless, Patty' 'Lox' 'Lucy Pearl' 'Ludacris' 'M2M'
     'Madison Avenue' 'Madonna' 'Martin, Ricky' 'Mary Mary' 'Master P'
     'McBride, Martina' 'McEntire, Reba' 'McGraw, Tim' 'McKnight, Brian'
     'Messina, Jo Dee' 'Metallica' 'Montgomery Gentry'
     'Montgomery, John Michael' 'Moore, Chante' 'Moore, Mandy'
     'Mumba, Samantha' 'Musiq' 'Mya' 'Mystikal' "N'Sync" 'Nas' 'Nelly' 'Next'
     'Nine Days' 'No Doubt' 'Nu Flavor' 'Offspring, The' 'Paisley, Brad'
     'Papa Roach' 'Pearl Jam' 'Pink' 'Price, Kelly' 'Profyle' 'Puff Daddy'
     'Q-Tip' 'R.E.M.' 'Rascal Flatts' 'Raye, Collin' 'Red Hot Chili Peppers'
     'Rimes, LeAnn' 'Rogers, Kenny' 'Ruff Endz' 'Sammie' 'Santana'
     'Savage Garden' 'SheDaisy' 'Sheist, Shade' 'Shyne' 'Simpson, Jessica'
     'Sisqo' 'Sister Hazel' 'Smash Mouth' 'Smith, Will' 'Son By Four' 'Sonique'
     'SoulDecision' 'Spears, Britney' 'Spencer, Tracie' 'Splender' 'Sting'
     'Stone Temple Pilots' 'Stone, Angie' 'Strait, George' 'Sugar Ray' 'TLC'
     'Tamar' 'Tamia' 'Third Eye Blind' 'Thomas, Carl' 'Tippin, Aaron' 'Train'
     'Trick Daddy' 'Trina' 'Tritt, Travis' 'Tuesday' 'Urban, Keith' 'Usher'
     'Vassar, Phil' 'Vertical Horizon' 'Vitamin C' 'Walker, Clay'
     'Wallflowers, The' 'Westlife' 'Williams, Robbie' 'Wills, Mark'
     'Worley, Darryl' 'Wright, Chely' 'Yankee Grey' 'Yearwood, Trisha'
     'Ying Yang Twins' 'Zombie Nation' 'matchbox twenty']


### Cleaning Tracks


```python
# Check 'track' column
bb['track'].describe()
```




    count                  317
    unique                 316
    top       Where I Wanna Be
    freq                     2
    Name: track, dtype: object




```python
# One track name repeats, so lets check the info for those instances
doubletrack = bb[bb['track'].str.contains("Where I Wanna Be")]
doubletrack
# It appears tqo artists each had a song with the same name, no cleaning required
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>x1st.week</th>
      <th>x2nd.week</th>
      <th>x3rd.week</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>118</th>
      <td>2000</td>
      <td>Jones, Donell</td>
      <td>Where I Wanna Be</td>
      <td>6,22,00 AM</td>
      <td>Rock</td>
      <td>April 22, 2000</td>
      <td>July 8, 2000</td>
      <td>81</td>
      <td>71</td>
      <td>65</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>305</th>
      <td>2000</td>
      <td>Sheist, Shade</td>
      <td>Where I Wanna Be</td>
      <td>4,16,00 AM</td>
      <td>Rap</td>
      <td>November 11, 2000</td>
      <td>November 18, 2000</td>
      <td>96</td>
      <td>95</td>
      <td>99</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>2 rows × 72 columns</p>
</div>



### Cleaning Genres


```python
# Check 'genre' column
bb.genre.describe().to_frame()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>genre</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>317</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>12</td>
    </tr>
    <tr>
      <th>top</th>
      <td>Rock</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>103</td>
    </tr>
  </tbody>
</table>
</div>




```python
bb.genre.unique()
```




    array(['Rock', "Rock'n'roll", 'Latin', 'Country', 'Rap', 'Pop',
           'Electronica', 'Jazz', 'R&B', 'Reggae', 'Gospel', 'R & B'], dtype=object)




```python
# R&B is repeated in two slightly different variations, need to relabel R & B to R&B
bb['genre'] = bb['genre'].str.replace('R & B', 'R&B')
bb['genre'].unique()
```




    array(['Rock', "Rock'n'roll", 'Latin', 'Country', 'Rap', 'Pop',
           'Electronica', 'Jazz', 'R&B', 'Reggae', 'Gospel'], dtype=object)




```python
# Check Rock'n'roll category
bb[bb['genre'] == "Rock'n'roll"].head()
# Artists in the rock'n'roll category seem to range from r&b to pop to Heavy metal
# Relabeling this data would take an inordinate amount of time for this project.
# I've chosen to assume the data given is correct for our purposes here.

# We could choose to relabel Rock'n'roll into either rock or R&B based on genre descriptions. 
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>x1st.week</th>
      <th>x2nd.week</th>
      <th>x3rd.week</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>2000</td>
      <td>Destiny's Child</td>
      <td>Say My Name</td>
      <td>4,31,00 AM</td>
      <td>Rock'n'roll</td>
      <td>December 25, 1999</td>
      <td>March 18, 2000</td>
      <td>83</td>
      <td>83</td>
      <td>44</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2000</td>
      <td>Sisqo</td>
      <td>Incomplete</td>
      <td>3,52,00 AM</td>
      <td>Rock'n'roll</td>
      <td>June 24, 2000</td>
      <td>August 12, 2000</td>
      <td>77</td>
      <td>66</td>
      <td>61</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2000</td>
      <td>N'Sync</td>
      <td>It's Gonna Be Me</td>
      <td>3,10,00 AM</td>
      <td>Rock'n'roll</td>
      <td>May 6, 2000</td>
      <td>July 29, 2000</td>
      <td>82</td>
      <td>70</td>
      <td>51</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2000</td>
      <td>Aguilera, Christina</td>
      <td>What A Girl Wants</td>
      <td>3,18,00 AM</td>
      <td>Rock'n'roll</td>
      <td>November 27, 1999</td>
      <td>January 15, 2000</td>
      <td>71</td>
      <td>51</td>
      <td>28</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2000</td>
      <td>Vertical Horizon</td>
      <td>Everything You Want</td>
      <td>4,01,00 AM</td>
      <td>Rock'n'roll</td>
      <td>January 22, 2000</td>
      <td>July 15, 2000</td>
      <td>70</td>
      <td>61</td>
      <td>53</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 72 columns</p>
</div>




```python
#Check rock category
bb[bb['genre'] == "Rock"].head()
# Artists in the rock category also seem to range from Rock, pop, R&B, Hip-Hop
# Again chosing to trust the data here under the scope of the project.
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>x1st.week</th>
      <th>x2nd.week</th>
      <th>x3rd.week</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000</td>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>3,38,00 AM</td>
      <td>Rock</td>
      <td>September 23, 2000</td>
      <td>November 18, 2000</td>
      <td>78</td>
      <td>63</td>
      <td>49</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000</td>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>4,18,00 AM</td>
      <td>Rock</td>
      <td>February 12, 2000</td>
      <td>April 8, 2000</td>
      <td>15</td>
      <td>8</td>
      <td>6</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000</td>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>4,07,00 AM</td>
      <td>Rock</td>
      <td>October 23, 1999</td>
      <td>January 29, 2000</td>
      <td>71</td>
      <td>48</td>
      <td>43</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000</td>
      <td>Madonna</td>
      <td>Music</td>
      <td>3,45,00 AM</td>
      <td>Rock</td>
      <td>August 12, 2000</td>
      <td>September 16, 2000</td>
      <td>41</td>
      <td>23</td>
      <td>18</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000</td>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>3,38,00 AM</td>
      <td>Rock</td>
      <td>August 5, 2000</td>
      <td>October 14, 2000</td>
      <td>57</td>
      <td>47</td>
      <td>45</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 72 columns</p>
</div>




```python
bb[bb['genre'] == "R&B"].head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>x1st.week</th>
      <th>x2nd.week</th>
      <th>x3rd.week</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>66</th>
      <td>2000</td>
      <td>Profyle</td>
      <td>Liar</td>
      <td>3,57,00 AM</td>
      <td>R&amp;B</td>
      <td>September 16, 2000</td>
      <td>October 28, 2000</td>
      <td>52</td>
      <td>32</td>
      <td>25</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>75</th>
      <td>2000</td>
      <td>Guy</td>
      <td>Dancin'</td>
      <td>4,08,00 AM</td>
      <td>R&amp;B</td>
      <td>December 18, 1999</td>
      <td>January 1, 2000</td>
      <td>46</td>
      <td>29</td>
      <td>19</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>100</th>
      <td>2000</td>
      <td>D'Angelo</td>
      <td>Untitled (How Does It Feel)</td>
      <td>7,10,00 AM</td>
      <td>R&amp;B</td>
      <td>January 22, 2000</td>
      <td>February 19, 2000</td>
      <td>77</td>
      <td>56</td>
      <td>35</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>133</th>
      <td>2000</td>
      <td>J-Shin</td>
      <td>One Night Stand</td>
      <td>4,34,00 AM</td>
      <td>R&amp;B</td>
      <td>December 25, 1999</td>
      <td>February 26, 2000</td>
      <td>96</td>
      <td>96</td>
      <td>69</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>137</th>
      <td>2000</td>
      <td>Carter, Aaron</td>
      <td>Aaron's Party (Come Get It)</td>
      <td>3,23,00 AM</td>
      <td>R&amp;B</td>
      <td>August 26, 2000</td>
      <td>September 16, 2000</td>
      <td>99</td>
      <td>75</td>
      <td>57</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 72 columns</p>
</div>




```python
bb[bb['genre'] == "Pop"]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>x1st.week</th>
      <th>x2nd.week</th>
      <th>x3rd.week</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>2000</td>
      <td>Blaque</td>
      <td>Bring It All To Me</td>
      <td>3,46,00 AM</td>
      <td>Pop</td>
      <td>October 23, 1999</td>
      <td>January 22, 2000</td>
      <td>73</td>
      <td>63</td>
      <td>50</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>81</th>
      <td>2000</td>
      <td>Simpson, Jessica</td>
      <td>I Think I'm In Love With You</td>
      <td>3,32,00 AM</td>
      <td>Pop</td>
      <td>July 1, 2000</td>
      <td>August 12, 2000</td>
      <td>63</td>
      <td>52</td>
      <td>44</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>84</th>
      <td>2000</td>
      <td>M2M</td>
      <td>Don't Say You Love Me</td>
      <td>3,41,00 AM</td>
      <td>Pop</td>
      <td>November 20, 1999</td>
      <td>January 8, 2000</td>
      <td>72</td>
      <td>53</td>
      <td>62</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>98</th>
      <td>2000</td>
      <td>Moore, Mandy</td>
      <td>I Wanna Be With You</td>
      <td>4,12,00 AM</td>
      <td>Pop</td>
      <td>June 17, 2000</td>
      <td>August 12, 2000</td>
      <td>69</td>
      <td>63</td>
      <td>54</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>110</th>
      <td>2000</td>
      <td>Hoku</td>
      <td>Another Dumb Blonde</td>
      <td>3,47,00 AM</td>
      <td>Pop</td>
      <td>February 19, 2000</td>
      <td>April 8, 2000</td>
      <td>69</td>
      <td>49</td>
      <td>49</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>129</th>
      <td>2000</td>
      <td>Fabian, Lara</td>
      <td>I Will Love Again</td>
      <td>3,43,00 AM</td>
      <td>Pop</td>
      <td>June 10, 2000</td>
      <td>August 12, 2000</td>
      <td>91</td>
      <td>80</td>
      <td>75</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>217</th>
      <td>2000</td>
      <td>M2M</td>
      <td>Mirror Mirror</td>
      <td>3,19,00 AM</td>
      <td>Pop</td>
      <td>April 1, 2000</td>
      <td>May 27, 2000</td>
      <td>87</td>
      <td>87</td>
      <td>94</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>301</th>
      <td>2000</td>
      <td>Anastacia</td>
      <td>I'm Outta Love</td>
      <td>4,01,00 AM</td>
      <td>Pop</td>
      <td>April 1, 2000</td>
      <td>April 1, 2000</td>
      <td>92</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>304</th>
      <td>2000</td>
      <td>A*Teens</td>
      <td>Dancing Queen</td>
      <td>3,44,00 AM</td>
      <td>Pop</td>
      <td>July 8, 2000</td>
      <td>July 29, 2000</td>
      <td>97</td>
      <td>97</td>
      <td>96</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>9 rows × 72 columns</p>
</div>




```python
bb[bb['genre'] == "Rap"].head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>x1st.week</th>
      <th>x2nd.week</th>
      <th>x3rd.week</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17</th>
      <td>2000</td>
      <td>Hill, Faith</td>
      <td>Breathe</td>
      <td>4,04,00 AM</td>
      <td>Rap</td>
      <td>November 6, 1999</td>
      <td>April 22, 2000</td>
      <td>81</td>
      <td>68</td>
      <td>62</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2000</td>
      <td>Jordan, Montell</td>
      <td>Get It On.. Tonite</td>
      <td>4,34,00 AM</td>
      <td>Rap</td>
      <td>October 23, 1999</td>
      <td>February 12, 2000</td>
      <td>92</td>
      <td>80</td>
      <td>72</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>31</th>
      <td>2000</td>
      <td>Eminem</td>
      <td>The Real Slim Shady</td>
      <td>4,42,00 AM</td>
      <td>Rap</td>
      <td>May 6, 2000</td>
      <td>June 24, 2000</td>
      <td>70</td>
      <td>32</td>
      <td>20</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>35</th>
      <td>2000</td>
      <td>Elliott, Missy "Misdemeanor"</td>
      <td>Hot Boyz</td>
      <td>3,51,00 AM</td>
      <td>Rap</td>
      <td>November 27, 1999</td>
      <td>January 8, 2000</td>
      <td>36</td>
      <td>21</td>
      <td>13</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>47</th>
      <td>2000</td>
      <td>Nelly</td>
      <td>(Hot S**t) Country Grammar</td>
      <td>4,17,00 AM</td>
      <td>Rap</td>
      <td>April 29, 2000</td>
      <td>September 16, 2000</td>
      <td>100</td>
      <td>99</td>
      <td>96</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 72 columns</p>
</div>




```python
# The genre column is bunk. A large number of songs are mislabelled.

# Ehhh, after some intial frustration, I will treat the genres as correctly labelled for this project.
# Billboard is the client...
```

### Cleaning Time - track length


```python
# Remove ' AM' from time string
bb['time'] = bb['time'].map(lambda x: x.rstrip(' AM'))
bb['time'].head()
```




    0    3,38,00
    1    4,18,00
    2    4,07,00
    3    3,45,00
    4    3,38,00
    Name: time, dtype: object




```python
# Function to split time and convert to seconds
def to_seconds(s):
    split = [(x.split(',')) for x in s]
    seconds = [(int(i[0])*60)+(int(i[1]))*(1+int(i[2])*.1) for i in split]
    return seconds
    
bb['time'] = to_seconds(bb['time'])
```


```python
bb.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>x1st.week</th>
      <th>x2nd.week</th>
      <th>x3rd.week</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000</td>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>September 23, 2000</td>
      <td>November 18, 2000</td>
      <td>78</td>
      <td>63</td>
      <td>49</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000</td>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>258.0</td>
      <td>Rock</td>
      <td>February 12, 2000</td>
      <td>April 8, 2000</td>
      <td>15</td>
      <td>8</td>
      <td>6</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000</td>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>247.0</td>
      <td>Rock</td>
      <td>October 23, 1999</td>
      <td>January 29, 2000</td>
      <td>71</td>
      <td>48</td>
      <td>43</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000</td>
      <td>Madonna</td>
      <td>Music</td>
      <td>225.0</td>
      <td>Rock</td>
      <td>August 12, 2000</td>
      <td>September 16, 2000</td>
      <td>41</td>
      <td>23</td>
      <td>18</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000</td>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>August 5, 2000</td>
      <td>October 14, 2000</td>
      <td>57</td>
      <td>47</td>
      <td>45</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 72 columns</p>
</div>




```python
bb.shape
bb.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>x1st.week</th>
      <th>x2nd.week</th>
      <th>x3rd.week</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000</td>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>September 23, 2000</td>
      <td>November 18, 2000</td>
      <td>78</td>
      <td>63</td>
      <td>49</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000</td>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>258.0</td>
      <td>Rock</td>
      <td>February 12, 2000</td>
      <td>April 8, 2000</td>
      <td>15</td>
      <td>8</td>
      <td>6</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000</td>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>247.0</td>
      <td>Rock</td>
      <td>October 23, 1999</td>
      <td>January 29, 2000</td>
      <td>71</td>
      <td>48</td>
      <td>43</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000</td>
      <td>Madonna</td>
      <td>Music</td>
      <td>225.0</td>
      <td>Rock</td>
      <td>August 12, 2000</td>
      <td>September 16, 2000</td>
      <td>41</td>
      <td>23</td>
      <td>18</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000</td>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>August 5, 2000</td>
      <td>October 14, 2000</td>
      <td>57</td>
      <td>47</td>
      <td>45</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 72 columns</p>
</div>




```python

```


```python

```

### Clean dates - date.entered and date.peaked


```python
# Import datetime to convert string dates to datetime
import datetime
```


```python
# Convert date.peaked and date.entered to date time
bb['date.entered'] = pd.to_datetime(bb['date.entered'],infer_datetime_format=True)
bb['date.peaked'] = pd.to_datetime(bb['date.peaked'],infer_datetime_format=True)
# bb['date.entered'].dtypes
# bb.head()
```


```python
# Create a value for the number of days it took a song to peak
daystopeak = abs(bb['date.entered']-bb['date.peaked'])
```


```python
# Data type of daystopeak
daystopeak.dtypes
```




    dtype('<m8[ns]')




```python
# Convert DaysToPeak to integer
daystopeak = daystopeak.astype('timedelta64[D]').astype(int)
print daystopeak.dtypes
daystopeak.head()
```

    int64





    0    56
    1    56
    2    98
    3    35
    4    70
    dtype: int64




```python
# Convert days to weeks
weekstopeak = daystopeak/7
weekstopeak = weekstopeak.astype(int)
weekstopeak.head()
```




    0     8
    1     8
    2    14
    3     5
    4    10
    dtype: int64




```python
# Insert WeeksToPeak column into dataframe
bb.insert(5, 'weeksToPeak', weekstopeak, allow_duplicates=False)
bb.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>weeksToPeak</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>x1st.week</th>
      <th>x2nd.week</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000</td>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>8</td>
      <td>2000-09-23</td>
      <td>2000-11-18</td>
      <td>78</td>
      <td>63</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000</td>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>258.0</td>
      <td>Rock</td>
      <td>8</td>
      <td>2000-02-12</td>
      <td>2000-04-08</td>
      <td>15</td>
      <td>8</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000</td>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>247.0</td>
      <td>Rock</td>
      <td>14</td>
      <td>1999-10-23</td>
      <td>2000-01-29</td>
      <td>71</td>
      <td>48</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000</td>
      <td>Madonna</td>
      <td>Music</td>
      <td>225.0</td>
      <td>Rock</td>
      <td>5</td>
      <td>2000-08-12</td>
      <td>2000-09-16</td>
      <td>41</td>
      <td>23</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000</td>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>10</td>
      <td>2000-08-05</td>
      <td>2000-10-14</td>
      <td>57</td>
      <td>47</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 73 columns</p>
</div>




```python
# Convert x_weeks columns to numeric
bb.iloc[:,8:] = bb.iloc[:,8:].apply(pd.to_numeric, errors='coerce')
bb.iloc[:,9].dtypes
```




    dtype('float64')




```python
# Compute the number of Weeks a track was in the Chart and assign to a new column
weeksInChart = bb.iloc[:,8:].count(axis=1)
# Add weeksInChart column to dataframe
bb.insert(5, 'weeksInChart', weeksInChart, allow_duplicates=False)
bb.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>x1st.week</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000</td>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>28</td>
      <td>8</td>
      <td>2000-09-23</td>
      <td>2000-11-18</td>
      <td>78</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000</td>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>258.0</td>
      <td>Rock</td>
      <td>26</td>
      <td>8</td>
      <td>2000-02-12</td>
      <td>2000-04-08</td>
      <td>15</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000</td>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>247.0</td>
      <td>Rock</td>
      <td>33</td>
      <td>14</td>
      <td>1999-10-23</td>
      <td>2000-01-29</td>
      <td>71</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000</td>
      <td>Madonna</td>
      <td>Music</td>
      <td>225.0</td>
      <td>Rock</td>
      <td>24</td>
      <td>5</td>
      <td>2000-08-12</td>
      <td>2000-09-16</td>
      <td>41</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000</td>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>21</td>
      <td>10</td>
      <td>2000-08-05</td>
      <td>2000-10-14</td>
      <td>57</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 74 columns</p>
</div>




```python
# Add TopRank column
MaxPosition = bb.iloc[:,9:].min(axis=1)
bb.insert(5, 'TopRank', MaxPosition, allow_duplicates=False)
```


```python
# TopRank to int
bb['TopRank'] = bb['TopRank'].astype(int)
bb.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>TopRank</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000</td>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>1</td>
      <td>28</td>
      <td>8</td>
      <td>2000-09-23</td>
      <td>2000-11-18</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000</td>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>258.0</td>
      <td>Rock</td>
      <td>1</td>
      <td>26</td>
      <td>8</td>
      <td>2000-02-12</td>
      <td>2000-04-08</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000</td>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>247.0</td>
      <td>Rock</td>
      <td>1</td>
      <td>33</td>
      <td>14</td>
      <td>1999-10-23</td>
      <td>2000-01-29</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000</td>
      <td>Madonna</td>
      <td>Music</td>
      <td>225.0</td>
      <td>Rock</td>
      <td>1</td>
      <td>24</td>
      <td>5</td>
      <td>2000-08-12</td>
      <td>2000-09-16</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000</td>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>1</td>
      <td>21</td>
      <td>10</td>
      <td>2000-08-05</td>
      <td>2000-10-14</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 75 columns</p>
</div>




```python
bb.tail()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>TopRank</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>312</th>
      <td>2000</td>
      <td>Ghostface Killah</td>
      <td>Cherchez LaGhost</td>
      <td>184.0</td>
      <td>R&amp;B</td>
      <td>98</td>
      <td>1</td>
      <td>0</td>
      <td>2000-08-05</td>
      <td>2000-08-05</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>313</th>
      <td>2000</td>
      <td>Smith, Will</td>
      <td>Freakin' It</td>
      <td>238.0</td>
      <td>Rap</td>
      <td>99</td>
      <td>4</td>
      <td>0</td>
      <td>2000-02-12</td>
      <td>2000-02-12</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>314</th>
      <td>2000</td>
      <td>Zombie Nation</td>
      <td>Kernkraft 400</td>
      <td>210.0</td>
      <td>Rock</td>
      <td>99</td>
      <td>2</td>
      <td>0</td>
      <td>2000-09-02</td>
      <td>2000-09-02</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>315</th>
      <td>2000</td>
      <td>Eastsidaz, The</td>
      <td>Got Beef</td>
      <td>238.0</td>
      <td>Rap</td>
      <td>99</td>
      <td>2</td>
      <td>0</td>
      <td>2000-07-01</td>
      <td>2000-07-01</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>316</th>
      <td>2000</td>
      <td>Fragma</td>
      <td>Toca's Miracle</td>
      <td>202.0</td>
      <td>R&amp;B</td>
      <td>99</td>
      <td>1</td>
      <td>0</td>
      <td>2000-10-28</td>
      <td>2000-10-28</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 75 columns</p>
</div>



### Calculate a song score based on weekly position


```python
# First Break out weeks columns and invert ranking
songScoreWk = bb.iloc[:,10:].apply(lambda x: 101 - x, axis=1)
songScoreWk.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x1st.week</th>
      <th>x2nd.week</th>
      <th>x3rd.week</th>
      <th>x4th.week</th>
      <th>x5th.week</th>
      <th>x6th.week</th>
      <th>x7th.week</th>
      <th>x8th.week</th>
      <th>x9th.week</th>
      <th>x10th.week</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>23.0</td>
      <td>38.0</td>
      <td>52.0</td>
      <td>68.0</td>
      <td>78.0</td>
      <td>86.0</td>
      <td>94.0</td>
      <td>96.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>86.0</td>
      <td>93.0</td>
      <td>95.0</td>
      <td>96.0</td>
      <td>99.0</td>
      <td>98.0</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>30.0</td>
      <td>53.0</td>
      <td>58.0</td>
      <td>70.0</td>
      <td>81.0</td>
      <td>88.0</td>
      <td>94.0</td>
      <td>95.0</td>
      <td>97.0</td>
      <td>97.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>60.0</td>
      <td>78.0</td>
      <td>83.0</td>
      <td>87.0</td>
      <td>99.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>99.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>44.0</td>
      <td>54.0</td>
      <td>56.0</td>
      <td>72.0</td>
      <td>78.0</td>
      <td>83.0</td>
      <td>90.0</td>
      <td>92.0</td>
      <td>92.0</td>
      <td>90.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 65 columns</p>
</div>




```python
# Compute song score
songScore = songScoreWk.sum(axis=1)
songScore.describe()
```




    count     317.000000
    mean      836.189274
    std       815.023892
    min         2.000000
    25%       185.000000
    50%       601.000000
    75%      1170.000000
    max      4133.000000
    dtype: float64




```python
# Convert song score to an integer
songScore = songScore.astype(int)
```


```python
bb.insert(5, 'SongScore', songScore, allow_duplicates=False)
bb.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>SongScore</th>
      <th>TopRank</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>date.entered</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000</td>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>2413</td>
      <td>1</td>
      <td>28</td>
      <td>8</td>
      <td>2000-09-23</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000</td>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>258.0</td>
      <td>Rock</td>
      <td>2353</td>
      <td>1</td>
      <td>26</td>
      <td>8</td>
      <td>2000-02-12</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000</td>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>247.0</td>
      <td>Rock</td>
      <td>2760</td>
      <td>1</td>
      <td>33</td>
      <td>14</td>
      <td>1999-10-23</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000</td>
      <td>Madonna</td>
      <td>Music</td>
      <td>225.0</td>
      <td>Rock</td>
      <td>2101</td>
      <td>1</td>
      <td>24</td>
      <td>5</td>
      <td>2000-08-12</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000</td>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>1702</td>
      <td>1</td>
      <td>21</td>
      <td>10</td>
      <td>2000-08-05</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 76 columns</p>
</div>




```python
# Add positions climbed column
climbed = bb['x1st.week'] - bb['TopRank']
bb.insert(9, 'Climb', climbed, allow_duplicates=False)
bb.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>SongScore</th>
      <th>TopRank</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>Climb</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000</td>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>2413</td>
      <td>1</td>
      <td>28</td>
      <td>8</td>
      <td>77</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000</td>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>258.0</td>
      <td>Rock</td>
      <td>2353</td>
      <td>1</td>
      <td>26</td>
      <td>8</td>
      <td>14</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000</td>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>247.0</td>
      <td>Rock</td>
      <td>2760</td>
      <td>1</td>
      <td>33</td>
      <td>14</td>
      <td>70</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000</td>
      <td>Madonna</td>
      <td>Music</td>
      <td>225.0</td>
      <td>Rock</td>
      <td>2101</td>
      <td>1</td>
      <td>24</td>
      <td>5</td>
      <td>40</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000</td>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>1702</td>
      <td>1</td>
      <td>21</td>
      <td>10</td>
      <td>56</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 77 columns</p>
</div>




```python
# Add column for first week position move
firstWeekMovement = bb['x1st.week'] - bb['x2nd.week']
bb.insert(7, 'firstWeekMove', firstWeekMovement, allow_duplicates=False)
bb.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>SongScore</th>
      <th>TopRank</th>
      <th>firstWeekMove</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000</td>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>2413</td>
      <td>1</td>
      <td>15.0</td>
      <td>28</td>
      <td>8</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000</td>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>258.0</td>
      <td>Rock</td>
      <td>2353</td>
      <td>1</td>
      <td>7.0</td>
      <td>26</td>
      <td>8</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000</td>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>247.0</td>
      <td>Rock</td>
      <td>2760</td>
      <td>1</td>
      <td>23.0</td>
      <td>33</td>
      <td>14</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000</td>
      <td>Madonna</td>
      <td>Music</td>
      <td>225.0</td>
      <td>Rock</td>
      <td>2101</td>
      <td>1</td>
      <td>18.0</td>
      <td>24</td>
      <td>5</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000</td>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>1702</td>
      <td>1</td>
      <td>10.0</td>
      <td>21</td>
      <td>10</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 78 columns</p>
</div>




```python
bb.tail(10)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>SongScore</th>
      <th>TopRank</th>
      <th>firstWeekMove</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>307</th>
      <td>2000</td>
      <td>Larrieux, Amel</td>
      <td>Get Up</td>
      <td>242.0</td>
      <td>R&amp;B</td>
      <td>9</td>
      <td>97</td>
      <td>3.0</td>
      <td>3</td>
      <td>1</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>308</th>
      <td>2000</td>
      <td>Braxton, Toni</td>
      <td>Spanish Guitar</td>
      <td>264.0</td>
      <td>Rock</td>
      <td>9</td>
      <td>98</td>
      <td>0.0</td>
      <td>3</td>
      <td>0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>309</th>
      <td>2000</td>
      <td>Tuesday</td>
      <td>I Know</td>
      <td>246.0</td>
      <td>Rock</td>
      <td>6</td>
      <td>98</td>
      <td>0.0</td>
      <td>2</td>
      <td>0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>310</th>
      <td>2000</td>
      <td>LL Cool J</td>
      <td>Imagine That</td>
      <td>240.0</td>
      <td>Rap</td>
      <td>5</td>
      <td>98</td>
      <td>1.0</td>
      <td>2</td>
      <td>1</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>311</th>
      <td>2000</td>
      <td>Master P</td>
      <td>Souljas</td>
      <td>213.0</td>
      <td>Rap</td>
      <td>3</td>
      <td>98</td>
      <td>NaN</td>
      <td>1</td>
      <td>0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>312</th>
      <td>2000</td>
      <td>Ghostface Killah</td>
      <td>Cherchez LaGhost</td>
      <td>184.0</td>
      <td>R&amp;B</td>
      <td>3</td>
      <td>98</td>
      <td>NaN</td>
      <td>1</td>
      <td>0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>313</th>
      <td>2000</td>
      <td>Smith, Will</td>
      <td>Freakin' It</td>
      <td>238.0</td>
      <td>Rap</td>
      <td>8</td>
      <td>99</td>
      <td>0.0</td>
      <td>4</td>
      <td>0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>314</th>
      <td>2000</td>
      <td>Zombie Nation</td>
      <td>Kernkraft 400</td>
      <td>210.0</td>
      <td>Rock</td>
      <td>4</td>
      <td>99</td>
      <td>0.0</td>
      <td>2</td>
      <td>0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>315</th>
      <td>2000</td>
      <td>Eastsidaz, The</td>
      <td>Got Beef</td>
      <td>238.0</td>
      <td>Rap</td>
      <td>4</td>
      <td>99</td>
      <td>0.0</td>
      <td>2</td>
      <td>0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>316</th>
      <td>2000</td>
      <td>Fragma</td>
      <td>Toca's Miracle</td>
      <td>202.0</td>
      <td>R&amp;B</td>
      <td>2</td>
      <td>99</td>
      <td>NaN</td>
      <td>1</td>
      <td>0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 78 columns</p>
</div>




```python
# Lets drop the year column as it is all the same
bb = bb.iloc[:,1:]
bb.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>SongScore</th>
      <th>TopRank</th>
      <th>firstWeekMove</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>Climb</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>2413</td>
      <td>1</td>
      <td>15.0</td>
      <td>28</td>
      <td>8</td>
      <td>77</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>258.0</td>
      <td>Rock</td>
      <td>2353</td>
      <td>1</td>
      <td>7.0</td>
      <td>26</td>
      <td>8</td>
      <td>14</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>247.0</td>
      <td>Rock</td>
      <td>2760</td>
      <td>1</td>
      <td>23.0</td>
      <td>33</td>
      <td>14</td>
      <td>70</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Madonna</td>
      <td>Music</td>
      <td>225.0</td>
      <td>Rock</td>
      <td>2101</td>
      <td>1</td>
      <td>18.0</td>
      <td>24</td>
      <td>5</td>
      <td>40</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>1702</td>
      <td>1</td>
      <td>10.0</td>
      <td>21</td>
      <td>10</td>
      <td>56</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 77 columns</p>
</div>




```python
# Lets take a quick first look at our data and the columns that we created
bb.iloc[:,:13].describe()
# Taking a look at songScore and weeksInChart we can already see our top performing songs are outliers.
# They performed well out of range for the typical song.

# The average amount of weeks for a track to chart was 17.
# It took approximately 7 weeks for a song to peak.
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>time</th>
      <th>SongScore</th>
      <th>TopRank</th>
      <th>firstWeekMove</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>Climb</th>
      <th>x1st.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>317.000000</td>
      <td>317.000000</td>
      <td>317.000000</td>
      <td>312.000000</td>
      <td>317.000000</td>
      <td>317.000000</td>
      <td>317.000000</td>
      <td>317.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>242.425868</td>
      <td>836.189274</td>
      <td>44.123028</td>
      <td>8.580128</td>
      <td>16.741325</td>
      <td>7.463722</td>
      <td>35.835962</td>
      <td>79.958991</td>
    </tr>
    <tr>
      <th>std</th>
      <td>42.401618</td>
      <td>815.023892</td>
      <td>29.223722</td>
      <td>8.437780</td>
      <td>9.083785</td>
      <td>5.838229</td>
      <td>25.061031</td>
      <td>14.686865</td>
    </tr>
    <tr>
      <th>min</th>
      <td>156.000000</td>
      <td>2.000000</td>
      <td>1.000000</td>
      <td>-21.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>15.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>219.000000</td>
      <td>185.000000</td>
      <td>20.000000</td>
      <td>NaN</td>
      <td>10.000000</td>
      <td>3.000000</td>
      <td>14.000000</td>
      <td>74.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>236.000000</td>
      <td>601.000000</td>
      <td>42.000000</td>
      <td>NaN</td>
      <td>18.000000</td>
      <td>7.000000</td>
      <td>33.000000</td>
      <td>81.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>257.000000</td>
      <td>1170.000000</td>
      <td>70.000000</td>
      <td>NaN</td>
      <td>20.000000</td>
      <td>10.000000</td>
      <td>56.000000</td>
      <td>91.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>470.000000</td>
      <td>4133.000000</td>
      <td>99.000000</td>
      <td>38.000000</td>
      <td>57.000000</td>
      <td>45.000000</td>
      <td>97.000000</td>
      <td>100.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Take a look at the top performing song.

bb.iloc[(bb['SongScore'].idxmax()),:12]

# Notice the song first entered the charts in November 1999.
# It was the most popular song for the year despite never reaching the top spot.
```




    artist.inverted            Hill, Faith
    track                          Breathe
    time                               244
    genre                              Rap
    SongScore                         4133
    TopRank                              2
    firstWeekMove                       13
    weeksInChart                        53
    weeksToPeak                         24
    Climb                               79
    date.entered       1999-11-06 00:00:00
    date.peaked        2000-04-22 00:00:00
    Name: 17, dtype: object




```python
# Lets try and deal with the genres again. Assuming they are labelled correctly. Before we viz
# Get counts of each genre
bb_genre = bb.genre.value_counts().to_frame()
# Get the percentages of each genre
bb_genre['percent'] = bb_genre['genre']/sum(bb_genre['genre'])
bb_genre
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>genre</th>
      <th>percent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rock</th>
      <td>103</td>
      <td>0.324921</td>
    </tr>
    <tr>
      <th>Country</th>
      <td>74</td>
      <td>0.233438</td>
    </tr>
    <tr>
      <th>Rap</th>
      <td>58</td>
      <td>0.182965</td>
    </tr>
    <tr>
      <th>Rock'n'roll</th>
      <td>34</td>
      <td>0.107256</td>
    </tr>
    <tr>
      <th>R&amp;B</th>
      <td>23</td>
      <td>0.072555</td>
    </tr>
    <tr>
      <th>Pop</th>
      <td>9</td>
      <td>0.028391</td>
    </tr>
    <tr>
      <th>Latin</th>
      <td>9</td>
      <td>0.028391</td>
    </tr>
    <tr>
      <th>Electronica</th>
      <td>4</td>
      <td>0.012618</td>
    </tr>
    <tr>
      <th>Gospel</th>
      <td>1</td>
      <td>0.003155</td>
    </tr>
    <tr>
      <th>Jazz</th>
      <td>1</td>
      <td>0.003155</td>
    </tr>
    <tr>
      <th>Reggae</th>
      <td>1</td>
      <td>0.003155</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Since Billboard groups genres by audience and there is crossover between audiences 
# we can think of binning certain genres together
# Let's take a look at the genres with less than 1%
bb[bb['genre'] == 'Gospel']
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>SongScore</th>
      <th>TopRank</th>
      <th>firstWeekMove</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>Climb</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>200</th>
      <td>Adams, Yolanda</td>
      <td>Open My Heart</td>
      <td>330.0</td>
      <td>Gospel</td>
      <td>665</td>
      <td>57</td>
      <td>0.0</td>
      <td>20</td>
      <td>8</td>
      <td>19</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>1 rows × 77 columns</p>
</div>




```python
# Bin Gospel to R&B as Open My Heart charted highest in the R&B chart - see charts for track
bb['genre'].replace('Gospel', 'R&B', inplace=True)
bb['genre'].value_counts()
```




    Rock           103
    Country         74
    Rap             58
    Rock'n'roll     34
    R&B             24
    Pop              9
    Latin            9
    Electronica      4
    Jazz             1
    Reggae           1
    Name: genre, dtype: int64




```python
# Jazz genre
bb[bb['genre'] == 'Jazz']
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>SongScore</th>
      <th>TopRank</th>
      <th>firstWeekMove</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>Climb</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>49</th>
      <td>Kenny G</td>
      <td>Auld Lang Syne (The Millenium Mix)</td>
      <td>470.0</td>
      <td>Jazz</td>
      <td>246</td>
      <td>7</td>
      <td>0.0</td>
      <td>5</td>
      <td>2</td>
      <td>82</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>1 rows × 77 columns</p>
</div>




```python
# grouping Jazz to Pop as Kenny G charted in the adult and mainstream charts
bb['genre'].replace('Jazz', 'Pop', inplace=True)
bb['genre'].value_counts()
```




    Rock           103
    Country         74
    Rap             58
    Rock'n'roll     34
    R&B             24
    Pop             10
    Latin            9
    Electronica      4
    Reggae           1
    Name: genre, dtype: int64




```python
# Reggae genre
bb[bb['genre'] == 'Reggae']
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>SongScore</th>
      <th>TopRank</th>
      <th>firstWeekMove</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>Climb</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>189</th>
      <td>Beenie Man</td>
      <td>Girls Dem Sugar</td>
      <td>257.0</td>
      <td>Reggae</td>
      <td>429</td>
      <td>54</td>
      <td>0.0</td>
      <td>15</td>
      <td>6</td>
      <td>18</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>1 rows × 77 columns</p>
</div>




```python
# grouping Reggae to R&B as Beenie Man charted in the R&B charts
bb['genre'].replace('Reggae', 'R&B', inplace=True)
bb['genre'].value_counts()
```




    Rock           103
    Country         74
    Rap             58
    Rock'n'roll     34
    R&B             25
    Pop             10
    Latin            9
    Electronica      4
    Name: genre, dtype: int64




```python
# Also I will bin rock'n'roll and r&b as they are related categories and 
# rock'n'roll is not a recognized contemporary genre.
# bb['genre'].replace("Rock'n'roll", 'R&B', inplace=True)
# bb['genre'].value_counts()
```


```python
# Apply dummy variables to genre
# bb['genre'].value_counts()
```


```python
bb.iloc[:,:13].head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>SongScore</th>
      <th>TopRank</th>
      <th>firstWeekMove</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>Climb</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>x1st.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>2413</td>
      <td>1</td>
      <td>15.0</td>
      <td>28</td>
      <td>8</td>
      <td>77</td>
      <td>2000-09-23</td>
      <td>2000-11-18</td>
      <td>78</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>258.0</td>
      <td>Rock</td>
      <td>2353</td>
      <td>1</td>
      <td>7.0</td>
      <td>26</td>
      <td>8</td>
      <td>14</td>
      <td>2000-02-12</td>
      <td>2000-04-08</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>247.0</td>
      <td>Rock</td>
      <td>2760</td>
      <td>1</td>
      <td>23.0</td>
      <td>33</td>
      <td>14</td>
      <td>70</td>
      <td>1999-10-23</td>
      <td>2000-01-29</td>
      <td>71</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Madonna</td>
      <td>Music</td>
      <td>225.0</td>
      <td>Rock</td>
      <td>2101</td>
      <td>1</td>
      <td>18.0</td>
      <td>24</td>
      <td>5</td>
      <td>40</td>
      <td>2000-08-12</td>
      <td>2000-09-16</td>
      <td>41</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>1702</td>
      <td>1</td>
      <td>10.0</td>
      <td>21</td>
      <td>10</td>
      <td>56</td>
      <td>2000-08-05</td>
      <td>2000-10-14</td>
      <td>57</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create debut ranking column
debut = bb['x1st.week']
bb.insert(12, 'debut', debut, allow_duplicates=False)
```


```python
weeks  = bb.iloc[:,13:]
weeks.columns = [range(1,66)]
weeks.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>...</th>
      <th>56</th>
      <th>57</th>
      <th>58</th>
      <th>59</th>
      <th>60</th>
      <th>61</th>
      <th>62</th>
      <th>63</th>
      <th>64</th>
      <th>65</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>78</td>
      <td>63.0</td>
      <td>49.0</td>
      <td>33.0</td>
      <td>23.0</td>
      <td>15.0</td>
      <td>7.0</td>
      <td>5.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15</td>
      <td>8.0</td>
      <td>6.0</td>
      <td>5.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>71</td>
      <td>48.0</td>
      <td>43.0</td>
      <td>31.0</td>
      <td>20.0</td>
      <td>13.0</td>
      <td>7.0</td>
      <td>6.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41</td>
      <td>23.0</td>
      <td>18.0</td>
      <td>14.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>57</td>
      <td>47.0</td>
      <td>45.0</td>
      <td>29.0</td>
      <td>23.0</td>
      <td>18.0</td>
      <td>11.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>11.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 65 columns</p>
</div>




```python
exit = []
for i in range(317):
    column = bb.loc[i,'weeksInChart']
    exit.append(weeks.loc[i,column])
exit.head()
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-2114-2c9cb58f5da0> in <module>()
          3     column = bb.loc[i,'weeksInChart']
          4     exit.append(weeks.loc[i,column])
    ----> 5 exit.head()
    

    AttributeError: 'list' object has no attribute 'head'



```python
bb.insert(13, 'exit', exit, allow_duplicates=False)
bb.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>SongScore</th>
      <th>TopRank</th>
      <th>firstWeekMove</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>Climb</th>
      <th>...</th>
      <th>x56th.week</th>
      <th>x57th.week</th>
      <th>x58th.week</th>
      <th>x59th.week</th>
      <th>x60th.week</th>
      <th>x61st.week</th>
      <th>x62nd.week</th>
      <th>x63rd.week</th>
      <th>x64th.week</th>
      <th>x65th.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>2413</td>
      <td>1</td>
      <td>15.0</td>
      <td>28</td>
      <td>8</td>
      <td>77</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>258.0</td>
      <td>Rock</td>
      <td>2353</td>
      <td>1</td>
      <td>7.0</td>
      <td>26</td>
      <td>8</td>
      <td>14</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>247.0</td>
      <td>Rock</td>
      <td>2760</td>
      <td>1</td>
      <td>23.0</td>
      <td>33</td>
      <td>14</td>
      <td>70</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Madonna</td>
      <td>Music</td>
      <td>225.0</td>
      <td>Rock</td>
      <td>2101</td>
      <td>1</td>
      <td>18.0</td>
      <td>24</td>
      <td>5</td>
      <td>40</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>1702</td>
      <td>1</td>
      <td>10.0</td>
      <td>21</td>
      <td>10</td>
      <td>56</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 79 columns</p>
</div>




```python

```


```python
# Break out only the columns with data to plot
# We could use the weekly data to plot a chart of track performance\
# over time but we will not use it for testing our hypothesis.
bbd = bb.iloc[:,:14]
```


```python
bbd.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>SongScore</th>
      <th>TopRank</th>
      <th>firstWeekMove</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>Climb</th>
      <th>date.entered</th>
      <th>date.peaked</th>
      <th>debut</th>
      <th>exit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>2413</td>
      <td>1</td>
      <td>15.0</td>
      <td>28</td>
      <td>8</td>
      <td>77</td>
      <td>2000-09-23</td>
      <td>2000-11-18</td>
      <td>78</td>
      <td>31.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>258.0</td>
      <td>Rock</td>
      <td>2353</td>
      <td>1</td>
      <td>7.0</td>
      <td>26</td>
      <td>8</td>
      <td>14</td>
      <td>2000-02-12</td>
      <td>2000-04-08</td>
      <td>15</td>
      <td>47.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>247.0</td>
      <td>Rock</td>
      <td>2760</td>
      <td>1</td>
      <td>23.0</td>
      <td>33</td>
      <td>14</td>
      <td>70</td>
      <td>1999-10-23</td>
      <td>2000-01-29</td>
      <td>71</td>
      <td>47.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Madonna</td>
      <td>Music</td>
      <td>225.0</td>
      <td>Rock</td>
      <td>2101</td>
      <td>1</td>
      <td>18.0</td>
      <td>24</td>
      <td>5</td>
      <td>40</td>
      <td>2000-08-12</td>
      <td>2000-09-16</td>
      <td>41</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>1702</td>
      <td>1</td>
      <td>10.0</td>
      <td>21</td>
      <td>10</td>
      <td>56</td>
      <td>2000-08-05</td>
      <td>2000-10-14</td>
      <td>57</td>
      <td>44.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# create Dummy variables from the genre category
genres = pd.get_dummies(bbd['genre'])

# Join the dummy variables to the main dataframe
bbd = pd.concat([bbd, genres], axis=1)
bbd.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>artist.inverted</th>
      <th>track</th>
      <th>time</th>
      <th>genre</th>
      <th>SongScore</th>
      <th>TopRank</th>
      <th>firstWeekMove</th>
      <th>weeksInChart</th>
      <th>weeksToPeak</th>
      <th>Climb</th>
      <th>...</th>
      <th>debut</th>
      <th>exit</th>
      <th>Country</th>
      <th>Electronica</th>
      <th>Latin</th>
      <th>Pop</th>
      <th>R&amp;B</th>
      <th>Rap</th>
      <th>Rock</th>
      <th>Rock'n'roll</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Destiny's Child</td>
      <td>Independent Women Part I</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>2413</td>
      <td>1</td>
      <td>15.0</td>
      <td>28</td>
      <td>8</td>
      <td>77</td>
      <td>...</td>
      <td>78</td>
      <td>31.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Santana</td>
      <td>Maria, Maria</td>
      <td>258.0</td>
      <td>Rock</td>
      <td>2353</td>
      <td>1</td>
      <td>7.0</td>
      <td>26</td>
      <td>8</td>
      <td>14</td>
      <td>...</td>
      <td>15</td>
      <td>47.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Savage Garden</td>
      <td>I Knew I Loved You</td>
      <td>247.0</td>
      <td>Rock</td>
      <td>2760</td>
      <td>1</td>
      <td>23.0</td>
      <td>33</td>
      <td>14</td>
      <td>70</td>
      <td>...</td>
      <td>71</td>
      <td>47.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Madonna</td>
      <td>Music</td>
      <td>225.0</td>
      <td>Rock</td>
      <td>2101</td>
      <td>1</td>
      <td>18.0</td>
      <td>24</td>
      <td>5</td>
      <td>40</td>
      <td>...</td>
      <td>41</td>
      <td>44.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aguilera, Christina</td>
      <td>Come On Over Baby (All I Want Is You)</td>
      <td>218.0</td>
      <td>Rock</td>
      <td>1702</td>
      <td>1</td>
      <td>10.0</td>
      <td>21</td>
      <td>10</td>
      <td>56</td>
      <td>...</td>
      <td>57</td>
      <td>44.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>




```python
# Lets the check performance of each genre using a pivot table using SongScore.
pd.pivot_table(bbd, index=['Country', 'Electronica', 'Latin', 'Pop', 'R&B','Rap', 'Rock', "Rock'n'roll"],\
               values=['SongScore'], aggfunc= [np.mean, min, max, np.median])
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th>mean</th>
      <th>min</th>
      <th>max</th>
      <th>median</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th>SongScore</th>
      <th>SongScore</th>
      <th>SongScore</th>
      <th>SongScore</th>
    </tr>
    <tr>
      <th>Country</th>
      <th>Electronica</th>
      <th>Latin</th>
      <th>Pop</th>
      <th>R&amp;B</th>
      <th>Rap</th>
      <th>Rock</th>
      <th>Rock'n'roll</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="7" valign="top">0.0</th>
      <th rowspan="6" valign="top">0.0</th>
      <th rowspan="5" valign="top">0.0</th>
      <th rowspan="4" valign="top">0.0</th>
      <th rowspan="3" valign="top">0.0</th>
      <th rowspan="2" valign="top">0.0</th>
      <th>0.0</th>
      <th>1.0</th>
      <td>1636.411765</td>
      <td>40</td>
      <td>3656</td>
      <td>1784.5</td>
    </tr>
    <tr>
      <th>1.0</th>
      <th>0.0</th>
      <td>936.504854</td>
      <td>4</td>
      <td>3950</td>
      <td>678.0</td>
    </tr>
    <tr>
      <th>1.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <td>645.982759</td>
      <td>3</td>
      <td>4133</td>
      <td>365.0</td>
    </tr>
    <tr>
      <th>1.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <td>392.120000</td>
      <td>2</td>
      <td>1075</td>
      <td>398.0</td>
    </tr>
    <tr>
      <th>1.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <td>655.300000</td>
      <td>19</td>
      <td>2303</td>
      <td>557.0</td>
    </tr>
    <tr>
      <th>1.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <td>1025.444444</td>
      <td>124</td>
      <td>2481</td>
      <td>853.0</td>
    </tr>
    <tr>
      <th>1.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <td>686.750000</td>
      <td>167</td>
      <td>1406</td>
      <td>587.0</td>
    </tr>
    <tr>
      <th>1.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <th>0.0</th>
      <td>637.500000</td>
      <td>31</td>
      <td>4085</td>
      <td>643.0</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python

```


```python

```


```python

```


```python
# Lets the check performance of each genre using a pivot table using toprank achieved.
pd.pivot_table(bb, index=['genre'], values=['TopRank'], aggfunc= [np.mean, min, max, np.median], margins=True)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>mean</th>
      <th>min</th>
      <th>max</th>
      <th>median</th>
    </tr>
    <tr>
      <th></th>
      <th>TopRank</th>
      <th>TopRank</th>
      <th>TopRank</th>
      <th>TopRank</th>
    </tr>
    <tr>
      <th>genre</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Country</th>
      <td>49.554054</td>
      <td>1.0</td>
      <td>92.0</td>
      <td>44.5</td>
    </tr>
    <tr>
      <th>Electronica</th>
      <td>49.250000</td>
      <td>6.0</td>
      <td>88.0</td>
      <td>51.5</td>
    </tr>
    <tr>
      <th>Latin</th>
      <td>31.444444</td>
      <td>1.0</td>
      <td>70.0</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>Pop</th>
      <td>38.600000</td>
      <td>5.0</td>
      <td>95.0</td>
      <td>25.5</td>
    </tr>
    <tr>
      <th>R&amp;B</th>
      <td>59.000000</td>
      <td>14.0</td>
      <td>99.0</td>
      <td>57.0</td>
    </tr>
    <tr>
      <th>Rap</th>
      <td>52.362069</td>
      <td>2.0</td>
      <td>99.0</td>
      <td>55.5</td>
    </tr>
    <tr>
      <th>Rock</th>
      <td>40.621359</td>
      <td>1.0</td>
      <td>99.0</td>
      <td>33.0</td>
    </tr>
    <tr>
      <th>Rock'n'roll</th>
      <td>22.294118</td>
      <td>1.0</td>
      <td>84.0</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>All</th>
      <td>44.123028</td>
      <td>1.0</td>
      <td>99.0</td>
      <td>42.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Lets the check performance of each genre using a pivot table using SongScore.
pd.pivot_table(bb, index=['genre'], values=['SongScore'], aggfunc= [np.mean, min, max, np.median], margins=True)

# We can see that Rock'n'roll tracks outperform by quite a bit tracks from other genres.
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>mean</th>
      <th>min</th>
      <th>max</th>
      <th>median</th>
    </tr>
    <tr>
      <th></th>
      <th>SongScore</th>
      <th>SongScore</th>
      <th>SongScore</th>
      <th>SongScore</th>
    </tr>
    <tr>
      <th>genre</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Country</th>
      <td>637.500000</td>
      <td>31.0</td>
      <td>4085.0</td>
      <td>643.0</td>
    </tr>
    <tr>
      <th>Electronica</th>
      <td>686.750000</td>
      <td>167.0</td>
      <td>1406.0</td>
      <td>587.0</td>
    </tr>
    <tr>
      <th>Latin</th>
      <td>1025.444444</td>
      <td>124.0</td>
      <td>2481.0</td>
      <td>853.0</td>
    </tr>
    <tr>
      <th>Pop</th>
      <td>655.300000</td>
      <td>19.0</td>
      <td>2303.0</td>
      <td>557.0</td>
    </tr>
    <tr>
      <th>R&amp;B</th>
      <td>392.120000</td>
      <td>2.0</td>
      <td>1075.0</td>
      <td>398.0</td>
    </tr>
    <tr>
      <th>Rap</th>
      <td>645.982759</td>
      <td>3.0</td>
      <td>4133.0</td>
      <td>365.0</td>
    </tr>
    <tr>
      <th>Rock</th>
      <td>936.504854</td>
      <td>4.0</td>
      <td>3950.0</td>
      <td>678.0</td>
    </tr>
    <tr>
      <th>Rock'n'roll</th>
      <td>1636.411765</td>
      <td>40.0</td>
      <td>3656.0</td>
      <td>1784.5</td>
    </tr>
    <tr>
      <th>All</th>
      <td>836.189274</td>
      <td>2.0</td>
      <td>4133.0</td>
      <td>601.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Check the first week rankings of songs that reached the top spot
bb[['x1st.week']][bb['TopRank'] == 1.0].describe()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x1st.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>17.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>66.647059</td>
    </tr>
    <tr>
      <th>std</th>
      <td>17.895325</td>
    </tr>
    <tr>
      <th>min</th>
      <td>15.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>59.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>71.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>81.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>84.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Check the first week climb of songs that reached the top spot
bbd[['firstWeekMove']][bb['TopRank'] == 1.0].describe()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>firstWeekMove</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>17.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>13.294118</td>
    </tr>
    <tr>
      <th>std</th>
      <td>7.363463</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>7.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>12.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>18.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>27.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Check the first week climb of all songs
bbd[['firstWeekMove']].describe()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>firstWeekMove</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>312.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>8.580128</td>
    </tr>
    <tr>
      <th>std</th>
      <td>8.437780</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-21.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>max</th>
      <td>38.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Check the exit ranks of top songs over weeksInCharts
bbd[['exit','weeksInChart']][bb['TopRank'] == 1.0].describe()
# We would expect high values for most songs exiting the charts
# However, most songs that reach the top 10 drop off the charts after descending below 40 beyond the 20 week mark
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>exit</th>
      <th>weeksInChart</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>17.000000</td>
      <td>17.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>44.705882</td>
      <td>30.411765</td>
    </tr>
    <tr>
      <th>std</th>
      <td>13.792048</td>
      <td>9.937673</td>
    </tr>
    <tr>
      <th>min</th>
      <td>22.000000</td>
      <td>20.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>41.000000</td>
      <td>24.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>44.000000</td>
      <td>26.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>47.000000</td>
      <td>33.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>89.000000</td>
      <td>55.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Check exit rank vs weeksInChart
bbd[['weeksInChart', 'exit']][bbd['exit'] > 50.0]
# Songs exiting the charts below rank 50 did not spend more than 20 weeks in the chart

# We can conclude that songs below the top 50 were dropped after 20 weeks either from quirks\
# in the industry or through Billboards ranking processes.

# Songs that were in the top 40 remained in the charts until they fell out of the top 40.
# Essentially there appears to be a 20 week or top 40 cutoff for songs charting.
# This may represent the abundance of top 40 radio airplay and the use of airplay in Billboards metrics for ranking\
# and also a 20 week rotation for songs not in the top 40.
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>weeksInChart</th>
      <th>exit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>16</th>
      <td>20</td>
      <td>89.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>20</td>
      <td>94.0</td>
    </tr>
    <tr>
      <th>31</th>
      <td>19</td>
      <td>98.0</td>
    </tr>
    <tr>
      <th>43</th>
      <td>20</td>
      <td>88.0</td>
    </tr>
    <tr>
      <th>44</th>
      <td>20</td>
      <td>66.0</td>
    </tr>
    <tr>
      <th>49</th>
      <td>5</td>
      <td>66.0</td>
    </tr>
    <tr>
      <th>51</th>
      <td>20</td>
      <td>96.0</td>
    </tr>
    <tr>
      <th>52</th>
      <td>20</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>54</th>
      <td>20</td>
      <td>53.0</td>
    </tr>
    <tr>
      <th>60</th>
      <td>18</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>61</th>
      <td>20</td>
      <td>58.0</td>
    </tr>
    <tr>
      <th>63</th>
      <td>20</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>66</th>
      <td>20</td>
      <td>99.0</td>
    </tr>
    <tr>
      <th>68</th>
      <td>20</td>
      <td>77.0</td>
    </tr>
    <tr>
      <th>69</th>
      <td>18</td>
      <td>96.0</td>
    </tr>
    <tr>
      <th>72</th>
      <td>20</td>
      <td>78.0</td>
    </tr>
    <tr>
      <th>74</th>
      <td>15</td>
      <td>98.0</td>
    </tr>
    <tr>
      <th>75</th>
      <td>11</td>
      <td>94.0</td>
    </tr>
    <tr>
      <th>77</th>
      <td>20</td>
      <td>56.0</td>
    </tr>
    <tr>
      <th>79</th>
      <td>20</td>
      <td>67.0</td>
    </tr>
    <tr>
      <th>80</th>
      <td>7</td>
      <td>95.0</td>
    </tr>
    <tr>
      <th>81</th>
      <td>16</td>
      <td>96.0</td>
    </tr>
    <tr>
      <th>83</th>
      <td>13</td>
      <td>95.0</td>
    </tr>
    <tr>
      <th>84</th>
      <td>12</td>
      <td>98.0</td>
    </tr>
    <tr>
      <th>86</th>
      <td>20</td>
      <td>59.0</td>
    </tr>
    <tr>
      <th>87</th>
      <td>18</td>
      <td>93.0</td>
    </tr>
    <tr>
      <th>89</th>
      <td>20</td>
      <td>51.0</td>
    </tr>
    <tr>
      <th>90</th>
      <td>20</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>91</th>
      <td>20</td>
      <td>78.0</td>
    </tr>
    <tr>
      <th>92</th>
      <td>20</td>
      <td>58.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>286</th>
      <td>7</td>
      <td>99.0</td>
    </tr>
    <tr>
      <th>287</th>
      <td>3</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>288</th>
      <td>20</td>
      <td>97.0</td>
    </tr>
    <tr>
      <th>289</th>
      <td>5</td>
      <td>95.0</td>
    </tr>
    <tr>
      <th>290</th>
      <td>18</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>291</th>
      <td>3</td>
      <td>98.0</td>
    </tr>
    <tr>
      <th>292</th>
      <td>9</td>
      <td>98.0</td>
    </tr>
    <tr>
      <th>293</th>
      <td>6</td>
      <td>93.0</td>
    </tr>
    <tr>
      <th>294</th>
      <td>5</td>
      <td>96.0</td>
    </tr>
    <tr>
      <th>295</th>
      <td>12</td>
      <td>97.0</td>
    </tr>
    <tr>
      <th>296</th>
      <td>6</td>
      <td>94.0</td>
    </tr>
    <tr>
      <th>297</th>
      <td>7</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>298</th>
      <td>4</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>299</th>
      <td>4</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>300</th>
      <td>8</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>302</th>
      <td>4</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>303</th>
      <td>7</td>
      <td>99.0</td>
    </tr>
    <tr>
      <th>304</th>
      <td>5</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>305</th>
      <td>5</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>306</th>
      <td>3</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>307</th>
      <td>3</td>
      <td>97.0</td>
    </tr>
    <tr>
      <th>308</th>
      <td>3</td>
      <td>98.0</td>
    </tr>
    <tr>
      <th>309</th>
      <td>2</td>
      <td>98.0</td>
    </tr>
    <tr>
      <th>310</th>
      <td>2</td>
      <td>98.0</td>
    </tr>
    <tr>
      <th>311</th>
      <td>1</td>
      <td>98.0</td>
    </tr>
    <tr>
      <th>312</th>
      <td>1</td>
      <td>98.0</td>
    </tr>
    <tr>
      <th>313</th>
      <td>4</td>
      <td>99.0</td>
    </tr>
    <tr>
      <th>314</th>
      <td>2</td>
      <td>99.0</td>
    </tr>
    <tr>
      <th>315</th>
      <td>2</td>
      <td>99.0</td>
    </tr>
    <tr>
      <th>316</th>
      <td>1</td>
      <td>99.0</td>
    </tr>
  </tbody>
</table>
<p>243 rows × 2 columns</p>
</div>



## Data Visualization 


```python
#Set plot style to seaborn dark
sns.set_style('darkgrid')
```


```python
# Get a list of columns
bbd.columns
```




    Index([u'artist.inverted', u'track', u'time', u'genre', u'SongScore',
           u'TopRank', u'firstWeekMove', u'weeksInChart', u'weeksToPeak', u'Climb',
           u'date.entered', u'date.peaked', u'debut', u'exit'],
          dtype='object')




```python
# Create a list of columns to plot
topairplot = ['artist.inverted', 'track', 'time', 'genre', 'SongScore', \
              'TopRank', 'weeksInChart', 'weeksToPeak', 'Climb',\
              'debut']
```


```python
# Pairplot data
sns.pairplot(bbd[topairplot])
plt.show()
```


![png](output_90_0.png)



```python
# Look for some correlations
tocorrelate = ['time', 'genre', 'SongScore', 'TopRank', 'firstWeekMove', 'weeksInChart', 'weeksToPeak', 'Climb',\
              'debut', 'exit']
sns.heatmap(bbd[tocorrelate].corr(), linewidths=0.5)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1340bc890>




![png](output_91_1.png)



```python
# Lets Plot exit ranking vs weeks spent in the charts
ax = bbd.plot(x='exit', y='weeksInChart', kind='scatter', color='dodgerblue',\
        s=40, alpha=.75)
ax.set_title('Weeks in Chart vs Exit Rank', y=1.01)
plt.show()
# We can more clearly see, with one exception, that songs exiting the charts\
# below the top 50 spent no more than 20 weeks in the charts.

# Tracks exiting the charts above the top 50 all spent more than 20 weeks in the charts.
```


![png](output_92_0.png)



```python
# A few songs exit the charts above position 30, lets check why this could be
bbd[['date.entered', 'weeksInChart', 'exit']][bbd['exit'] < 30.0]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date.entered</th>
      <th>weeksInChart</th>
      <th>exit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7</th>
      <td>2000-04-01</td>
      <td>20</td>
      <td>28.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1999-06-05</td>
      <td>55</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>46</th>
      <td>1999-09-11</td>
      <td>57</td>
      <td>29.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Transpose weeks back to normal
weeks = weeks.T
```


```python
#Lets plot the track in a line chart to view the 20 week / top 40 phenomenon

ax = weeks.plot(figsize=(16,8))

# Invert the y axis to plot top rankings at the top
ax.set_ylim(ax.get_ylim()[::-1])

# set the title
ax.set_title('Track Rankings vs Weeks Charting', fontsize=18, y=1.01)

# Remove the legend
ax.legend_.remove()

# x-axis labels
ax.set_ylabel('Rank')

# y-axis labels
ax.set_xlabel('Weeks in Chart')
plt.show()
```


![png](output_95_0.png)


## Lets look at our Null Hypothesis'

### Does the debut ranking have an effect on song performance

The debut ranking of a track has no effect on overall song performance. <br>
$H_0$: The median debut ranking of the top 10% of songs in the Hot 100 was the same as the median debut all songs.


```python
# Plot song performance vs debut ranking in the charts
ax = bbd.plot(x='SongScore', y='debut', kind='scatter', color='dodgerblue',\
        s=40, alpha=.5)
# Invert the y-axis
ax.set_ylim(ax.get_ylim()[::-1])

# set the title
ax.set_title('Song Performance vs Debut Ranking', y=1.01)

# x-axis labels
ax.set_ylabel('Debut Rank')

# y-axis labels
ax.set_xlabel('Track Score')
plt.show()
```


![png](output_99_0.png)



```python
# Find the top 10% of tracks
bbd.SongScore.describe(percentiles=.9)
```




    count     317.000000
    mean      836.189274
    std       815.023892
    min         2.000000
    50%       601.000000
    90%      2001.800000
    max      4133.000000
    Name: SongScore, dtype: float64




```python
topsongs = bbd['SongScore'].map(lambda x: True if x > 2001 else False)
bbd['topsongs'] = topsongs
bbd['topsongs'].describe()
```




    count       317
    unique        2
    top       False
    freq        285
    Name: topsongs, dtype: object




```python
# Lets use the median debut ranking for our central tendency
# Lets get the median debut ranking of the top 10% of tracks
medDebutTop10 = bbd['debut'][bbd['SongScore'] >= 2001.0].median()
medDebutTop10
```




    76.5




```python
# Lets get the median debut ranking of the all tracks
medDebutAll = bbd['debut'].median()
medDebutAll
```




    81.0




```python
# Calculate the difference in medians values
diffDebut = medDebutAll - medDebutTop10
diffDebut
```




    4.5



### Lets find the probability that the top 10% of tracks could have a median debut rank of 4.5 spots higher.

- Lets use the shuffle method since our dataset is small.
- Lets set our alpha: $$\alpha = .05$$


```python
alpha = .05
trials = 100000
counter = 0
a = bbd['debut']
toptracks = bbd['track'][bbd['topsongs'] == True].count()
for i in range(trials):
    b = np.random.permutation(a)
    top = b[:toptracks]
    alltracks = b[:]
    diff = np.median(alltracks) - np.median(top)
    if diff >= 4.5:
        counter += 1.0000
    pval = counter/trials
    
print 'p-value: {}%'.format((counter/trials)*100), pval > alpha 
```

    p-value: 2.876% False


We get a p-value of just under 3%, so in this case we reject our null hypothesis. <br>
The median debut ranking of the top 10% of songs in the Hot 100 was **not** the same as the median debut ranking of all songs.


```python

```


```python

```

### Do Rock'n'roll songs perform better than all genres?

- Problem Statement: Rock'n'roll tracks performed no better than tracks from all genres. <br>
- $H_0$: The median song score of Rock'n'roll tracks was no different than the median song score of all tracks.


```python
# Make a violin plot of genre
ax = sns.violinplot(x="genre", y="SongScore", data=bbd)
ax.set_title('Track Performance by Genre')
ax.set_ylabel('Track Score')
ax.set_xlabel('Genre')
plt.show()
```


![png](output_112_0.png)


The violin plot allows us clearly see that Rock'n'roll tracks have a higher mean score. The mean track scores for the other genres are relatively similar with Latin, Country, and Rock being slightly higher than the others. 


```python
# Median song score of Rock'n'roll tracks
medRnRscore = bbd['SongScore'][bbd['genre'] == "Rock'n'roll"].median()
medRnRscore
```




    1784.5




```python
# Calculate the median score for all songs
medallscore = bbd['SongScore'].median()
medallscore
```




    601.0




```python
# Calculate the differnce of the median scores
diffscore = medRnRscore - medallscore
diffscore
```




    1183.5



### Lets use the shuffle method again to calculate the probability of Rock'n'roll songs having a median song score 1183.5 points better than all songs.


```python
rockroll = bbd['track'][bbd['genre'] == "Rock'n'roll"].count()
rockroll
```




    34




```python
alpha = .05
trials = 100000
counter = 0
a = bbd['SongScore']
rockroll = bbd['track'][bbd['genre'] == "Rock'n'roll"].count()
for i in range(trials):
    b = np.random.permutation(a)
    rr = b[:rockroll]
    alltracks = b[:]
    diff = np.median(alltracks) - np.median(rr)
    if diff >= 1183.5:
        counter += 1.0000
    pval = counter/trials
    
print 'p-value: {}%'.format((counter/trials)*100), counter, pval > alpha
```

    p-value: 0 False


The probability of a Rock'n'roll song achieving a median score 1183.5 points higher than the median score for all songs is 0. We therefore reject our null hypothesis and conclude that the median song score of Rock'n'roll tracks was **not** no different than the median song score of all tracks. <br>
Rock'n'roll songs did perform better in the year 2000! By quite a bit.


