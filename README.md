# Microsoft Studio Project Overview

# Final Project Submission

Please fill out:
* **Student name:** Shayan Abdul Karim Khan
* **Student pace:** Self Paced
* **Scheduled project review date/time:** 
* **Instructor name:** Abhineet Kulkarni
* **Blog post URL:** 

## Problem Overview

### Venture Opportunity:
A lot of companies are producing original video content generating huge revenues, including box office movies. In the post-pandemic world, people have filled theaters and cinema halls allowing top movies to rack up millions in box office revenues.

### Client Insight:
Microsoft has decided to venture into the world of movie production with a new movie studio. In order to make the movie studio a success, Microsoft needs to understand what kind of movies to produce. 

### Client Goals:
This notebook focuses on three client goals:
1. Positive viewer response
2. Impactful market entry
3. Profitable 

### Business Questions
This notebook will focus on three business questions to help achieve the client's goals. There are **three** business questions that this notebook will recommend answers to:

1. Which genres to focus on?
    - The popular genres will identify what type of movie will receive positive viewer responses
    
*It is important to understand the customer base and how different factors influence their behavior. Any product should primmarily be focused on providing the customer with whata they need. This guarantees success in the long run and develops customer loyalty. Customer satisfaction is directly correlated with profits and better reviews which will allow long-term success.*
<br>


2. Should the movie be launched internationally?
    - The international launch of the movie will help the client in the future with regards to an impactful market entry. If the movie needs to be launched internationally, it will need to have a cast, crew, story, advertising and marketing plans made accordingly. Whereas a only a US specific production would require different plans.
<br>


3. What should be the expected budget/initial investment?
    - The financial aspects will help identify how successful the business side will be. It is important to remember that a movie can be very popular but if it's not adequately profitable, it will be difficult for the movie studio to continue operations.
<br>


### Value Proposition:
This notebook will look at multiple sources of data to understand what will allow Microsoft to generate the most promising content and set it up for long-term success. The strategy described below will be used to generate actionable insight to answer the **Business Questions** based on two main criterion:
<br>
1. *Movie Reviews*
2. *Movie Profits*

## Strategy
To answer the complex question of the secret ingredients of a successful movie, there are a myriad of aspects to consider. The different aspects analyzed in this notebook will be evaluated based on the two KPIs listed above; Profits and reviews. 

Good **Movie Reviews** are important indicators of the quality of a movie nonetheless they can not solely justify an investment opportunity. Therefore **Movie Profits** will be used as an indicator of high potential investment opportunities. The two KPIs coupled together can give the client a more thorough lay of the land. 

These KPIs will be used to answer the three main business questions in the following manner:

1. Which genres to focus on?
    - genre vs average reviews analysis
    - genre vs profit analysis
    - genre vs average reviews vs profit analysis
<br>


2. Should the movie be launched internationally?
    - genre vs domestic profit analysis
    - genre vs foregin profit analysis
<br>


3. What should be the expected budget/initial investment?
    - genres vs production budget vs domestic & foreign profits analysis

## Data Sources

To solve the problem, 5 data sources have been gathered. These data sources will be investigated to identify which data will be helpful in the analysis. The data sources are listed below:

