# **Exploratory Data Analysis on Spotify 2023 Dataset**
The code uses `Pandas` to handle and manipulate data, displaying rows and columns, and `Matplotlib` and `Seaborn` to create plots and graphs that help illustrate trends and distributions in the data for visualization.

## Overview of Dataset
**1. Rows and columns of the dataset**

When Python loads the .csv file (using the `.read_csv` function), it declares a dataset with 953 rows and 24 columns.

**2. Data types of each column**

The `.dtypes` attribute was used to extract the data types of each column.

## Basic Descriptive Statistics
**1. Mean, median, and standard deviation of the streams column**

The mean, median, and standard deviation of the streams are 514137424.93907565, 290530915.0, 566856949.0388832 respectively. These are extracted using the pandas function `.mean`, `.median`, and `.std`.

**2. Distribution of `released_year` and `artist_count`**

To analyze the distribution of `released_year` and `artist_count`, the `.describe()` function is used on the DataFrame. This provides summary statistics such as mean, standard deviation, quartiles, and percentiles for the specified columns. To observe trends over time, the average (`.mean()`) of `artist_count` for each `released_year` is calculated, and `.plot()` is used to create a line graph of the average artist count by release year. The notable spike in artist count between the years 1960 and 1980 could indicate an outlier or a unique trend in that period, where more artists collaborated on certain tracks.

## Top Performers
**1. Top 5 most streamed tracks**

The streams column was passed to the `.sort_value` function to extract the streams in order. Since this function sorts from lowest to highest (ascending) values, the `.tail` function was called. This reveals Dance Monkey by Tones and I, Someone You Loved by Lewis Capaldi, Shape of You by, Blinding Lights by The Weeknd, and Love Grows (Where My Rosemary Goes) by Edison Lighthouse to be the Top 5 most streamed tracks.

**2. Top 5 most frequent artists based on the number of tracks**

The `.value_counts()` function was used to extract the frequency of each artist’s appearances in the dataset, ranking the artists with the most streamed songs. This reveals artists Taylor Swift, The Weeknd, Bad Bunny, SZA, and Harry Styles to have the most number of most streamed tracks in the dataset.

## Temporal Trends
**1. Number of tracks released per year**

To analyze trends in track releases per year, a line plot was created using the matplotlib library, clearly visualizing the rise and fall of trends over time. The line graph shows that the number of tracks released per year has increased significantly in recent years, with a sharp spike near the end of the timeline. This trend suggests that music production has increased over time, especially in the most recent years shown.

**2. Number of tracks released per month**

Using the Matplotlib library, a bar plot was created to analyze patterns in track releases per month. The plot shows spikes in January and May, indicating that these are the months with the highest number of track releases.

## Genre and Music Characteristics
**1. Correlation between streams and musical attributes (`bpm`, `danceability_%`, and `energy_%`)**

To analyze the correlation between streams and musical attributes, the correlation matrix is first calculated using the `.corr()` function on a DataFrame containing only streams and the relevant musical attributes. The correlation matrix is then visualized with `sns.heatmap` from Seaborn. By sorting the correlation values using `.sort_values()`, it is identified that danceability, with a correlation of -0.105457, has the highest absolute correlation with streams. However, this is a weak negative correlation, so it does not strongly influence streams. 

**2. Correlation between `danceability_%` and `energy_%`, and `valence_%` and `acousticness_%`**

Using `.loc`, specific correlations between danceability_% and energy_%, and between valence_% and acousticness_% were accessed for further analysis.

## Platform Popularity
**1. Comparison between the numbers of tracks in `spotify_playlists`, `spotify_charts`, and `apple_playlists`**

To better visualize the comparison between the number of tracks in Spotify playlists, Spotify charts, and Apple playlists, the `.plot` function from Matplotlib is used to create a bar chart. The total number of appearances for each platform is calculated directly from the relevant columns and used `.replace` to format the platform names by replacing underscores with spaces for readability. The results reveal that Spotify playlists have a significantly higher representation of tracks compared to Spotify charts and Apple playlists, suggesting that Spotify playlists may favor popular tracks more extensively.

## Advanced Analysis
**1. Patterns among tracks with the same key or mode (Major vs. Minor)**

To analyze patterns between streams and tracks with the same key or mode, the average streams per key and mode are calculated by grouping the data by key and mode, then using the `.mean()` function on the streams column. To sort the average streams by key in descending order, `.sort_values(ascending=False)` is applied. This reveals that tracks with the key C# in a major mode tend to receive more streams than other keys and modes.

**2. Most frequently appearing artists in playlists or charts**

To calculate the total number of times each artist appears in Spotify playlists, Spotify charts, and Apple playlists, the data is first grouped by `artist(s)_name` and the `.sum(axis=1)` function is applied on the `in_spotify_playlists`, `in_spotify_charts`, and `in_apple_playlists` columns. This gives the (row-wise) total appearances for each artist across all platforms. The results are then sorted in descending order by applying `.sort_values(by='total_appearances', ascending=False)`. This reveals that the artists with the most appearances in playlists and charts are The Weeknd, Taylor Swift, Ed Sheeran, Harry Styles, and Eminem.
