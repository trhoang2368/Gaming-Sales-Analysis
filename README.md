# Gaming-Sales-Analysis

## I. Introduction and analysis goal: 
- The data is from a video gaming online store - Ice. The information available in this data set are user/ critic reviews; genres, platforms, historical games sales in different regions (North America, Europe, Japan and other). The year that we are analyzing for this data set is from 1980 - 2017.
- This analysis helps answering the question of what games, what genres or what platforms are potential big winners. Knowing this piece of information would assist in planning suitable marketing/advertising campaigns.

**Used Library:** pandas, numpy, nltk, re, matplotlib, scipy 

## II. Data Cleansing
 ### 1) Missing values 
 ![image](https://user-images.githubusercontent.com/60806068/88839087-86881e80-d1a8-11ea-94d8-51634e3c3599.png)
 #### Year_of_released column: 
 - Filling the missing values in this column: 
    - Look for the year within the name ome
    - Calculate the average time a game releasing depending on its' platform
 
 #### User_score and Critic_score columns
 - Filling the missing values in this column:
   - Grouping the user_score/critic_score based on the name of the game.
   - Use the average difference between user_score and critic_score to fill the null value
   - For the remaining null values, I fill them based on the average user_score/ critic_score for each genre. 

#### Rating column: 
- There are in total 8 kinds of ratings in the system, E, M, T, E10+, K-A, A-O, EC, RP. But I will regroup them into 3 groups: E - Everyone (K-A, EC, E10+), T - Teen and M - mature (AO), for easier analysis. 
- For missing values in this column: 
   - I use lemmatization and regular expression operations to find what are the highest count words per rating (removing prepositions and articles). The rating of the game would be determine based on what word that has the highest count in what rating
     
 ### 2) Check for duplicates: 
 - Checking for duplicates in the column 'name' and 'platform' and 'year_of_released'. If there are any duplicates, I would combine their sales and calculate the average score for critic_score and user_score
 ### 3) Converting to reasonable data type 
 - Year_of_released has integer data type
 - User_score, critic_score, and all sales columns have float data type
## III. Data Exploratory + Data Analysis 
### 1) Answering General Questions: 
After handling the data, I thought of several potential questions that can be answered from this data set. These questions assisted me in achieving my goal: building a measurable marketing strategy.

a) What are the total sales for each game per year- grouping the game based on only its' name and not its' platform. How many games were released in different years?
- 'games_sales' table is about the total sales for each game?
- The number of game released per year changes from having less than 100 (1980-1993), to a significant spike 1482 in 2009. In the most current year from 2012 - 2016, the number of games released per year is roughly 500-600. 

![image](https://user-images.githubusercontent.com/60806068/89559981-5bbf4b00-d7e4-11ea-95a9-d55eedc3de63.png)  

b) Platform general analysis: 

 b.1) How has sales varied from platform to platform? Build a distribution graph based on the platforms that have the greatest total sales. Find platforms that used to be popular but now have zero sales.
- I create the distribution graphs for top platforms that have the highest total sales

![image](https://user-images.githubusercontent.com/60806068/88999011-5ed8a980-d2c1-11ea-8464-509cd6f5c4ac.png)

Find platforms that used to be popular but now have zero sales. 
- From the graphs above, we do see that the platforms that used to be famous but now has no sales are PS2 and PS
 
 b.2) How long does it generally take for new platforms to appear and old ones to fade? 
- The average time before a platform fades:  7.818181818181818 years 
<p> Before determining the current top selling platform, I take into consideration the average time that a platform would fade in finding the suitable time frame to analyze. The big question I should ask is can I eliminate irrelevant time frames? For example, if we are studying the current marketing trends, it wouldn't make sense to consider old trends in 1980. </p>
- Because what we are focusing on is analysing the potential platforms and the platforms that decrease in demands. As indicated in my findings, new platform technology usually lasts for around 7-8 years. As I only consider from 1999 up until 2016; I drop all of the years before 1999. 
- I am also dropping all the platforms in which their total_sales is 0 for more than 3 years consecutively counting from 2017. Because this is a good sign that the technology for that platform is outdated.
 
 b.3) Which platforms are leading in sales? Which ones are growing or shrinking? Create a table of potentially profitable platforms and its total sales globally 
