# Movie Platform Availability Prediction

## Scope of the Project
Imagine opening Netflix on a Friday night, scrolling through Amazon Prime on Saturday, and dipping into Disney+ on Sunday. Some films follow you everywhere, while others seem to vanish from one service and reappear on another. Why?

Our project follows each film on its journey. We start with basic facts: its IMDb rating, release year, genre, content type, and watch where it ends up: Netflix, Amazon Prime, Disney+, or nowhere at all.
We want to see if a movie’s good reviews or its well-known director and actors help it land on the big streaming shelves. Is a high IMDb score a golden ticket? Do certain genres or release years get picked first? Or are there other reasons we don’t yet, see?
By the end, we want to explain how movies move from initial release to streaming menus and why some always show up while others never do.

## Research Question
Are movies with high IMDb ratings and notable attributes, such as content type, year, description and genre, more likely to be available on Netflix, Amazon Prime, or Disney+?

## Preprocessing Steps
Our preprocessing was divided into three main parts: cleaning the IMDb dataset, preparing the platform datasets (Netflix, Amazon Prime, and Disney+), and finally merging everything into a single, enriched dataset for analysis.

## 1. IMDb Dataset Preparation
### Combining movies and series:

We began by loading two separate IMDb datasets one for movies and one for TV series. To unify them, we standardized the rating column and added a new type column to distinguish between "movie" and "tv show".

### Text cleaning:

We cleaned text-based columns such as title, genre, and description by converting them to lowercase, removing punctuation, and trimming extra spaces. This ensured consistent formatting for later merging with platform datasets.

### Standardizing year, votes, and duration:

The year column was extracted and converted to integers. The votes and duration columns were cleaned (e.g., removing characters like "min" or commas) and converted to numeric types.

### Genre one-hot encoding:

Each genre was split and transformed into separate binary columns (e.g., genre_comedy, genre_drama) to represent multi-genre entries. This allows genre information to be used directly in machine learning models.

## 2. Platform Dataset Preparation

### Loading and labeling:

We loaded the Netflix, Amazon, and Disney+ datasets, and added a new column to each indicating its source platform.

### Column harmonization:

To match the IMDb dataset, we normalized columns such as type and listed_in, and renamed listed_in to genre and release_year to year. Unnecessary columns (e.g., show_id, director, cast) were dropped.

### Title standardization:

All titles were converted to lowercase and stripped of punctuation and extra spaces to ensure consistency with IMDb titles during merging.

## 3. Merging IMDb with Platform Data

### Combining platform availability:

Using the cleaned titles, we grouped and merged the platform data into the IMDb dataset, adding a column that shows which platforms each title is available on (e.g., "netflix, amazon").

### Binary availability label:

A new column, platform_flag, was created to indicate whether a title is available on at least one of the three platforms (1) or not (0). The full platform names were kept in a separate column.

### TF-IDF transformation:

We applied TF-IDF vectorization to the description column to turn it into numerical features, using the top 500 most relevant words after filtering English stopwords. This was done for use in future modeling steps.

### Final cleaning:

Rows with missing or empty values in key columns such as description, rating, and duration were removed. This resulted in a clean, ready to  use dataset for building machine learning models.

## Content Distribution Insights
#### Genre Distribution
The first chart shows the frequency of genres across the entire dataset. The most common genres are Drama, Comedy, and Action, which make up the majority of titles. Less represented genres include Biography, Sci-Fi, and Documentary.

<h4>Genre Distribution</h4>
<img src="https://github.com/user-attachments/assets/ede50fdb-7626-499d-842e-2ca52f9b6fd1" width="600"/>

#### Availability Across Platforms
The second chart compares the number of titles that are available on at least one of the platforms (Netflix, Amazon Prime, or Disney+) versus those that are not. A large portion of the content is not available on these major platforms, highlighting the selective nature of streaming content acquisition.

<h4>Availability Across Platforms</h4>
<img src="https://github.com/user-attachments/assets/b29c6e46-f07b-4707-a030-b3b2a4c1dedb" width="600"/>


