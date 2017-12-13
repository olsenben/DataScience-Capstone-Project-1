![alt text](https://startupbeat.com/wp-content/uploads/2015/12/springboard-logo-secondary-RGB.jpg "Logo Title Text 1")
# Capstone Project 1 - Milestone Report
### Prepared by Ben Olsen
## What Is The Problem You Want To Solve?
This project is an effort to determine the usefulness of the Myers Briggs Type Indicator, which in short is 
an "introspective self-report questionnaire with the purpose of indicating differing psychological preferences in how people 
perceive the world around them and make decisions" according to Wikipedia. While generally accepted by various internet
communities as a valid assement of personality type, the professional field of psychology and other technical researchers have
more or less discarded this test due to its poor retestibility results, mostly due to the fact that it relies on categorical 
classification based on a continuous scale (a difference of one point could result in a misclassication, a margin of error that professionals find too unforgiving to be useful). While the clinical application of the test has been discredietd as unreliable and ultimately left to the wayside by clinicians, the test's usefulness has yet to be evaluated in the context of online behavior. This project will attempt to validate the relevance of the MBTI in an online social context based on an analysis of a person's online posting characteristics, specifically by examining the features of text that he or she post online. While MBTI is no longer considered to be theoretically validated construction of personality, a distiguishable difference in features of text per reported personality that of other personalities could potentially point a manifestation of personality in posting style, as well as a relevance in testing other, more clinically sound personality tests (such as the Big 5) as the data becomes more readily accessible.
## Who Is Your Client And Why Do They Care About This Problem?
Natural language processing and classification has a variety of applications varying in usefulness, but the ability to analyze text and classify people into personality types based on their choice of language has few specific uses that stand out as particularly valuable accomplish the goals of various kinds of clients.
#### 1. Media And Content Delivery

   Media companies have build long and illustrious histories of reporting valuable news and delivering useful content in the past, but in the 21st century the move to digital media began to wreck havoc on many last century media giants. The shift in media consumption habits created a valuable marketplace online for digital media gurus to new ways to deliever content, and one of the more modern inventions of content delivery of this century is curate content, which is content delivery tailored to specific audiences based on their media consumption habits. The ability to classify content based on the word usage of the writer to know that writers personality style will also reveal what kind of readers the content will resonate with. Additionally, being able to classify users based on their language usage can reveal valuable details about them that can help tailor specific content for their  consumption.

#### 2. Targeted Advertising

   Many modern companies are very image-centric, meaning that they monitor their public image and the ethos that they exude quite religiously. Knowing what subset of personality types that their advertising campaigns are resonating with provides another layer of understanding beyond simple sentiment analysis. Additionally, a marketing company could more easily target user subsets by identifying their personality types based on their language choice in their posting style and tailor ad content to that particular personality type.
   
#### 3. Hiring

   Hiring agencies understand how important it is for a person's personality to match the workplace where they are being placed. Hoever, much foreward-facing content that individuals contribute to professional sites where networking and professionalism are the aim is carefully curated and oriented to be apear professional and appealing. Beyond this curated offering, there is really no way to get a glimpse of what a person is like without a third-party reference to their strengths, weaknesses, and personality attributes. Being able ascertain personality traits from a person's writing style would provide an unbiased measure of where their strengths might lie and what placement would suit them best. 

## What Data Is Necessary? 
The dataset in question for this project is a large number of people's MBTI type and content written by them. This data was collected through the PersonalityCafe forum, as it provides a large selection of people and their MBTI personality type, as well as what they have written. The full description for this dataset can be found @ <https://www.kaggle.com/datasnaek/mbti-type>

The Myers Briggs Type Indicator (or MBTI for short) is a personality type system that divides everyone into 16 distinct personality types across 4 axis:

* Introversion (I) – Extroversion (E)
* Intuition (N) – Sensing (S)
* Thinking (T) – Feeling (F)
* Judging (J) – Perceiving (P)

This dataset contains over 8600 rows of data, on each row is a person’s:

1. Type (This person's 4 letter MBTI code/type)
2. A section of each of the last 50 things they have posted (Each entry separated by "|||" (3 pipe characters)). 

### Steps
The goal was to clean the entries categorized by MBTI type to make it appropriate for use in a text classification model. For this task, ```pandas```, ```matplotlib```, ```nltk```, and ```re``` libraries were be used.
#### 1. Visualization
Once the data was read into the environment, there was a total of 8675 rows of data. Using ```.value_counts()``` on personality type showed how many entries the dataset had per personality type. This returned a skewed distribution of data over personality types, meaning that some personality types appeared more often than others. 
#### 2. Entry Combining
Each entry was actually described as having 50 separate comments separated by ```"|||"``` characters. Utilizing the ```re``` library's ```.sub()``` function, the pipe characters were replaced with whitespace to create one long string of text. 
#### 3. Remove Escaping HTML Characters
The data was cleaned of escaping HTML characters, since this data was presumably collected from the web. Escaping HTML characters can muck up code and cause unexpected problems, so they were removed using the ```html``` library's ```.unescape()``` function. 
#### 4. Remove Hyperlinks
Many of the entries contained hyperlinks to webpages. Since there aren't useful in text analysis, they were removed. I wrote a function utilizing the ```re``` library's ```.sub()``` function along with a regular expression to accomplish this. 
#### 5. Remove Contractions
All the contractions had to be to be removed. Just like escaping HTML characters, apostrophes can really cause problems later down the road. Also, when the time comes to remove stopwords, it will be better to have the contractions full english representation,  so using a dictionary of contractions, all contractions  were mapped to their regular english counterparts.
#### 6. Remove Digits
Since digits don't contribute to text analysis, using ```re``` library's ```.sub()``` and a regular expression, all digits were removed from entries.
#### 7. Remove Punctuation
To prevent any odd interaction with code in the future, all punctuation was removed from the entries. It isn't useful anyway. I used ```str.replace()``` with a regular expression to replace all punctuation with an empty string. 
#### 8. Remove Stopwords
Finally, all the stop words were removed from the dataframe. Stopwords are words that don't really contribute anything useful to the text analysis so I removed them completely using stopwords from ```nltk.corpus```.

## What Other Data Could Be Useful?




