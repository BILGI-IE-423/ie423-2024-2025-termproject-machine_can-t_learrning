# Movie Platform Availability Prediction

## Abstract
This project investigates factors influencing whether movies and TV shows become available on popular streaming platforms such as Netflix, Amazon Prime, and Disney+. By analyzing attributes like IMDb ratings, genres, release year, and descriptions, we aim to predict platform availability.

We collected relevant datasets from IMDb and individual streaming platforms, applied extensive preprocessing, and performed exploratory data analysis to uncover significant patterns and trends. Using this enriched and processed dataset, we are developing machine learning models to predict content availability and to identify which characteristics most influence a streaming platform’s decision-making.

This predictive analysis can offer valuable insights for content selection strategies, enhance user recommendations, and help understand viewer preferences.

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

### Genre Distribution
The first chart shows the frequency of genres across the entire dataset. The most common genres are Drama, Comedy, and Action, which make up the majority of titles. Less represented genres include Biography, Sci-Fi, and Documentary.

*The chart reveals an imbalanced dataset, with certain genres (e.g., Drama) dominating the distribution. This imbalance will be taken into account during model training to avoid biased predictions.*

<h4>Genre Distribution Graph</h4>
<img src="https://github.com/user-attachments/assets/b29c6e46-f07b-4707-a030-b3b2a4c1dedb" width="800"/>

### Availability Across Platforms
The second chart compares the number of titles that are available on at least one of the platforms (Netflix, Amazon Prime, or Disney+) versus those that are not. A large portion of the content is not available on these major platforms, highlighting the selective nature of streaming content acquisition.

<h4>Availability Across Platforms Graph</h4>
<img src="https://github.com/user-attachments/assets/ede50fdb-7626-499d-842e-2ca52f9b6fd1" width="700"/>

## Rating Distribution Heatmaps

### Top 15 Genres vs Rating Bins
This heatmap shows how different genres are distributed across IMDb rating intervals. For example, biography and drama films tend to be concentrated in the mid-to-high rating bins (e.g., 6.0–7.5), while genres like horror and thriller have a wider spread across lower ratings. The normalization helps to compare genres of varying overall frequencies on an equal scale

<h4>Genres vs Rating</h4>
<img src="https://github.com/user-attachments/assets/6858a4bd-cd85-4ae1-90ab-a05d751c9796" width="700"/>

### Release Year vs Rating Bins (Last 15 Years)
This heatmap visualizes how IMDb ratings have been distributed over the last 15 years. A clear concentration appears between 6.0 and 7.5 ratings, consistent across years. More recent years such as 2021–2022 also follow the same trend, indicating that rating patterns have remained relatively stable over time.

<h4>Release Year vs Rating</h4>
<img src="https://github.com/user-attachments/assets/17061d45-c0fa-440f-bf81-41febe09ec76" width="700"/>

### Rating vs Votes Heatmap
This heatmap shows how user votes are distributed across rating intervals. Lower-rated titles (around 1.0–4.0) are mostly clustered in the 100–1K vote range, indicating less visibility or niche audiences. Higher-rated titles (7.0+) begin to spread into higher vote bins, especially 1K–10K and beyond, which suggests broader popularity and user engagement.

<h4>Rating vs Votes</h4>
<img src="https://github.com/user-attachments/assets/58a3da2f-bd27-4620-a672-becfa352ba06" width="700"/>

### Rating vs Duration Heatmap
This heatmap illustrates how movie durations relate to IMDb ratings. Films between 60–120 minutes dominate most rating bins, especially mid-range ratings like 5.0–7.0. Interestingly, the highest-rated titles (9.0+) show more variability in duration, including both very short and very long formats.

<h4>Rating vs Duration</h4>
<img src="https://github.com/user-attachments/assets/f3abef26-29c1-4237-b17d-e06eea9d5026" width="700"/>


## Model Tranings

### Text Feature Extraction with TF-IDF
To incorporate textual information from the description field, we applied TF-IDF (Term Frequency–Inverse Document Frequency) vectorization. This technique transforms raw text into numerical features by evaluating how important each word is within a document relative to the entire corpus. We limited the number of features to the top 1,000 most informative terms (max_features=1000) and removed common English stop words (stop_words="english"). This approach helps reduce dimensionality and noise, allowing the model to focus on meaningful keywords that may contribute to distinguishing platform availability.


