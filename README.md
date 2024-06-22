# Netflix_Cleaning_Analysis_SQL_Python
  This is ELT project. ELT stands for Extract, Load and Transform . I am using Netflix dataset to clean and analyze the data using SQL and Python.

  Dataset download here: https://www.kaggle.com/datasets/shivamb/netflix-shows 
  
  Project tutorial credit to: Ankit Bansal

  ## Python
  1. Read file using pandas
  2. Connect to SQL server
  3. Check every column character length
  4. Check for missing values

## Cleaning using SQL
### Remove Duplicate
1.	identifies and retrieves all records from the netflix_raw table that have duplicates based on the combination of title (case-insensitive), type, director, and country.
2.	The results are then sorted by the title column.

### Create New Table for Netflix
1.	creates a new table named netflix that contains unique records from the netflix_raw table based on the combination of title, type, director, and country.
2.	includes specific columns and ensures that each combination of these attributes appears only once
3.	A CASE expression is used to handle the duration column: if duration is NULL, it substitutes the value of rating; otherwise, it retains the value of duration.

### Create New Table for Director, Country, Cast and Genre
1.	creates a new table (netflix_directors, netflix_country, netflix_cast, and netflix_genre) by splitting the corresponding column values (director, country, cast, and listed_in) in the netflix_raw table into individual rows.
2.	The cross apply string_split(column, ',') function is used to perform the splitting,
3.	the trim(value) function ensures that the resulting values do not have leading or trailing spaces.

### Populate Missing Values in Country, Duration Columns
1.	populate the missing country values in the netflix_country table by matching directors from the netflix_raw table with the known country values from the netflix_country and netflix_directors tables.
2.	By doing this, it leverages the existing data to fill in gaps where the country information is missing.


## Analysis using SQL

### For each director count the number of movies and tv shows created by them in separated columns for directors who have created tv shows

1.	generates a list of directors who have created both movies and TV shows
2.	For each director, it displays the number of movies they have directed (no_of_movies) and the number of TV shows they have directed (no_of_tvshow).
3.	By using the having clause with COUNT(distinct n.type) > 1, the query ensures that only directors who have directed at least one TV show are included in the results.

### Which country has highest number of comedy movies

1.	finds the country with the highest number of comedy movies
2.	Joining the netflix_genre, netflix_country, and netflix tables.
3.	Filtering for rows where the genre is 'Comedies' and the type is 'Movie'.
4.	Grouping the results by country and counting the distinct show IDs for comedy movies.
5.	Sorting the results in descending order of the count and selecting the top result.

### For each year (as per data added to Netflix), which director has maximum number of movies released

1.	determines the director with the most movies released each year on Netflix
2.	Counting the number of movies added each year for each director
3.	Ranking directors within each year by the number of movies they released
4.	Selecting the top-ranked director for each year.

### What is average duration of movies in each genre

1.	calculates the average duration of movies for each genre
2.	Joining the netflix and netflix_genre tables to associate each movie with its genre
3.	Filtering to include only movies
4.	Removing the ' min' suffix from the duration values, converting the numeric part to an integer.
5.	Calculating the average duration for each genre and grouping the results by genre

### Find the list of directors who have created horror and comedy movies both, and display director names along with number of comedy and horror movies directed by them.

1.	identifies directors who have created both horror and comedy movies and displays their names along with the number of comedy and horror movies they have directed
2.	Joining the netflix, netflix_genre, and netflix_directors tables.
3.	Filtering the results to include only movies and only the specified genres ('Comedies' and 'Horror Movies').
4.	Grouping the results by director and counting the number of movies in each genre.
5.	Filtering to include only those directors who have movies in both genres.

