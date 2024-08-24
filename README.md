Sentiment Analysis of Amazon Product Reviews

This script performs sentiment analysis on a dataset of reviews. It utilizes the `pandas` library for data manipulation, `TextBlob` for sentiment analysis, and `matplotlib` for visualization.

Dependencies
Ensure you have the following Python libraries installed:
- `pandas`
- `textblob`
- `matplotlib`

You can install the necessary libraries using pip:
```bash
pip install pandas textblob matplotlib
```

Script Overview

1. **Load the Dataset:**
   ```python
   df = pd.read_csv('path/to/your/reviews.csv')
   ```
   The dataset is loaded from a CSV file. Adjust the file path as needed.

2. **Inspect the Columns:**
   ```python
   print(df.columns)
   ```
   This line prints the column names in the dataset to identify the relevant columns for reviews.

3. **Clean the Reviews:**
   ```python
   def clean_review(text):
       text = text.lower()  # Convert to lowercase
       text = re.sub(r'http\S+|www\S+|https\S+', '', text, flags=re.MULTILINE)  # Remove URLs
       text = re.sub(r'\@\w+|\#', '', text)  # Remove mentions and hashtags
       text = re.sub(r'[^A-Za-z0-9\s]', '', text)  # Remove special characters
       return text
   df['Cleaned_Review'] = df['Review'].apply(clean_review)
   ```
   The `clean_review` function preprocesses the text by converting it to lowercase, removing URLs, mentions, hashtags, and special characters. The cleaned reviews are stored in a new column `Cleaned_Review`.

4. **Analyze Sentiment:**
   ```python
   def analyze_sentiment(text):
       analysis = TextBlob(text)
       if analysis.sentiment.polarity > 0:
           return 'Positive'
       elif analysis.sentiment.polarity == 0:
           return 'Neutral'
       else:
           return 'Negative'
   df['Sentiment'] = df['Cleaned_Review'].apply(analyze_sentiment)
   ```
   The `analyze_sentiment` function uses `TextBlob` to analyze the sentiment of each review. Reviews are classified as 'Positive', 'Neutral', or 'Negative' based on their sentiment polarity. The results are added to the `Sentiment` column.

5. **Display and Visualize Results:**
   ```python
   sentiment_counts = df['Sentiment'].value_counts()
   plt.figure(figsize=(10,6))
   sentiment_counts.plot(kind='bar', color=['green', 'blue', 'red'])
   plt.title('Sentiment Analysis of Amazon Product Reviews')
   plt.xlabel('Sentiment')
   plt.ylabel('Number of Reviews')
   plt.show()
   ```
   The sentiment counts are computed and visualized using a bar chart. The chart shows the number of reviews categorized as Positive, Neutral, or Negative.

Usage

1. Update the file path in the script to point to your CSV file containing Amazon product reviews.
2. Run the script to perform sentiment analysis and visualize the results.

---
