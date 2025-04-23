# TLAB-Music-Recommendation


📘 README: 

# Project Title:

Audio Recommendation Algorithm - Basic Project

### 📂 Dataset Description

The dataset used in this project contains anonymized financial transaction records. Each row represents a single transaction, and the goal is to classify whether the transaction is fraudulent (1) or legitimate (0). Fraudulent transactions are rare, which introduces a significant class imbalance—a central challenge in this project.

Columns Overview
- artist_name: The name of the artist

- track_name: The name of the song

- release_date: When this song was released

- genre: The categorical genre of this song

- lyrics: The pre-tokenized lyrics of this song. Disclaimer: note that as this is real-world data, lyrical content is often obscene. 

- len:  The number of words in the lyrics of this song

- dating: A score from 0 to 1 expressing how likely it is that this song’s lyrics have something to do with dating.

- violence: A score from 0 to 1 expressing how likely it is that this song’s lyrics have something to do with violence.

- world/life: A score from 0 to 1 expressing how likely it is that this song’s lyrics have something to do with the world or life in general terms.

- night/time: A score from 0 to 1 expressing how likely it is that this song’s lyrics have something to do night-life or time.

- shake the audience: A score from 0 to 1 expressing how likely it is that this song’s lyrics have something to do with provocative feeling.

- family/gospel: A score from 0 to 1 expressing how likely it is that this song’s lyrics have something to do with family-oriented content or the gospel.

- romantic: A score from 0 to 1 expressing how likely it is that this song’s lyrics have something to do with romantic feeling.

- communication: A score from 0 to 1 expressing how likely it is that this song’s lyrics have something to do with communication (either in romantic terms or otherwise).

- obscene: A score from 0 to 1 expressing how likely it is that this song’s lyrics have something to do with obscene content (money, rockstar-lifestyle, etc).

- music: A score from 0 to 1 expressing how likely it is that this song’s lyrics have something to do with music (music about music, basically).

- movement/places: A score from 0 to 1 expressing how likely it is that this song’s lyrics have something to do with movement or various locations.

- light/visual perceptions: A score from 0 to 1 expressing how likely it is that this song’s lyrics have something to do with the sun or other physical weather-related patterns.

- family/spiritual: A score from 0 to 1 expressing how likely it is that this song’s lyrics have something to do with the importance of 
family or spirituality.


- sadness: A score from 0 to 1 expressing how likely it is that this song’s lyrics have something to do with the importance of family or spirituality.

- feelings: A score from 0 to 1 expressing how likely it is that this song’s lyrics have something to do with emotions, either positive or negative.

- topic: The categorical label of lyrical content

- age: A score from 0 to 1 expressing how “old” a song is from our perspective. 1 being the oldest, and 0 being the newest.

### Project Goals

- Perform EDA
- Data cleaning
- Model training and evaluation.

### Exploratory Data Analysis (EDA)

EDA Insists

- Most of the features like violence, sadness, and obscene are heavily right-skewed, meaning the majority of songs have low values for these traits.

- There’s a clear imbalance in genres and topics pop and country appear the most, and topics like sadness and violence are more frequent.

- The correlation heatmap shows that features don’t really overlap much, which is good because it means each one is adding something unique to the data.

- The 3D scatter of violence, communication, and sadness shows a lot of overlap across genres, so these features alone don’t clearly separate songs into groups.

- When it comes to preparing the data for KMeans, the skewness and outliers mean I definitely need to scale everything to give features equal weight. And while PCA won’t help the model directly, it’s still useful for visualizing how the clusters look after training.


### Data Cleaning

To prepare the dataset for modeling. I removed all non-numerical columns such as artist_name, track_name, release_date, lyrics, genre, and topic. These columns were not directly usable in KMeans clustering, which requires numerical input. After filtering out these columns, I saved the remaining numerical features into a clean version of the dataset. 

### Model Training & Evaluation

I first ran KMeans without scaling to see the difference compared to using scaled data. There was a noticeable improvement after scaling—the clusters were much cleaner and more defined. I also used PCA for visualization after scaling, which helped show how the data was separated more clearly.


I used both the elbow method and silhouette scores to decide on the best value for K. Based on the highest silhouette score and a clear bend in the elbow plot, I chose K = 10 for my final model. This number gave me well-separated and stable clusters.


After scaling, I applied PCA to reduce the data to two dimensions, but only for visualization purposes. This helped me clearly see how the clusters were forming and how well-separated they were. I didn’t include PCA in the actual modeling pipeline—just used it to better understand the cluster layout.


Once I had the cluster labels, I added them back to the dataset. I looked at the mean feature values in each group to understand what made each cluster unique. This helped me give names to each cluster based on the top 4 most dominant features in each group.


### Tools & Libraries

🧪 Data Handling & Analysis:
pandas – for data manipulation, cleaning, and DataFrame operations

numpy – for numerical computations and array handling

📊 Data Visualization:
matplotlib – for plotting graphs like elbow plots, scatter plots, 3D plots

seaborn – for visualizations like heatmaps, histograms, and boxplots

🧠 Machine Learning:
sklearn.preprocessing.StandardScaler – for feature scaling

sklearn.decomposition.PCA – for dimensionality reduction (used for visualization)

sklearn.cluster.KMeans – for clustering the music dataset

sklearn.metrics.silhouette_score – to evaluate the quality of clusters

🔢 Statistical Tools:
scipy.stats (optional, if used for further stats tests or outlier treatment)