- **[Box Office Mojo](https://www.boxofficemojo.com/)**

- **[The Numbers](https://www.the-numbers.com/)**

- **[Rotten Tomatoes](https://www.rottentomatoes.com/)**

- **[IMDB](https://www.imdb.com/)**

- **[TheMovieDB](https://www.themoviedb.org/)**

The content and relevance of the data available is dealt with in detail in the **Data Understanding** Section.

## Data Understanding

### Box Office Mojo Dataset
The **Box Office Mojo** dataset is stored in the `zippedData` folder. 

The file is called `bom.movie_gross.csv.gz`.

There are **five** columns in this dataset:

- `title` : This is the movie title. It is an important column because it shows which movie the record is for. This will be valuable in comparing/merging data to give more context to the analysis.
<br>

- `studio` : This gives an outlook on the competitors in the market. This won't be valuabale in answering any of the three business questions.
<br>

- `domestic_gross` : This data is particularly important because it provides the financial overview within the US market. Since there is no currency sign associated, we will assume `$` but more on that in the **Data Prepartion** section.
<br>

- `foreign_gross` : This is similar to `domestic gross` and equally valuable. It provides insights on foreign performance of a movie.
<br>

- `year` : This is the year that the movie was released. It is important to keep the year in mind so that the analysis isn't skewed. We will later evaluate which timelines to focus on for the analysis.

There are `3387` records in total in this dataset which is a good size for our analysis. 

**Summary:** 

The **Box Office Mojo** data will be valuable to conduct financial analysis but we have another financial informatiion dataset that we'll look at next. We will compare these two datasets to understand what information to carry into our analysis from these.


### The Numbers Dataset
This dataset is stored in the `zippedData` folder. 

The file is called `tn.movie_budgets.csv.gz`.

There are **six** columns in this dataset with a total of `5782` records with no missing values.

It is difficult to guage what the `id` column is doing in this dataset. We should be able to drop this column since it doesn't signify anything unique. This will be done in the **Data Preparation** section.

A brief overview of the columns of interest in the `tn_df` dataframe is as follows:


- `release_date` : This is the release date of the movie and will be valuable in determining if we wwant to limit the timeline of the dataset we use.
<br>

- `movie` : This is the movie name which shows which movie the record is for.
<br>

- `production_budget` : This column is important in understanding the initial investments that have to be made by the client. This will also allow us to calculate the net profits.
<br>

- `domestic-gross` : Similar to `bom_df`, this column provides insight into the revenue generated in the US market by the movie.
<br>

- `worldwide-gross` : This is slightly different than the `foreign_gross` column of `bom_df`. It was found through exploration and comparison with the **Box Office Mojo** dataset that thiis column is the sum of domestic gross and foreign gross. 

An important thing to note is that `tn_df` has `5782` records while `bom_df` has `3378`. 

**Summary:** 

`tn_df` has similar data bins (i.e. columns) as `bom_df` but more records. Considering that `tn_df` has more records and a complete dataset, therefore it would be better to use this dataset for analysis.

`tn_df` will be the main dataset we will be using to conduct financial analysis.

### Rotten Tomatoes Dataset
There are 2 datasets from Rotten Tomatoes that we are going to explore and understand their utility for our analysis.

- `rt.movie_info.tsv`
- `rt.reviews.tsv`

Both of these files are stored in the `zippedData` folder.

The two datasets are related through the id column as shown below. Since there are multiple reviews for movies, we see a big discrepancy between the total number of records between the two datasets.

`rtmov_df` has `1560` records

`rtrev_df` has `54432` records

![image.png](attachment:image.png)

Since there is no information on the movie name that these records are for, it becomes very difficult to join/compare this data with other datasets. 

Note that the `rating` columns in the two dataframes show different data. The one in `rtmov_df` is to signify what age group the movie was for (eg. R, PG13, etc) whereas the one in `rtrev_df` is the movie review on a scale of 0 to 5.

- `id` : This is the key column in both dataframes. We will be using this column to join the dataframes.
<br>

- `rtmov_df` `rating` : This column contains information on the age group that the movie was released for. For example R-rated movies have age restrictions. This will be valuable in understanding the demographic of the users.
<br>

- `rtmov_df` `genre` : This column provides an insight into what genre the movie was. Comparing this column with `rating` and `reviews` will showcase which genres are highly competetive and which ones are low performingor have high standards.
<br>

- `rtrev_df` `rating`: This column stores the ratings reviewers gave the movie out of 5. This data will be used as the basepoint to compare what type of movies are successful. This column will be renamed to avoid confusion with the `rtmov rating` data.

An important thing to note is that the **Rotten Romatoes** data only has `1560` movie records. This is much smaller than the other two data sources we have looked at. 

Therefore, if we find a dataset with similar information but more records, we will ignore this dataset. 

**Summary:** 

While this data is valuable for analysing genres vs reviews, we need to look at the other datasets with more records before deciding how critical the rotten tomatoes data will be.

### IMDB Database

The **IMDB** Database is stored in the `zippedData` folder.

The file is called `im.db`.

We have the following Entity Relationship Diagram (ERD) explaining the different tables in the database:

![movie_data_erd.jpeg](attachment:movie_data_erd.jpeg)

The `persons` table contains the records for the cast and crew of the movies which are not relevant to the business questions that this notebook explores. 

Nonetheless, this is something that should be investigated separately. Alongside this data, experts in the field of movie production should be consulted to understand which cast and crew would be ideal for the kind of movie that the client decides to pursue.

Leveraging the **ERD** above, we can skip exploring `writers`, `directors`, `principals` and `known_for` tables because these are information about the cast and crew.

The `movie_basics` table give us the principal information about the movies that will be used for joining and relating with other tables. It will be important to use this table in analysis to relate reviews and profits to genres.

It has **six** columns, all with valuable information, with `146144` records which will greatly improve the analysis.

- `movie_id` : This is the primary key of the table. It can be seen in the ERD that it relates to the other tables based on this id.
<br>

- `primary_title` : This column represents the changed title for different markets. These can be translations if the movie is a foreign production. A lot of movies are released with different names in different regions. This might end up not being a useful column for analysis but further exploration will calrify that.
<br>

- `original_title` : This column is self-explanatory. It has the original title of the movie in the local language of the region it was prooduced in. This will be important to link to the other datasets and other tables within the database.
<br>

- `start_year` : This is the year that the movie was launched. This will be important to filter the records for the timeline being evaluated.
<br>

- `runtime_minutes` : This column contains the data on the total length of the movie. This data does not contribute to the business questions being answered.
<br>

- `genres` : This column contains the genres of the movie. This will be critical in our analysis to understand which genres should the client focus on.

The `movie_ratings` table will be extremely valuable in analyzing genres vs reviews and generating recommendations for which type of movie should the client pursue.

This is the dataframe storing the average reviews for the movies and the corresponding total number of votes for each movie. 

Nonetheless, it only has `73856` records compared to `movie_basics` `146144` records. Only movies that have reviews data will be used in the analysis.

These reviews can be correlated with the genres of the movies from `movie_basics` using the `movie_id` column. This will give us a good comparison of genres vs reviews.

These can be further analysed with profits for every movie, resulting in a genres vs reviews vs profits comparison.

This dataframe has **three** columns:

- `movie_id` : This is the key that is relating this table to the `movie_basics` table.
<br>

- `averagerating` : This is the average of all the ratings for a specific movie.
<br>

- `numvotes` : This is the total number of reviews that a movie received. It will be important to set a baseline of minimum number of votes to use for filtering the data to avoid skewwing results.


`movie_akas` is a relatively large dataframe with `331703` records. This is because the `title` column has separate names that movies had in different regions. 

We will use the laanguage column to identify which movies were produced for most of the US population. 

Using **English** as the baseline laanguage will allow the movie to have the greatest reach in doemstic and international markets.

The are `44700` original titles in this dataset but almost all of them are missing region and lanaguage data.

This renders this table invaluable for our analysis since it doesn't have any extra information that will help answer the **Business Questions**

That finishes the exploration of the `im.db` database.

**Summary:** 

- `persons`, `principals`, `known_for`, `directors` and `writers` contain information on cast and crew. These tables will not be used in the analysis because they do not add value to answering the **Business Questions** laid out in the **Problem Overview** section.
<br>

- `movie_basics` is an important table wih the principal information about the movie. This table is linked to two other important tables and will be critical in the analysis.
<br>

- `movie_ratings` stores the average ratings and number of votes for movies. This will serve as the main reference for analyses based on reviews.
<br>

- `movie_akas` contains movie names in different regions. Because of missing values, it doesn't provide us any valuable data to use in our analysis. This table will also be ignored. 

### The MovieDB Dataset

**The MovieDB** Dataset is stored in the **zippedData** folder.

The file is called `tmdb.movies.csv`.

There are **ten** columns and `26517` records in this dataset.

- The `Unnamed` column is the index of the records therefore this column can be ignored.
<br>

- The `genre_ids` column can be ignored since we can grab the genres from other tables which would be more helpful
<br>

- The `id` column can be dropped because we can use `original_title` as the key to relate to the `im.db` database.
<br>


The columns that we will be carrying into analysis will be the following:

- The `original_language` column can be used to determine which movies will have the greatest reach. Using **English** as a the baseline language, will allow the maximum domestic and international reach.
<br>

- `original-title` : This is the original title of the movie which we can use to correlate data in other dataframes.
<br>

- `popularity` : This will be an important data to look at alongside reviews to analyse the response to the movies. While the scale isn't known, we can manipulate the values to create a custom scale to better understand the values.
<br>

- The `release_date` column can be used to filter records for the timeline that will be used in analsis.
<br>

- `title` : This will be an important column to keep in case we need to link the `bommovies` dataset using the title column instead of `original_title`.
<br>

- `vote_average` : This gives us an extra benchmark to use for comparison of reviews to the `imm.db` database
<br>

- `vote_count` : The number of votes allows us to filter to ensure that wew are not skewing data because of very good or very bad reviews of a only a handful viewers.

**Summmary:** 

The `tmdb_db` dataset will be very useful for analyzing movie reviews vs proftis vs genres. We can directly link this dataset to the `im_db` tables using the `original_title` column.

#### Review
That was a lot of information. Lets take an overall look at the ERD of all of our datasets and talk about which ones we will be using in our analysis, and how we'll use them.
In the diagram below, yellow is for the **IMDB** database. Everything else is labelled.

![Complete%20ERD.png](attachment:Complete%20ERD.png)

`im.db` database is the most valuable database which has all the info for the movies except for revenues.
<br>

- `persons`, `principals`, `known_for`, `directors`, `writers`, and `movie_akas` datasets will be ignored because they are not relevant to the **Business Questions** mentioned earlier.
<br>

- `movie_basics` will be the main dataset used for the principal information for the movies, i.e genre, title, etc.
<br>

- `movie_ratings` will be used for tallying up the reviews and correlating genre with review and financial performance.
<br>

`Box Office Mojo` and `The Numbers` datasets are next most valuable ones because they contain information on financial performance of the movies.

- `Box Office Mojo` and `The Numbers` data contains the same financial information. 
<br>

- Since `The Numbers` dataset has more records, the `Box Office Mojo` dataset will be ignored. `The Number` dataset will be used to calculate the profits for financial analysis.
<br>

- The genre, reviews, and financial performance data will be joined with the imdb dataset. The joined dataset will be the main financial analysis daataframe that this notebook will use. 
<br>

- The timeline available in `The Numbers` dataset will be one of the limiting factors for analysis.

`The MovieDB` datasets will serve as an additional resource to compare with `movie_ratings`. The dataset wwill be joined with the `im.db` database and the reviews will be averaged between the two.

The `Rotten Tomatoes` datasets will be ignored because they don't provide any additional value for analysing customer reviews. `im.db` provides movie-specific data with more records.


## Data Interpretation and Visualizations

### Which genres bring in the highest ratings and profits?

#### genre vs ratings analysis:

image.png

We can easilly decypher that the top 4 most popular genre combinations that are rated above average are (Recall that **NA** means that there wasn't a combination for thata column:

1. `Drama`
2. `Adventure, Animation, Comedy`
3. `Comedy, Drame` tied with `Documentary`
4. `Action, Adventure, Sci-fi`

Nonetheless, purely good reviews can't be only reference of producing a successful movie. It needs to be looked at from the financial lens also. For this purpose, we will look at genre vs profits analysis next.

### genre vs profits analysis

image.png

The figure above shows the Top 20 profitable genre combinations.

The most common genre in the top 10 are 
1. Adventure with 10 groupings
2. Action with 7 groupings
3. Fantasy with 6 groupings
4. Family with 5 and Comedy with 5 groupings
5. Animation with 4 and Sci-fi with 4 groupings
6. Musical with 2 and Thriller with 2 groupings
7. Drama, Mystery, Documentary, History with 1 groupings each

We can see that `Adventure` is the big common between these two analysis with **ten** highly profitable combinations. 

`Documentary` and `Drama` only had a **single** combination to their names so we can ignore them because we want to investigate movies that have a high chance of getting good reviews and making a good profit. With only one occurance it greatly reduces the chances of being a profitable venture with either of those genres. 

We did see `Animation` and `Comedy` pop up in the top 10 profitable category with **four** aand **five** combinations.

We also saw `Action` and `Sci-fi` in the race with **seven** and **four** combinations respectively.

We can also see that `Family` and `Fantasy` are up there but our previous analysis showed us that the chances of these movies getting high viewer ratings is low so we are not going to focus on them.

This tells us that we should keep an eye out for the following three categories going forward:

1. `Adventure`
2. `Action`
3. `Comedy`
4. `Animation`
5. `Sci-fi`


### genre vs ratings vs profits analysis

We will focus on the 5 genres that we have shortlisted and their combinations.

image.png

Recapping the 5 genres we shortlisted:

1. `Adventure`
2. `Action`
3. `Comedy`
4. `Animation`
5. `Sci-fi`

We can clearly see some good and bad spikes in the graph:

- `Adventure` is the common genre in all the 5 peaks of movie ratings with the grouping of `Fantasy` in 3 of them.

- In the 8 groupings with 7 or below average ratings, `Adventure` was a part of 4 of them which shows that `Adventure` genre on it's own is a mixed fortune. It is the pairings with `Adventure` that play a big part.

- 4 out of the 7 groupings of `Action` ended up having an average rating of 7 or less. That shows that it is difficult to generate good customer reviews with this genre. In all the 3 groupings that were above 7 were with `Adventure`. We will continue to explore `Action` but in context of pairing with `Adventure`

- `Comedy` faired better with 3 out of 5 combinations racking up average ratings higher than 7 in the most profitable combinations. Out of these 3, 2 were pairings with `Adventure`

- `Animation` had an average performance with 2 out of 4 combinations getting above 7 ratings. Both of these were paired with `Comedy`. We will be looking at `Animation` in combination with `Comedy` pairings for better insights going forward.

- `Sci-Fi` did really good on its own or when paired wiht with `Adventure` and `Drama`. Pairings with `Action` proved to bring down the ratings. We will continue to explore `Sci-Fi` as a possible pairing with `Adventure` or other genres.


In light of these insights, we will shift our focus to looking at pairings with `Adventure` and the following genres:

1. `Action`
2. `Comedy`
3. `Animation` 
4. `Sci-Fi`


We will take a look at foreign success and movie budgets next to understand what pairings will prove to be the best with `Adventure`.

### Should the movie be launched internationally?

Similar to the last analysis, we will cut down our shortlist to the 5 genres and minimumm average rating of 7 to pick out the top genre combinations. Then we will evaluate how did these genres perform in the foreign and domestic markets.

image.png

This chart makes it clear that the launch of a movie in foreign merkets is essential to have high profitability and success. In most of the genre combinations, the foreign profits are eiher dominating the total profits or contributing as much as the domestic profits. 

Lets see how have our shortlisted genres done in domestic and foreign markets:

The `Adventure` genre has consistently brought in almost $200 million profits in the US market.

The most repeated combination with `Adventure` has been of `Action` with 3 out of the 5 shortlisted.

The next most repeated one has been with `Comedy` with 2 combinations.

`Sci-Fi` and `Animation` both had a single combination each with `Adventure`.

The combination with `Sci-Fi` was the highest rated amongst all 5 aand a close second for net profit with almost $550 million.

Interestingly, the combination of `Action, Adventure, Comedy` didn't end up being the most profitable or the best reviewed amongst the 5 but those are the 3 genres which are showing up to be the most consistent in performance. But this combination did bring in the highest domestic profit amongst the shortlisted genres. Therefore, if he client chooses to not pursue an international launch, this cmbination would be the most reliable to bring in high domestic profits.

To finally choose which combination will work best, we still need to look at the production budget required for these genres. This will provide the client insight on which genre to choose depending on the money available to the client.

### What should the budget target be for the movie?

image.png

The highest production budget with the lowest profits was the combination of `Adventure, Animation, Comedy` which rules it out of selection.

The lowest production budget was for `Adventure, Drama, Sci-Fi` and then `Action, Adventure, Comedy` with only a small difference between the two. Both of these genres have similar net profits therefore the financial impacts will also be similar.

This gives the client options on which genre combination to choose from for pursuing the most financially sound option.

## Conclusion and Recommendation

Our analysis gave us the following insights for the questions posed:

1. Which genres bring in the highest ratings and profits?
    - `Adventure` genre is one of the most common genres to produce high customer reviews and good profit margins but it has to be paired with the correct genres to make this possible.
<br>


2. Should the movie be launched internationally?
    - The shortlisted genres were focused arouond `Adventure` because statistically, `Adventure` was the most common genre doing well with reviewers and with profit margins.
    - Between domestic and foreign markets, foreign markets proved to be the more lucrative ones. They contributed significantly to the net profits
 <br>
 
 
3. What should the budget target be for the movie?
    - The shortlisted genres were focused arouond `Adventure` for this analysis.
    - Most of the shortlisted genres had production budgets of $200 million or less except for one exception which was chosen to be ignored.


The recommendations from the analysis are as follows:

The client has 3 options of genres to choose from for **maximum profitability** and **positive viewer reponse**. The pros and cons are listed below with the recommendations:

1. `Action, Adventure, Family` : 
    - Net Profit: ~$600 million
        - This genre combinatiion has the most net profits amongst the three final candidates.
<br>

    - Average Rating: ~7.0
        - `Family` genre combinations are not poopular in having high average ratings so the chances of getting a **positive viewer response** with the genre combination are low.
<br>  

    - Production Budget: ~$175 million
        - This genre combination has the highest production budget amongst the final candidates.    

<br>


2. `Adventure, Drama, Sci-Fi` :
    - Net Profit: ~$550 million
        - This is the second highest net profit amongst the final options
        
        - `Drama` combinations can garner a lot of **positive viewer responses** but they were a rare occurance in the top 20 most profitable genre combinations therefore are not a guarantee to be highly **profitable**.

    - Average Rating: ~8.0
        - This is the highest average rating amongst the final candidates and well above the average of 6.5 of the dataset and 7.0 of IMDB
        - `Drama` genre combinations are the most popular amongst viewers. They were the most common in the high average rating analysis.
    
    - Production Budget: ~$100 million
        - This is the lowest production budget amongst the final candidates

<br>


3. `Action, Adventure, Comedy` : 
    - Net Profit: ~$525 million
    
        - This is the least amount of net profit amongst the final three options. 
        - All of the three genres in this combination were a consistent occurance in the top 20 most profitable genre combinations.
    - Average Rating: ~7.3
        - All of the three genres were the most consistent genres to show up for high average ratings and high proftiability which means that they can garner a lot of **positive viewer response** and be highly **profitable**
    - Production Budget: ~$150 million
        - This is the second highest production budget from the final 3 options.

**Impactful market entry** is a mix of good reviews, high profits and global exposure. Reviewws and profits have already been discussed. Looking at the scope of international market launch, depending on the client's strategy, the options will be limited. The financial performance in domestic and foreign markets of the 3 options is given below:

    1. `Action, Adventure, Family` : 
        - Barely break even. Most of the profits are from international markets
        - Cannot pursue

    2. `Adventure, Drama, Sci-Fi` :
        - Domestic profit of ~$200 million.
        - Foreign profit of ~$350 million.

    3. `Action, Adventure, Comedy` :
        - Domestic profit of ~$200 million.
        - Foreign profit of ~$325 million.
        
        
This shows that for an impactful market entry, international markets can not be ignored and have to be catered to.

With all of that in mind, the final recommendation would be to pursue a film in the genre commbination of `Action, Adventure, Comedy`. 

This is because it will meet all 3 of the client's goals. These 3 genres are most common occurances in the high customer reviews list and the most profitable genres list. This increases the statistical chances of the movie having high **profits** and high **positive viewer responses**.


Alongside the recommendation would be to launch this movie in the international market for greater exposure and profits. 

Also, the average production budget for this genre is consideraably lower and can be recouped just through the domestic revenue streams which is a guarantee of success.

Ensuring that the movie has high chances of good reviews and has a wide exposure across different markets will ensure an **impactful market entry**.
