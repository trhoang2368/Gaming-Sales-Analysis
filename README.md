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
- All the sales columns (na_sales, eu_sales, jp_sales, other_sales, and total_sales) have the unit of millions USD 
## III. Data Exploratory + Data Analysis 
### 1) Answering General Questions: 
After handling the data, I think of several potential questions that can be answered from this data set. Those questions assist me in achieving my goal: building a measurable marketing strategy.

a) The total sales for each game - grouping the game based on only its' name and not its' platform. How many games were released in different years?
- 'games_sales' table is about the total sales for each game.
- The number of game released per year changes from having less than 100 (1980-1993), to a significant spike 1482 in 2009. In the most current year from 2012 - 2016, the number of games released per year is rooughly 500-600. 

b) Platform general analysis: 

 b.1) How sales varied from platform to platform? Build a distribution graph based on the platforms that have the greatest total sales. Find platforms that used to be popular but now have zero sales.
- I create the distribution graphs for top platforms that have the highest total sales

![image](https://user-images.githubusercontent.com/60806068/88999011-5ed8a980-d2c1-11ea-8464-509cd6f5c4ac.png)

Find platforms that used to be popular but now have zero sales. How long does it generally take for new platforms to appear and old ones to fade?
- From the 10 graphs above, we do see that the top 3 platforms that used to be famous but now has no sales are PS2 and PS

 b.2) How long does it generally take for new platforms to appear and old ones to fade? 
- The average time before a platform fades:  7.818181818181818
<p> Before determining the current top selling platform, the question regarding to the what time frame is the most suitable to analyze need to be answered. Can I eliminate irrelevant time frame? For example, if we are studying the current marketing trends, it wouldn't make sense to consider old trends in 1980. </p>
- Because what we are focusing on analysing the potential platforms and the platform that decreases in demands. For a platform, a new technology usually last for around 7-8 years. I only need to consider from 1999 up until 2016; I would drop all the year before 1999. 
- I am also dropping all the platforms that their total_sales is 0 for more than 3 years consecutively. Because this is a good sign that the technology for that platform is outdated.

 b.3) Which platforms are leading in sales? Which ones are growing or shrinking? Create a table of potentially profitable platforms and its total sales globally 
- After filtering out the year (removing all the year before 1999), I would deliver distribution graphs of the top 10 platforms that are still available. From those graphs, the potential growing platforms are 'ps4' and 'xone'
- The shrinking platforms are: 'x360', 'ps3', 'wii', '3ds', 'psp', 'wiiu'
- The platforms that would still be in business: 'pc'

c)  Games Sales analysis:   
d.1) Build a box plot for the global sales of all games, broken down by platform. Are the differences in sales significant? 

Boxplot of the total sales per platform 

![image](https://user-images.githubusercontent.com/60806068/88999353-4f0d9500-d2c2-11ea-9711-48e776057e4f.png)

- The boxplot shows that the average sales that each game generate is similar throughout every platforms, which is roughly 1 million dollar. But the range that the sales might actually end up can go any from roughly 0 millions USD to 20 millions USD
d.2) Compare the sales of the same games on other platforms.
- The popular the platform, the higher the total sales within the same game. For example,'ps3' is one of the highest total sales platforms and A game would sale better if it is available in 'ps3'.
- Because of the nonpopularity of 'psv', not that many games produced in that platform; if they do, the sales of a game in 'psv' don't generate that much interest compared to the more popular one 'ps3' 

e) Video games genre: Take a look at the general distribution of games by genre and their sales. What are the most profitable genres globally?


