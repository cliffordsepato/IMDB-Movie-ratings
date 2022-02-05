# Project-2-Group-1

## Proposal

Three datasets were utilised, two of which originated from IMDb and the third from wikipedia. The IMDb data was contained within tsv files, a table was extracted from a wikipedia page to make up the third dataset. The aim was to compare the highest grossing movies from Wikipedia against the highest rated movies on IMDB, to see if there is a correlation between how well a movie perfoms and the rating it recieves.The data was transformed in jupyter notebook and loaded into Postgres (pgAdmin) where individual tables represented each dataset. These tables were then merged to produce a table showing the rank of highest grossing movies and the ratings and votes recieved on IMDB.
From the table we can see that there is no clear correlation between high rating and high grossing movies, though the high grossing movies err on the side of high rating, the highest rated movies are not necessarily the highest grossing. The highest grossing movie is Avatar, though the rating is only 7.8. The highest rated movie is The Dark Knight, though this is only the 48th highest grossing movie. 


## Report
**Extraction**

The IMDb datasets were downloaded from https://datasets.imdbws.com/ as zipped tsv files. After the files had been unzipped using 7zip/winzip, they were imported into jupyter notebook. Two datasets were downloaded, titled 'title.ratings.tsv' and 'title.basic.tsv'. 

The basic file contained information regarding the unique ID, format of the title (e.g. if it is a move, tv series etc.), main promotional title used, original title, if it is aimed for an adult audience (18+), release year, end year for the series, the runtime of the title and the genre.

The rating file contains unique ID, average rating and number of votes for titles.

The wikipedia data was taken from 'https://en.wikipedia.org/wiki/List_of_highest-grossing_films'. The table was read and imported into jupyter notebook.

**Transformation**

The IMDb data was inserted into dataframes in jupyter notebook. Both datasets were filtered by format type to present only those that were movies. The basic and rating tables were then merged using the unique ID (tconst). Null values appeared as the rating data could not be filtered by format type. The null values were dropped.
The data was then sorted by the number of votes in descending order. The index was reset and the columns that were needed from the tables were then selected (averageRating, numVotes and primaryTitle). These columns were then renamed. This data was then exported as a csv file.

The wikipedia data was read from the webpage and imported into a dataframe. The required columns were selected (Title and Rank) and renamed. This data was exported as a csv.

Web scraping:

We used rotten-tomatoes-scraper library to scrap Rotten Tomatoes website to extract metadata of movies. All what you need to do is to feed movie_url or movie_title to extract the movie metadata. A list with movie's titles from IMDB files was created which helped us to feed the movie_title. All the extractions from Rotten Tomatoes were stored in a list of dictionaries and transformed after in a dataframe. We merged Rotten Tomatoes dataframe with IMDB dataframe to have all data in one table.
A database called movie_list was created in PostrgeSQL and the new created dataframe was loaded into database.

**Loading**

The IMDb and wikipedia data was imported into SQL database (Postgres) using the connection in jupyter notebook. The tables were merged in SQL user an inner join in order to compare the highest grossing films to the highest rated films.
