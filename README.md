# Paul-EDA
Learning Explanatory data analysis

1) Investigating netflix movies

# Importing pandas and matplotlib
import pandas as pd
import matplotlib.pyplot as plt

# Read in the Netflix CSV as a DataFrame
netflix_df = pd.read_csv("netflix_data.csv")

# -----------------------------------------
# 1. Filter the data for movies released in the 1990s
# -----------------------------------------

# Subset the data for movies only
netflix_movies = netflix_df[netflix_df["type"] == "Movie"]

# Filter the years between 1990 and 1999
nineties_movies = netflix_movies[(netflix_movies["release_year"] >= 1990) &
                                 (netflix_movies["release_year"] < 2000)]

# -----------------------------------------
# 2. Find the most frequent movie duration
# -----------------------------------------

# Plot histogram of durations
plt.hist(nineties_movies["duration"])
plt.xlabel("Duration")
plt.ylabel("Frequency")
plt.title("Distribution of Movie Durations (1990s)")
plt.show()

# Based on histogram, find the most frequent duration
duration = nineties_movies["duration"].mode()[0]

# -----------------------------------------
# 3. Count short action movies from the 1990s
# -----------------------------------------

# Filter for action movies
action_movies = nineties_movies[nineties_movies["genre"] == "Action"]

# Set counter
short_movie_count = 0

# Iterate through action movies
for label, row in action_movies.iterrows():
    if row["duration"] < 90:
        short_movie_count += 1

# Print results
print("Most frequent duration:", duration)
print("Number of short action movies (<90 mins):", short_movie_count)

