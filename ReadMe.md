# Netflix Movie Duration Analysis

![Netflix](https://assets.datacamp.com/production/project_1237/img/netflix.jpg)

In this project, we explore the trend of movie durations on Netflix over the years. We start by analyzing aggregated data provided by a friend and then move on to a more comprehensive analysis using a dataset obtained from a CSV file.

## 1. Loading Your Friend's Data into a Dictionary
We begin by creating a dictionary containing movie durations for the years 2011 to 2020, provided by our friend.

```python
# Create the years and durations lists
years = [2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020]
durations = [103, 101, 99, 100, 100, 95, 95, 96, 93, 90]

# Create a dictionary with the two lists
movie_dict = {"years": years, "durations": durations}
```

## 2. Creating a DataFrame from a Dictionary
We convert the dictionary into a pandas DataFrame for further analysis.

```python
# Import pandas under its usual alias
import pandas as pd

# Create a DataFrame from the dictionary
durations_df = pd.DataFrame(movie_dict)
```

## 3. A Visual Inspection of Our Data
We visualize the movie durations over the years using a line plot.

```python
# Import matplotlib.pyplot under its usual alias and create a figure
import matplotlib.pyplot as plt
fig = plt.figure()

# Draw a line plot of years and durations
plt.plot(durations_df["years"], durations_df["durations"])

# Create a title
plt.title("Netflix Movie Durations 2011-2020")

# Show the plot
plt.show()
```

## 4. Loading the Rest of the Data from a CSV
We load the complete Netflix dataset from a CSV file and filter for movie entries only.

```python
# Read in the CSV as a DataFrame
netflix_df = pd.read_csv("datasets/netflix_data.csv")

# Filter for type "Movie" and select relevant columns
netflix_df_movies_only = netflix_df[netflix_df["type"]=="Movie"]
netflix_movies_col_subset = netflix_df_movies_only[["title", "country", "genre", "release_year", "duration"]]
```

## 5. Filtering for Movies!
We filter the dataset for movies with durations less than 60 minutes.

```python
# Filter for durations shorter than 60 minutes
short_movies = netflix_movies_col_subset[netflix_movies_col_subset["duration"] < 60]
```

## 6. Creating a Scatter Plot
We create a scatter plot to visualize movie durations over the years.

```python
# Create a figure and increase the figure size
fig = plt.figure(figsize=(12,8))

# Create a scatter plot of duration versus year
plt.scatter(netflix_movies_col_subset["release_year"], netflix_movies_col_subset["duration"])

# Create a title
plt.title("Movie Duration by Year of Release")

# Show the plot
plt.show()
```

## 7. Digging Deeper
We analyze shorter movies to understand their impact on the overall trend.

```python
# Print the first 20 rows of short_movies
print(short_movies.head(20))
```

## 8. Marking Non-Feature Films
We mark non-feature films with different colors in the scatter plot.

```python
# Define colors based on genre
colors = []
for lab, row in netflix_movies_col_subset.iterrows():
    if row["genre"] == "Children":
        colors.append("red")
    elif row["genre"] == "Documentaries":
        colors.append("blue")
    elif row["genre"] == "Stand-up":
        colors.append("green")
    else:
        colors.append("black")
```

## 9. Plotting with Color!
We create a scatter plot with colors representing different genres.

```python
# Set the figure style and initalize a new figure
plt.style.use('fivethirtyeight')
fig = plt.figure(figsize=(12,8))

# Create a scatter plot of duration versus release_year with color coding
plt.scatter(netflix_movies_col_subset["release_year"], netflix_movies_col_subset["duration"], color=colors)

# Create a title and axis labels
plt.title("Movie Duration by Year of Release")
plt.xlabel("Release Year")
plt.ylabel("Duration (min)")

# Show the plot
plt.show()
```

## 10. What Next?
We conclude the analysis by reflecting on the insights gained and suggesting further avenues for exploration.

---

This project provides a glimpse into the trends of movie durations on Netflix and demonstrates the application of Python programming skills in data analysis and visualization. Further analysis could involve exploring the impact of genres, regional preferences, and production trends on movie durations.
