# Netflix Movies/TV Shows Analysis
![logo](https://github.com/user-attachments/assets/2852505e-3dd4-4cbb-9d83-5c64ecd562d4)
#
*Netflix* is an American subscription video on-demand over-the-top streaming service. The service primarily distributes original and acquired films and television shows from various genres, and it is available internationally in multiple languages. Launched in 2007, nearly a decade after Netflix, Inc. began its pioneering DVD-by-mail movie rental service. By 2022, *Netflix Original* productions accounted for half of its library in the United States and the namesake company had ventured into other categories, such as video game publishing of mobile games through its flagship service. As of 2025, *Netflix* is the 18th most-visited website in the world, with 21.18% of its traffic coming from the United States, followed by the United Kingdom at 6.01%, Canada at 4.94%, and Brazil at 4.24%.

Using the database of movies and series available on *Netflix*, I conducted a complete analysis of the offer of this streaming platform to draw interesting conclusions and try to find places for optimization.

To do this project I used:
- Microsoft Excel and Power Query to familiarize myself with the data and to do some preliminary data cleaning and preparation,
- SQL (Microsoft SQL Server) to create the database and analyze it by writing queries and creating views,
- Microsoft Power BI to present the data in the form of visualizations.

The dataset was taken from [Kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows).
### Table of Contests
- [Prerequisites](https://github.com/krystian-staszewski/netflix-shows-analysis#prerequisites)
- [Data Overview](https://github.com/krystian-staszewski/netflix-shows-analysis#data-overview)
- [Data Cleaning & Preparation](https://github.com/krystian-staszewski/netflix-shows-analysis#data-cleaning--preparation)
- [Creating a Relational Database](https://github.com/krystian-staszewski/netflix-shows-analysis#creating-a-relational-database)
- [Analysis](https://github.com/krystian-staszewski/netflix-shows-analysis#analysis)
- [Conclusions](https://github.com/krystian-staszewski/netflix-shows-analysis#conclusions)
## Prerequisites
The aim of this project is to build a comprehensive analysis of the data in order to obtain business knowledge. Let’s say we work in the analytics department at *Netflix* or a competitor. Our job is to understand trends and content gaps to drive revenue, engagement, and optimize content strategy and support decisions on which films/series to produce or promote. For example, we can assume that *Netflix* wants to expand in specific countries or in specific age groups. Based on the analysis of the film catalog, it is possible to identify whether, for example, Poland lacks films of a given genre, or whether crime series or comedies are the most popular globally. The results of the analysis will allow for the preparation of strategic recommendations.

The key questions are:
- How many films and how many series do we have?
- How are they distributed over time?
- Which countries and genres dominate?
- Which films/series have the longest duration or the highest rating?
- Which directors and actors have the most titles?
## Data Overview
Using Microsoft Excel, I initially reviewed the data and familiarized myself with it. There are 8807 records in the database and 12 columns:
- `show_id` - unique identifier for each record,
- `type` - type of show; amovie or a TV show,
- `title` - the title of a movie or TV show,
- `director` - name and surname of the director or directors,
- `cast` - names and surnames of the cast of the show,
- `country` - countries where the show is or was broadcast,
- `date_added` - date the show was added to *Netflix*,
- `release_year` - show release date (year),
- `rating` - rating of the show based on content rating system,
- `duration` - length of the show in minutes or seasons,
- `listed_in` - genres in which the show is classified,
- `description` - a short description of the show's plot.
## Data Cleaning & Preparation
Step 1: I loaded the .csv file into Microsoft Excel, separated into columns, and did a preliminary review of the data - primarily to make sure there were no invalid values.

Step 2: I noticed that there are three invalid records. I checked the other columns to find a continuation of this error - the `description` column led me to the source of the problem. After a quick check on the Internet, I came to the conclusion that two of them should be merged and fixed. Since I won't need the show description for my analysis, I decided I could remove the first record.

![1](https://github.com/user-attachments/assets/02f3be04-9f7c-430b-a318-38cb53747b90)

Further steps to prepare the data for analysis will be much more convenient in Power Query, so I decided to move to this tool.

Step 3: I removed the letter "s" from the value in the `show_id` column for better clarity and removed the `description` column because I won't need it for analysis.

Step 4: Due to the large amount of empty/missing values ​​(~800), I decided to replace them with "Unknown". Filling these values ​​in manually would take a very long time. I did this for every column where such deficiencies occurred.

![2](https://github.com/user-attachments/assets/b08b20c5-3f7a-4590-aad3-bb4eebd2e72a)

Step 5: I duplicated my query and started splitting the data into individual tables (I decided to create a star schema) so that I would have unique values ​​for directors, cast, countries, etc. This will help me analyze more precisely, since I had several values ​​in one column. I created dimension tables in which I have each value as unique with its own identifier and tables connecting to the fact table.

![3](https://github.com/user-attachments/assets/25ae4899-f9eb-4f7a-9b64-d6aee9e544a0)
![4](https://github.com/user-attachments/assets/e8635806-9015-48f8-b229-a07b4dd8a77b)

Step 6: I split the `duration` column to get integer in one column, and in the new `duration_type` column to have two categories: minutes and seasons. Thanks to this, I will be able to extract duration data more efficiently.

Step 7: Finally, I created a fact table where I removed unnecessary columns (those already in the dimension tables).

![5](https://github.com/user-attachments/assets/22f33049-4c85-4a3c-82f0-34be4da2b866)
## Creating a Relational Database
Once I had the .csv files created, I went to Microsoft SQL Server Management Studio and created a new database. Then, using the GUI, I loaded the .csv files into the database and set foreign keys for the linking tables. That gave me a ready-made database to work with.

![6](https://github.com/user-attachments/assets/e8f40dee-4ee2-4d70-acf8-f797fe5bfc22)
## Analysis
## Conclusions
