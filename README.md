# 🎬 Streaming Platform Genre Analysis

This project analyzes and visualizes genre distributions and trends across three major streaming platforms: **Netflix**, **Amazon Prime**, and **Disney Plus**. It includes genre normalization, cross-platform comparison, and a time-based trend analysis focused on Netflix.

---

## 📁 Data Sources

- `netflix_titles.csv`
- `amazon_prime_titles.csv`
- `disney_plus_titles.csv`

Each dataset was enriched with a `platform` column and then merged into a unified DataFrame for comparative analysis.

---

## ⚙️ Preprocessing Steps

1. **Standardization of Columns**  
   Columns like `listed_in`, `date_added`, and `release_year` were renamed and unified.

2. **Datetime Conversion**  
   `date_added` was converted to datetime, and a new column `year_added` was extracted.

3. **Genre Cleaning**  
   - Converted all genre strings to lowercase  
   - Removed international-specific genres (e.g., `"korean tv shows"`)  
   - Standardized similar genres (e.g., `"sci-fi"` → `"science fiction"`) using a genre mapping dictionary

4. **Rare Genre Handling**  
   Genres with fewer than 100 occurrences were grouped under the `"other"` label.

5. **Genre Explosion**  
   Multiple genres per title were split and exploded into individual rows for granular analysis.

---

## 📊 Visualizations

### 1. Genre Distribution by Platform

A grouped bar chart shows how each genre is distributed across the three platforms.  
Key insights:
- Netflix dominates in *documentary*, *dramas*, and *comedy*
- Disney Plus has a strong focus on *family* and *animation*
- Amazon Prime exhibits diverse, balanced genre coverage

### 2. Netflix Genre Trends Over Time

A stacked area chart visualizes how genre popularity evolved over the years (based on `year_added`).  
Findings:
- Increasing growth in *documentaries* and *comedies* since 2017  
- Rising interest in *thrillers* and *science fiction* between 2019–2020  
- Decline or stagnation in *romance* and *action* genres

---

## 🧠 Key Insights

- Genre offerings vary significantly across platforms, likely reflecting target demographics and brand identity.
- Netflix appears to shift content focus dynamically year over year.
- Grouping rare genres into `"other"` made major trends more interpretable.

---

## 🚀 Future Work

- Add IMDb or user ratings to enrich the genre impact analysis
- Extend temporal analysis to Amazon Prime and Disney Plus
- Use NLP techniques (e.g., sentiment analysis) on descriptions to identify genre tone

---

## 📌 Requirements

- Python 3.7+  
- pandas  
- seaborn  
- matplotlib  

---

## 📝 License

This project is released under the MIT License.
