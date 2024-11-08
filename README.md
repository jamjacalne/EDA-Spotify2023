# **Exploratory Data Analysis on Spotify 2023 Dataset**

## Overview of Dataset
**1. How many rows and columns does the dataset contain?**

When Python loads the .csv file, it declares a dataset with 953 rows and 24 columns.

**2. What are the data types of each column? Are there any missing values?**

The `.dtypes` attribute was used to extract the data types of each column.

## Basic Descriptive Statistics
**1. What are the mean, median, and standard deviation of the streams column?**

The mean, median, and standard deviation of the streams are 514137424.93907565, 290530915.0, 566856949.0388832 respectively. These are extracted using the pandas function `.mean`, `.median`, and `.std`.

**2. What is the distribution of released_year and artist_count? Are there any noticeable trends or outliers?**

To analyze the distribution of `released_year` and `artist_count`, the `.describe()` function is used on the DataFrame. This provides summary statistics such as mean, standard deviation, quartiles, and percentiles for the specified columns. To observe trends over time, the average (`.mean()`) of `artist_count` for each `released_year` is calculated, and `.plot()` is used to create a line graph of the average artist count by release year. The notable spike in artist count between the years 1960 and 1980 could indicate an outlier or a unique trend in that period, where more artists collaborated on certain tracks.

## Top Performers
**1. Which track has the highest number of streams? Display the top 5 most streamed tracks.**

The streams column was passed to the `.sort_value` function to extract the streams in order. Since this function sorts from lowest to highest (ascending) values, the `.tail` function was called. 

**2. Who are the top 5 most frequent artists based on the number of tracks in the dataset?**

The `.value_counts()` function was used to extract the frequency of each artist’s appearances in the dataset, ranking the artists with the most streamed songs.

## Temporal Trends
**1. Analyze the trends in the number of tracks released over time. Plot the number of tracks released per year.**

To analyze trends in track releases per year, a line plot was created using the matplotlib library, clearly visualizing the rise and fall of trends over time.

**2. Does the number of tracks released per month follow any noticeable patterns? Which month sees the most releases?**

Using the matplotlib library, a bar plot was created to analyze patterns in track releases per month. The plot shows spikes in January and May, making these the months with the most streamed tracks.

## Genre and Music Characteristics
**1. Examine the correlation between streams and musical attributes like bpm, danceability_%, and energy_%. Which attributes seem to influence streams the most?**

To analyze the correlation between streams and musical attributes, the correlation matrix is first calculated using the `.corr()` function on a DataFrame containing only streams and the relevant musical attributes. The correlation matrix is then visualized with `sns.heatmap` from Seaborn. By sorting the correlation values using `.sort_values()`, it is identified that danceability, with a correlation of -0.105457, has the highest absolute correlation with streams. However, this is a weak negative correlation, so it does not strongly influence streams. 

**2. Is there a correlation between danceability_% and energy_%? How about valence_% and acousticness_%?**

Using `.loc`, specific correlations between danceability_% and energy_%, and between valence_% and acousticness_% were accessed for further analysis..

## Platform Popularity
**1. How do the numbers of tracks in spotify_playlists, spotify_charts, and apple_playlists compare? Which platform seems to favor the most popular tracks?**

To better visualize the comparison between the number of tracks in Spotify playlists, Spotify charts, and Apple playlists, the `.plot` function from Matplotlib is used to create a bar chart. The total number of appearances for each platform is calculated directly from the relevant columns and used `.replace` to format the platform names by replacing underscores with spaces for readability. The results reveal that Spotify playlists have a significantly higher representation of tracks compared to Spotify charts and Apple playlists, suggesting that Spotify playlists may favor popular tracks more extensively.

## Advanced Analysis
**1. Based on the streams data, can you identify any patterns among tracks with the same key or mode (Major vs. Minor)?**

To analyze patterns between streams and tracks with the same key or mode, the average streams per key and mode are calculated by grouping the data by key and mode, then using the `.mean()` function on the streams column. To sort the average streams by key in descending order, `.sort_values(ascending=False)` is applied. This reveals that tracks with the key C# in a major mode tend to receive more streams than other keys and modes.

**2. Do certain genres or artists consistently appear in more playlists or charts? Perform an analysis to compare the most frequently appearing artists in playlists or charts.**

To calculate the total number of times each artist appears in Spotify playlists, Spotify charts, and Apple playlists, the data is first grouped by `artist(s)_name` and the `.sum(axis=1)` function is applied on the `in_spotify_playlists`, `in_spotify_charts`, and `in_apple_playlists` columns. This gives the (row-wise) total appearances for each artist across all platforms. The results are then sorted in descending order by applying `.sort_values(by='total_appearances', ascending=False)`. This reveals that the artists with the most appearances in playlists and charts are The Weeknd, Taylor Swift, Ed Sheeran, Harry Styles, and Eminem.