![image](https://user-images.githubusercontent.com/60806068/88999564-e8d54200-d2c2-11ea-8f7b-381a57f263dc.png)

- Most profitable genres: 
    - Action, shooter, sports 
- Least profitable genres: 
    - Puzzle, Strategy, Adventure
### 2) Regional marketing analysis - Europe, North America, and Japan
- The top five platforms and genres for each region; describe and analyze the findings

The top 5 platforms: 

![image](https://user-images.githubusercontent.com/60806068/89000592-bc6ef500-d2c5-11ea-9fb1-9185f4084a6d.png)

   - Within the top 5 platorms for every region, the common platform that creates the most profits is 'ps2'.
    - The market share for EU and North America is pretty similar because there are a lot of similar platforms, 'ps3', 'x360', 'ps2', 'wii'. The difference is that in NA region, users prefer 'ps' and in EU region, users prefer 'ps'


The top 5 genres: 

![image](https://user-images.githubusercontent.com/60806068/89000521-947f9180-d2c5-11ea-8619-a9b69fdd6820.png)

   - The common genres that are famous in the 3 regions: 'action', 'sports', 'misc'
   - Suprisingly, again, top 5 genres for NA and EU are very similar; most of top 5 genres are the same, 'action', 'shooter', 'sports', 'misc'; 
   - The difference is in NA region, the users prefer 'role-playing', in EU region, the users prefer 'racing' 
   - For the 'Japan' market share, their most profitable genre is 'role-playing'

General comments/observation for all 3 regions: 
   - The reason why there are somewhat huge difference between the best selling genre in 'Japan', 'EU' and 'NA' because of culture. There are somewhat resemblences in the EU and NA customer's culture so therefore these 2 regions share similarity in both top genres and top platforms 

- Do ESRB ratings affect sales in individual regions?

![image](https://user-images.githubusercontent.com/60806068/89000200-c2b0a180-d2c4-11ea-832a-e4dc340af42a.png)

   - Because the majority of the games are in the E rating. It is not surprised that in all 3 regions, the 'E' rating has the highest sales. 
   - In the NA region, there are a roughly 300 millions USD difference between E and other ratings. This might mean that the users in the NA has a strong preference towards E rating
   - In JP regions, the sales for M rating is not as preference comparing to other rating games. 
   - So far, most likely that the E rating games would generate the more sales compared to other due to its vast audience and all ages friendly.

## IV. Test the following hypotheses:
### 1) There is Relationship between user/critic reviews and total sales of a game

<p>I supposed that the user/critic score might affect a sale of the game </p>
- The platform I choose to analyze is 'x360' because it ranks the second highest total_sales and that platform is still available in 2016. I want to understand what factor causes 'x360' to reduce sales. 

![image](https://user-images.githubusercontent.com/60806068/88997195-1919e200-d2bd-11ea-912b-bd798c3b9d93.png)

![image](https://user-images.githubusercontent.com/60806068/88997222-2a62ee80-d2bd-11ea-9090-4b5d2a50a949.png)

- From both of the graphs, there are postive correlation between the total sales and the critic_score/user_score. 
- The user_score and total_sales do show some sort of positive correlation but there are points that are sporadically distributed
- The critic_score and total_sales is more correlated.

To quantified the conclusion, we calculate the correlated values for 2 cases: 
- Coefficient correlation between user reviews and total_sales:  0.18489512471716105
- Coefficient correlation between critic reviews and total_sales:  0.36916629330736916

### 2) Compare the difference the critic score between 2 platforms and between 2 genres: 
Because the total sales of each game correlated with the critic score, I am testing to see if there is any difference between the critic score of the games in the most profitable platform (x360) and the critic score of the games in the most common platform (PC). This might help me understand a little bit about the trends in platform.
- Average critic ratings of the current profitable platform and PC are the same.
<p> I am going to also compare the critic scores of 2 famous genre - Action and Sports. </p>

- Average critic ratings for the Action and Sports genres are the same.

<p> Result of the testing: </p>
- There is difference in the user_score between X360 and PC. This result indicates that eventhough the total sales and critic score are related to each other, that statement doesn't imply that the platforms have higher sales would have higher critic_score.
- There is no difference in the user_score between Xbox One and PC. The average critic_scores for action and sports genres are not different. We can start to see the trend that people who enjoy action game would potentially enjoy sports game.

## V. Conclusions: 
#### 1) Top 10 games that are currently most profitable: 

![image](https://user-images.githubusercontent.com/60806068/89000982-c513fb00-d2c6-11ea-96d1-3b964039a34f.png)

#### 2) Top 5 platforms: 

![image](https://user-images.githubusercontent.com/60806068/89001014-d5c47100-d2c6-11ea-810c-49c79739cca2.png)

#### General conclusions: 
- From the distribution graphs:
    - The platforms that are becoming less popular are x360, PS3, Wii, 3DS and WiiU. 
    - The potential growing platforms are PS4 and XOne 

- User/Critic scores and total sales: 
    - The critic scores influence the total sales more than the user scores. The correlation coefficient of the critic scores and total sales (0.37) is higher than the correlation coefficient of user scores and total sales
    
- Genres and total sales: 
    - The most profitable genre is action. The total sales for games that have action as the genre generate around 1000 millions USD. 
- ESRB rating preference: 
    - Users prefer game that are rated "E - everyone". More games have E as their rating!
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
- Both X-One and PS4 are a potential growing platforms, we can also take advantages of that growth to generate more interest
