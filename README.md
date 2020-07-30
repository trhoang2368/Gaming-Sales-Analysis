# Gaming-Sales-Analysis

## I. Introduction and analysis goal: 
- The data is from an online store - Ice - selling video games. The information available in this data set are user, critics reviews; genre, platforms, historical games sales in different region (North America, Europe, Japan and other)
- This analysis help answering the questions what games, what genres or what platforms are potential big winners. Knowing this piece of information would assist in planning suitable marketing/advertising campaigns.
** Library:** pandas, numpy, nltk, re, matplotlib, scipy 

## II. Data Cleansing
 ### 1) Missing values 
 ![image](https://user-images.githubusercontent.com/60806068/88839087-86881e80-d1a8-11ea-94d8-51634e3c3599.png)
 #### Year_of_released column: 
 - I find this column based on the what platform the game is using. To fill the missing values, I calculate the average time a game releasing depending on its' platform
 
 #### User_score and Critic_score columns
 - Firstly, I would fill those null by grouping the user_score/critic_score based on the name of the game.
 - I find the average of the difference between the two columns. If a row of either columns has null and the other column hasn't, then I would use the difference to calculate the column that has a null value. 
 - For the remaining null values on both column, I would fill them based on the average user_score/ critic_score for each genre. 

#### Rating column: 
- There are in total 8 kinds of rating in the system, E, M, T, E10+, K-A, A-O, EC, RP. But I will group them to 3 groups: E - Everyone, T - Teen and M - mature for easier analysis. 
- To handle missing values, I use lemmatization and regular expression operations to find what are the most popular words (the condition is the count for each word per rating is larger than 10) among 3 rating
- To make my list of most popular word to be precise, I elimate preposition and article
 ### 2) Check for duplicates: 
 - I am checking for duplicates in the column 'name' and 'platform' and 'year_of_released'. If there are any duplicates, I would combine their sales and calculate the average score for critic_score and user_score
 ### 3) Converting to reasonable data type 

## III. Data Exploratory 
### 1) Answering General Questions: 
I think of several potential questions that can be answered from this data set. Those questions assist me in achieving my goal: building a measurable marketing strategy 

### 2) Regional marketing analysis - Europe, North America, and Japan

## IV. Hypothesis Testing
### 1) Relationship between user/critic reviews and total sales of a game
### 2) Comparing user reviews between 2 platforms: 
## 
## V. Conclusions: 
#### 1) Top 10 games that are currently most profitable: 
#### 2) Top 5 platforms: 
### Potential Marketing Strategy: 
- The common strategy for all regions:
  - Promoting he top 10 games that are currently the best-selling games in the world (including the total amount of money/or games have sold through out the worlds are an excellent way to attract customer)
  - Focusing on promoting games that have genre 'action' with high critic scores and are available in famous platform PS, PS2 and DS

- The store should have their strategy slightly different depending on their markets:
  - In Japan, beside games that have genre action and are available in PS:
     - Focusing promoting game that have role-playing genre
     - Other preference platforms are snes, 3DS
     - Maybe promoting other famous genres sports, misc, platform
  - NA and EU markets share a lot of similarity so it is reasonable if they share similar marketing strategies
      - Other preference platforms are PS3, Wii, X360
      - Maybe promoting other famous genres shooter, sports, misc, role-playing and racing

    Both X-One and PS4 are a potential growing platforms, we can also take advantages of that growth to generate more interest


