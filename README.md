# Notion : [here](https://reinvented-horse-6c7.notion.site/Enhancing-Hotel-Review-Search-Engines-fe7437036308427ca48671b864ed8a44?pvs=4)


# Enhancing Hotel Review Search Engines:

# Overview:

In this assessment, we aimed to enhance traditional search engines by moving beyond embedding-based search methods. We explored a dual approach that combines embedding-based search with Aspect-based Sentiment Analysis (ABSA) to improve search relevance and user satisfaction.

### 1. Collecting the Data:

The dataset used for this assessment is the **hotel_datasets** from Hugging Face. This dataset contains **5997 rows** and **14 columns** that provide comprehensive information about various hotels in five different cities worldwide.

### **Dataset Columns:**

- **hotel_name**
- **hotel_description**
- **review_title**
- **review_text**
- **rate**
- **tripdate**
- **hotel_url**
- **hotel_image**
- **price_range**
- **rating_value**
- **review_count**
- **street_address**
- **locality**
- **country**

![Screenshot 2024-08-09 170528.png](Enhancing%20Hotel%20Review%20Search%20Engines%20fe7437036308427ca48671b864ed8a44/Screenshot_2024-08-09_170528.png)

### **2. Search Approach**

### **2.1 Embedding-Based Search**

To perform an embedding-based search, we combined data from multiple columns:

- **hotel_name**
- **locality (city)**
- **review_text**

This merged data was stored in a new column called **"reviews_search."**

### **Data Preprocessing:**

- The data in the "reviews_search" column was cleaned to contain only letters and digits (0-9).
- The text was converted to lowercase.
- The resulting text was embedded using a suitable embedding model.
- The generated embeddings were saved in a new column called **"embeddings."**

![Screenshot 2024-08-09 170954.png](Enhancing%20Hotel%20Review%20Search%20Engines%20fe7437036308427ca48671b864ed8a44/Screenshot_2024-08-09_170954.png)

### **2.2 Aspect-Based Sentiment Analysis (ABSA)**

To expand beyond embedding-based search, we performed Aspect-based Sentiment Analysis (ABSA) on the **review_text** column.

### **Aspects Considered:**

1. Room
2. Service
3. Location
4. Staff
5. Food
6. Noise
7. Bed
8. View

We used the **nomic-ai/nomic-embed-text-v1.5** model to analyze the sentiments of the sentences in the reviews.

### **Functions Defined:**

1. **`extract_aspects(review, aspects)`**
    - Splits the review text into sentences.
    - Checks each sentence to see if it mentions any of the defined aspects.
    - Stores the aspect and the sentence as a tuple in a list called **`aspect_sentences`**.
2. **`analyze_sentiment(sentences)`**
    - Takes a list of aspect-sentence tuples.
    - Analyzes the sentiment of each sentence using the sentiment model.
    - Records the mentioned aspect, the sentence itself, the sentiment label (Positive or Negative), and the sentiment score.

Each review in the **review_text** column is processed to extract sentences related to the defined aspects, followed by sentiment analysis.

![Screenshot 2024-08-09 171043.png](Enhancing%20Hotel%20Review%20Search%20Engines%20fe7437036308427ca48671b864ed8a44/Screenshot_2024-08-09_171043.png)

### **3. Composite Scoring for Enhanced Search**

The search engine leverages a function named **`composite_score`** that integrates both embedding-based similarity and sentiment analysis results.

### **How It Works:**

- **Cosine Similarity:** Measures the similarity between the user's search query and the embeddings of the review content.
- **Sentiment Score:** Reflects the sentiment associated with predefined aspects, calculated based on predefined aspect weights.

The **`composite_score`** function averages these two scores, providing a balanced evaluation of content relevance and sentiment, which is then used to rank the search results.

![Screenshot 2024-08-09 173339.png](Enhancing%20Hotel%20Review%20Search%20Engines%20fe7437036308427ca48671b864ed8a44/Screenshot_2024-08-09_173339.png)

![Screenshot 2024-08-09 171906.png](Enhancing%20Hotel%20Review%20Search%20Engines%20fe7437036308427ca48671b864ed8a44/Screenshot_2024-08-09_171906.png)

### **4. Conclusion**

By combining embedding-based search with Aspect-based Sentiment Analysis, we have enhanced the search engine's ability to deliver more relevant and sentiment-aware results. This dual approach ensures that both the content's relevance and the user's emotional response to key aspects are considered, leading to improved user satisfaction.

# Notebook(Demo):

[Task2-Hotel Review Search Engines](https://colab.research.google.com/github/SARA3SAEED/Task2/blob/main/Task2.ipynb)

# Team member:

Sara Almutairi

Hadeel Alnasiri

Sarah Almohammedsaleh