### Logistic Regression with Default Threshold (0.5)

We trained a Logistic Regression model to predict whether a movie is available on a streaming platform (platform_flag = 1) based on its metadata. The feature set included:

Text features (TF-IDF of the description),

Numerical features (duration, year, votes, rating),

Categorical encoding of movie type,

Binary genre flags (e.g., genre_action, genre_drama).

The model was trained with class_weight='balanced' to compensate for the imbalance between platform and non-platform classes.

Performance at Threshold = 0.5:
Accuracy: 77.02%

Precision (class 1): 33.00%

Recall (class 1): 61.99%

F1 Score (class 1): 42.76%

![image](https://github.com/user-attachments/assets/61d1c21b-82f4-4b9e-a86a-a6ebf39e8f70)


![image](https://github.com/user-attachments/assets/c95ef39e-f6f9-45f5-a606-07e87ec64c2c)




This output shows that while the model is fairly good at identifying movies not available on platforms, it sacrifices precision in identifying those that are. The high number of false positives for class 1 (3,054) indicates that many movies were incorrectly predicted as being on a platform.



### Logistic Regression with Tuned Threshold (0.6)

To improve the balance between precision and recall, we adjusted the classification threshold from the default 0.5 to 0.6. This means the model now requires a higher predicted probability to label a movie as available on a platform (platform_flag = 1).

Performance at Threshold = 0.6:
Accuracy: 84.13%

Precision (class 1): 44.19%

Recall (class 1): 50.19%

F1 Score (class 1): 47.00%


![image](https://github.com/user-attachments/assets/dcee3949-9b5d-44b4-b020-2d29ee68b8d5)


By increasing the threshold:

Precision improved from 33% to 44%, meaning fewer false positives.

Recall decreased slightly but stayed reasonable, capturing over half of the actual platform movies.

Overall, F1-score increased, indicating a better trade-off between precision and recall for the minority class.

This threshold tuning step highlights the importance of going beyond default settings, especially in imbalanced classification problems like this one.

#### Trade-off Between Precision and Recall with Threshold Adjustment
When we increased the classification threshold from 0.5 to 0.6, we observed a slight improvement in overall accuracy. However, this came at a cost, especially for the minority class (class 1) — which represents titles available on at least one platform.

While the model became more conservative (less likely to predict class 1), it also missed more actual positives, meaning more titles that were actually available were wrongly predicted as unavailable. This is evident in the drop in recall for class 1, even though precision slightly improved.

In other words, the model got "better" at being sure when it predicted availability, but it missed more available titles in the process.

### Support Vector Machine (SVM) with Linear Kernel (C = 1)

In this stage of our project, we trained a Support Vector Machine (SVM) using LinearSVC to predict whether a movie is available on a specific platform. The model uses a linear kernel, making it suitable for large, sparse datasets, especially when working with high-dimensional representations like TF-IDF features.

To address the class imbalance problem, where class 0 (not available on platform) is far more frequent than class 1, we used class_weight="balanced", which assigns higher weight to the minority class during training.

The regularization parameter C was set to 1, allowing the model to balance bias and variance effectively.

After training on 80% of the data and testing on the remaining 20%, the model achieved:

Accuracy: 77.37%

Precision for class 1: 33%

Recall for class 1: 62%

F1-score for class 1: 43%

![image](https://github.com/user-attachments/assets/ff51d2b2-63a5-4734-9eb8-6ca5ee10b198)

This result shows that the model is reasonably effective at identifying platform-available titles (class 1) but still struggles with precision due to class imbalance and feature overlap. The confusion matrix further shows that while true positives improved, false positives remain a challenge  a common issue in imbalanced binary classification.

### Linear SVC (C = 0.1) — Improving Minority Class Performance
In this iteration, we reduced the regularization parameter C from 1 to 0.1 while keeping class_weight="balanced" in our Linear Support Vector Classifier. Lowering C increases regularization, encouraging the model to prioritize generalization over fitting specific training points — this is especially helpful when dealing with imbalanced datasets, as it can shift the decision boundary to better capture the minority class (platform availability = 1).

After training and testing, the model achieved:

Accuracy: 88.18%

Precision (class 1): 58%

Recall (class 1): 60%

F1-score (class 1): 59%

This marks a significant improvement in recall and precision for the minority class compared to the previous SVC model with C = 1. The confusion matrix shows:

1448 true positives (class 1 correctly identified),

979 false negatives (class 1 missed),
 
A decrease in false positives, improving reliability.

![image](https://github.com/user-attachments/assets/d7c8431a-d484-4880-a9cd-8587376a4d45)


This performance demonstrates that stronger regularization (lower C) can help in recovering more true positives for underrepresented classes, leading to better balance in classification metrics. It's a promising tradeoff, especially when recall is prioritized over precision, such as in recommendation systems or content discovery.

### XGBoost Classifier 

In this experiment, we used an XGBoost classifier trained on a comprehensive feature set including TF-IDF vectors from movie descriptions, numerical attributes (e.g., duration, year), categorical data (e.g., type), and genre indicators. Given the imbalance in the target classes (with significantly more class 0 examples), we addressed this by setting the scale_pos_weight parameter to reflect the class ratio. This helps the model better account for the underrepresented class during training.

To support generalization and stable learning, we selected the following parameters:

A maximum depth of 3, which helps control the complexity of individual trees,

200 estimators, allowing the model to learn patterns over multiple boosting rounds,

A learning rate of 0.1, which helps the model update weights more gradually during training.

Results:
Accuracy: 80.18%

Precision (class 1): 38%

Recall (class 1): 68%

F1-score (class 1): 49%

The model demonstrates a strong ability to capture true positives, as reflected by the improved recall score. This makes it particularly useful in scenarios where identifying as many available titles as possible is more important than minimizing false positives.

![image](https://github.com/user-attachments/assets/4ed01255-5deb-4800-aced-a66d5f7fc9f2)

This configuration of XGBoost provides a reasonable trade-off between precision and recall. It performs well in identifying platform availability and shows potential for practical applications.

## Conclusion: Streaming the Unseen

In today’s crowded digital landscape, not every movie ends up on your favorite streaming platform. Some titles appear everywhere Netflix, Prime, Disney+ while others remain mysteriously absent. We set out to uncover the patterns behind this digital availability, combining data science with a bit of storytelling.

We began by collecting and cleaning a large dataset of movies and TV shows. With features like IMDb rating, genre, description, year, and duration, we captured both the quantitative essence of a title and its creative identity. These were merged with availability information across three major platforms, turning our dataset into a lens through which we could explore streaming patterns.

To predict whether a movie is streamable or not, we built and evaluated three machine learning models: Logistic Regression, Support Vector Machines (SVM), and XGBoost.

Logistic Regression offered a transparent and interpretable baseline. After tuning the classification threshold, it provided solid overall accuracy (~84%) but struggled with the minority class predicting which titles are available.

SVM, especially with a lower regularization parameter (C=0.1), performed better in balancing both precision and recall. It achieved higher accuracy and improved recognition of available titles, showing that margin-based classifiers can be effective even with high-dimensional feature spaces.

XGBoost emerged as a strong contender. With thoughtful feature engineering and class balancing, it delivered the best performance in terms of identifying available content achieving a promising blend of recall and precision for the positive class. Its ability to model non-linear interactions gave it an edge in capturing subtle patterns that linear models may miss.

Each model taught us something valuable not just about algorithmic performance, but about the underlying nature of content selection across platforms. By transforming textual descriptions with TF-IDF, encoding genre patterns, and balancing class distributions, we saw how both technical and narrative elements influence streaming availability.

In the end, this project goes beyond prediction. It reveals part of the hidden decision-making behind what we see when we open a streaming app. And while not every movie finds its way onto a platform, through data and models, we’ve begun to understand why.







## Contributors
Yiğit Can Kınalı - 122203103

Poyraz Esin - 121203089

Eren Cem Beker - 120203070

Mehmet Fatih Çetinkaya - 121205031




