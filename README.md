1. Import Libraries
We begin by importing the necessary libraries for data handling, API requests, concurrent processing, and machine learning. Key libraries include:

requests for making API calls.
pandas for data manipulation.
concurrent.futures for parallel processing.
nltk for natural language processing tasks.
sklearn for machine learning models and metrics.
xgboost for regression modeling.
sentence_transformers for generating text embeddings.
2. Fetch Movie Data
API Key: An API key is defined to access the TMDB API.
Fetch Movie Details: A function is created to fetch detailed information about movies using their IDs. This includes details like title, genres, synopsis, rating, and credits (cast and crew).
Fetch Data: Another function is defined to fetch popular movies from the TMDB API, iterating through multiple pages to collect data. The movie details are fetched concurrently using a thread pool for efficiency.
3. Data Preparation
Concatenation: The fetched movie data is combined into a single DataFrame.
Column Cleanup: Unnecessary columns are removed from the DataFrame to focus on relevant data.
4. Data Cleaning
A function is defined to preprocess the text data:

Convert text to lowercase.
Tokenize the text into words.
Remove stopwords and punctuation to clean the text for further analysis.
The cleaning function is applied to the synopsis column of the DataFrame.

5. Feature Engineering
Average Ratings: New columns are added to the DataFrame to calculate the average ratings for actors and directors based on their previous works.
Rating Categories: The movie ratings are categorized into bins (Low, Medium, High, Very High) for classification tasks.
6. Data Splitting
The cleaned and processed data is split into training and testing sets using train_test_split, with 20% of the data reserved for testing.

7. Feature Extraction
TF-IDF Vectorization: The synopsis text data is transformed into numerical format using the TF-IDF vectorizer, which quantifies the importance of words in the documents.
Sentence Embeddings: The synopsis is also converted into embeddings using the SentenceTransformer model for better representation in the feature space.
8. Model Training and Evaluation
8.1 XGBoost Regressor
An XGBoost model is instantiated and trained on the combined features (embeddings, genres, average ratings).
Predictions are made on the test set, and performance metrics such as R² score and Mean Squared Error (MSE) are calculated.
8.2 Logistic Regression
A Logistic Regression model is trained on the TF-IDF features.
Predictions are made, and the accuracy and classification report are printed.
8.3 Naive Bayes
A Multinomial Naive Bayes model is trained on the TF-IDF features.
Predictions are made, and the accuracy and classification report are printed.
8.4 Support Vector Classifier (SVC)
An SVC model is trained on the TF-IDF features.
Predictions are made, and the accuracy and classification report are printed.
9. Saving Models
Finally, all trained models and relevant data (like genre columns and average ratings) are saved to disk using pickle for future use.
