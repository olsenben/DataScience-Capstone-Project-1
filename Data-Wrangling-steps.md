# Steps to cleaning the(MBTI) Myers-Briggs Personality Type Dataset
This dataset includes a large number of people's MBTI type and content written by them.

## Data Set Context
The description for this dataset can be found @ <https://www.kaggle.com/datasnaek/mbti-type>
The Myers Briggs Type Indicator (or MBTI for short) is a personality type system that divides everyone into 16 distinct personality types across 4 axis:

Introversion (I) – Extroversion (E)
Intuition (N) – Sensing (S)
Thinking (T) – Feeling (F)
Judging (J) – Perceiving (P)
(More can be learned about what these mean here)

This dataset contains over 8600 rows of data, on each row is a person’s:

1. Type (This person's 4 letter MBTI code/type)
2. A section of each of the last 50 things they have posted (Each entry separated by "|||" (3 pipe characters))

### Acknowledgements

This data was collected through the PersonalityCafe forum, as it provides a large selection of people and their MBTI personality type, as well as what they have written.

## Steps
Our goal is to split each 'posts' entry up into individual entries categorized by MBTI type, then clean the data to make it appropriate for use in a text classification model. For this task, ```pandas```, ```matplotlib```, ```nltk```, and ```re``` libraries will be used.
### 1. Visualization
Once the data is read into the environment, there is a total of 8675 rows of data. use ```.value_counts()``` on personality type to see how many entries the dataset has per personality type. This returns a skewed distribution of data over personality types. 
### 2. Entry Splitting
Since each entry is actually described as having 50 separate comments separated by ```"|||"``` characters. Set the personality type (```mbti_df.type```) as the index, then split each entry by these characters. Stack the resulting data on the original dataframe, then unstack the index at level=0 to reset the index and fill each new entry in``` mbti_df.type``` with the corresponding personality type.
### 3. Re-checking the Data
Once the entries are split, re-examining the data shows that the dataframe now contains 422,845 entries (433,750 expected). The data is still skewed with several personality types disproportionately represented. 
### 4. Remove Escaping HTML Characters
Clean out escaping HTML characters, since this data was presumably collected from the web. Escaping HTML characters can muck up code and cause unexpected problems, so get rid of them using the ```html``` library's ```.unescape()``` function. 
### 5. Remove Hyperlinks
Many of the entries contain hyperlinks to webpages. Since we won't be using any of these in text analysis, remove them. I wrote a function utilizing the ```re``` library's ```.sub()``` function along with a regular expression. 
### 6. Remove Contractions
All the contractions need to be removed. Just like escaping HTML characters, apostrophes  can really cause problems later down the road. Also, when the time comes to remove stopwords, it will be better to have the contractions full english representation,  so using a dictionary of contractions, map all contractions to their regular english counterparts.
### 7. Remove Digits
Since digits won't contribute to a text analysis, using ```re``` library's ```.sub()``` and a regular expression, remove all digits from entries.
### 8. Remove Punctuation
To prevent any odd interaction with code in the future, remove all punctuation from the entries. It won't be useful anyway. I used ```str.replace(```) with a regular expression to replace all punctuation with an empty string. 
### 9. Remove Stopwords
Remove all the stop words in the dataframe. Stopwords are words that don't really contribute anything useful to the text analysis so  just remove them completely using stopwords from ```nltk.corpus```
### 10. Filter Out Empty Entries
The result of using all these techniques on the dataframe is a lot of entries in ```mbti_df.clean_posts``` with empty strings. Filter those out.
### 11. Re-check Data
The cleaning has resulted in 13,680 entries being dropped (from 422,845 to 409,165). Checking the distribution of total entries by personality type reveals an exsacerbation of the skewed distribution. 