- After filtering out the year (removing all the year before 1999), I would deliver distribution graphs of the top 10 current platforms and its total sales. 
- From those graphs: 
  - The potential growing platforms are 'ps4' and 'xone'
  - The shrinking platforms are: 'x360', 'ps3', 'wii', '3ds', 'psp', 'wiiu'
  - The platforms that would still be in business: 'pc'

c)  Games Sales analysis:   
d.1) Build a box plot for the global sales of all games, broken down by platform. Are the differences in sales significant? 

Boxplot of the total sales per platform 

![image](https://user-images.githubusercontent.com/60806068/88999353-4f0d9500-d2c2-11ea-9711-48e776057e4f.png)

- The boxplot shows that the average sales that each game generates are similar throughout every platform, which is roughly 1 million dollar. But the range that the sales might actually end up can go any from roughly 0 millions USD to 20 millions USD

d.2) Compare the sales of the same games on other platforms.
- Within the same game, the more popular the platform, the higher the sales compared to other platforms. For example,'ps3' is one of the highest total sales platforms and A game would sell better if it is available in 'ps3'.

e) Video game genres: Take a look at the general distribution of games by genre and their sales. What are the most profitable genres globally?

![image](https://user-images.githubusercontent.com/60806068/88999564-e8d54200-d2c2-11ea-8f7b-381a57f263dc.png)

- Most profitable genres: 
    - Action, shooter, sports 
- Least profitable genres: 
    - Puzzle, Strategy, Adventure
### 2) Regional marketing analysis - Europe, North America, and Japan
- The top five platforms and genres for each region; describe and analyze the findings

The top 5 platforms: 

![image](https://user-images.githubusercontent.com/60806068/89000592-bc6ef500-d2c5-11ea-9fb1-9185f4084a6d.png)

   - Within the top 5 platforms for every region, the common platform that creates the most profits is 'ps2'.
   - The market share for EU and North America is pretty similar because there are a lot of similar platforms, 'ps3', 'x360', 'ps2', 'wii'. The difference is that in NA region, users prefer 'ps' and in EU region, users prefer 'ps'

The top 5 genres: 

![image](https://user-images.githubusercontent.com/60806068/89000521-947f9180-d2c5-11ea-8619-a9b69fdd6820.png)

   - The common genres that are famous in the 3 regions: 'action', 'sports', 'misc'
   - Surprisingly, top 5 genres for NA and EU are very similar; most of top 5 genres are the same, 'action', 'shooter', 'sports', 'misc'; 
   - The difference is in NA region, the users prefer 'role-playing', in EU region, the users prefer 'racing' 
   - For the 'Japan' market share, their most profitable genre is 'role-playing'

General comments/observation for all 3 regions: 
   - The reasons for the difference between the best selling genre or preferable platform in 'Japan', 'EU' and 'NA' come from culture and users' preferences. There are similarity in the EU and NA customers' preference so these 2 regions share similarity in both top genres and top platforms 

- Do ESRB ratings affect sales in individual regions?

![image](https://user-images.githubusercontent.com/60806068/89000200-c2b0a180-d2c4-11ea-832a-e4dc340af42a.png)

   - Because the majority of the games are in the E rating. It is not surprised that in all 3 regions, the 'E' rating has the highest sales. 
   - In the NA region, there is a roughly 300 millions USD difference between E and other ratings. This might mean that the users in the NA has a strong preference towards E rating
   - In JP regions, the sales for M rating is not as preferred compared to other rating games. 
   - So far, it is most likely that the E rated games would generate more sales compared to games with other ratings due to its vast audience and all ages friendly.

## IV. Testing the following hypotheses:
### 1) There is Relationship between user/critic reviews and total sales of a game

<p> My initial hypothesis is the user/critic score might affect a sale of the game </p>
- The platform I choose to analyze is 'x360' because it ranks the second highest total_sales and that platform is still available in 2016. I want to understand what factor causes 'x360' to reduce sales. 

![image](https://user-images.githubusercontent.com/60806068/88997195-1919e200-d2bd-11ea-912b-bd798c3b9d93.png)

![image](https://user-images.githubusercontent.com/60806068/88997222-2a62ee80-d2bd-11ea-9090-4b5d2a50a949.png)

- From both of the graphs, there are positive correlation between the total sales and the critic_score/user_score. 
- The user_score and total_sales do show some sort of positive correlation but there are points that are sporadically distributed
- The critic_score and total_sales is more correlated.

To quantify the conclusion, I calculate the correlated values for 2 cases: 
- Coefficient correlation between user reviews and total_sales:  0.18489512471716105
- Coefficient correlation between critic reviews and total_sales:  0.36916629330736916

### 2) Compare the difference the critic score between 2 platforms and between 2 genres: 
Because the total sales of each game correlated with the critic score, I tested to see if there are any differences between the critic score of the games in the most profitable platform (x360) and the critic score of the games in the most common platform (PC). This might help me understand a little bit about the trends in platform with a critic reviews' perspective

- Null hypothesis H_0: There is no difference in the average critic_score between 'X360' and 'PC' 
- Alternative Hypothesis H_a: There are differences in the average critic_score between 'X360' and 'PC'

<p> Similarly, I am going to also compare the critic scores of 2 famous genre - Action and Sports. </p>

- Null hypothesis H_0: There is no difference in the average critic_score between Action and Sports 
- Alternative Hypothesis H_a: There are differences in the average critic_score between Action and Sports 

**Result of the testing:**

- Comparing the average critic_score between 2 platforms:
  - There is a difference in the critic_score between X360 and PC. This result indicates that even though the total sales and critic score are related to each other, that statement doesn't imply that the platforms have higher sales would have higher critic_score
- Comparing the average critic_score between 2 genres:
  - There is no difference in the critic_score between Action and Sport. We might start to see the trend that people who enjoy action games would potentially enjoy sports games.

## V. Conclusions: 
#### 1) Top 10 games that are currently most profitable: 

![image](https://user-images.githubusercontent.com/60806068/89000982-c513fb00-d2c6-11ea-96d1-3b964039a34f.png)

#### 2) Top 5 platforms: 

![image](https://user-images.githubusercontent.com/60806068/89001014-d5c47100-d2c6-11ea-810c-49c79739cca2.png)

#### General conclusions: 
- From the distribution graphs:
    - The platforms that are becoming less popular are x360, PS3, Wii, 3DS and WiiU. 
    - The platforms with high growth potential are PS4 and XOne 

- User/Critic scores and total sales: 
    - The critic scores influence the total sales more than the user scores. The correlation coefficient of the critic scores and total sales (0.37) is higher than the correlation coefficient of user scores and total sales
    
- Genres and total sales: 
    - The most profitable genre is action. The total sales for games that have action as the genre generate around 1000 millions USD. 
- ESRB rating preference: 
    - Users prefer games that are rated "E - everyone". More games have E as their rating!
### Potential Marketing Strategy: 
- The common strategy for all regions:
  - Promoting the top 10 games that are currently the best-selling games in the world (including the total amount of money or games have sold throughout the world are excellent ways to attract customer)
  - Focusing on promoting games that have genre 'action' with high critic scores and are available in famous platform PS, PS2 and DS

- The store should have their strategy slightly different depending on their markets:
  - In Japan, beside games that have genre action and are available on PS:
     - Focusing on promoting games that have role-playing genre
     - Other preference platforms are snes, 3DS
     - Maybe promoting other famous genres: sports, misc, platform
  - NA and EU markets share a lot of similarity so it is reasonable if they share similar marketing strategies
      - Other preference platforms are PS3, Wii, X360
      - Maybe promoting other famous genres shooter, sports, misc, role-playing and racing
- Both X-One and PS4 are a potential growing platforms, we can also take advantages of that growth to generate more interest
