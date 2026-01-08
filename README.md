# UCI-ML-Drug-Review-Cluster-Analysis

### Project Overview

This project aims to analyze a dataset of drug reviews to understand patient experiences, drug efficacy, and potential side effects. By leveraging natural language processing (NLP) techniques, we can extract valuable insights from unstructured text data.

### Technologies Used

  * Google Colab
  * Python
  * pandas (for data manipulation)
  * matplotlib, seaborn (for visualizations)
  * zipfile (for extracting data)
  * scikit-learn (for preprocessing, dimensionality reduction, and clustering)
  * Hugging face transformer library (for natural language processing)

### Methodology
  1. Data Loading
      * The initial step involves loading the drug review dataset from a ZIP file and then reading the `drugsComTrain_raw.csv` into a pandas DataFrame.

  2.  Data Sanity Check
      * Checked the shape and information of the DataFrame.
      * Identified missing values and their percentages.
      * Checked for duplicate entries.
      * Identified potential garbage values in categorical columns.

  3. Exploratory Data Analysis (EDA)
      * Visualizing distributions (histograms, box plots), relationships (scatter plots), and correlations (heatmap).

  4. Missing Value Treatments
      * Filled missing values in the 'condition' column with the mode.

  5. Garbage Value Treatment
      * Identified and removed rows containing 'garbage' conditions (e.g., 'users found this comment helpful').
      *  Cleaned the 'review' column by replacing HTML entities like `&#039;` with apostrophes.

  6. Data Stratification
    - Due to hardware limitation (takes long time to process every data) stratified sampling was performed to create a reduced but balanced subset of the data. A sample of 10,000 rows was created.


  7. Sentiment Analysis
      * Utilized a pre-trained `cardiffnlp/twitter-roberta-base-sentiment` model from the `transformers` library to classify the sentiment of each drug review (LABEL_0: negative, LABEL_1: neutral, LABEL_2: positive).
      * Added new columns `sentiment_label` and `sentiment_score` to the DataFrame.
        
     <ul>
       <br>
       <img width="859" height="547" alt="Sentiment Labels per Cluster" src="https://github.com/user-attachments/assets/b124679c-48d5-4007-8370-610097be9114" />
     </ul>

  9. Zero Shot Classification
      * Employed a `facebook/bart-large-mnli` model for zero-shot classification to categorize reviews into specific topics such as 'Effective', 'Bad reaction', 'Life saving', etc.
      * Added a new column `topic` to the DataFrame.

  10. Preprocessing
      * Dropped irrelevant columns such as 'uniqueID', 'review', 'date', and 'usefulCount'.
      * Separated numerical and categorical columns for preprocessing.
      * Applied `StandardScaler` to numerical columns and `OneHotEncoder` to categorical columns using `ColumnTransformer`.

  11. Dimensionality Reduction
      * Applied Principal Component Analysis (PCA) with 2 components to reduce the dimensionality of the preprocessed data for visualization and clustering purposes.
      * Visualized the PCA-transformed data in a scatter plot.

  12. K-Means Clustering
      * Performed K-Means clustering on the PCA-transformed data to group similar drug reviews.
      * Initialized K-Means with 3 clusters and visualized the clusters.
    
      <ul>
       <br>
       <img width="457" height="624" alt="Kmeans" src="https://github.com/user-attachments/assets/03f5e9ce-af63-49ee-b54d-e89b463560b7" />
      </ul>
     
  13. Elbow Method
      * Used the elbow method to determine the optimal number of clusters for K-Means, by plotting the inertia score against the number of clusters.

  14. Integrated Interpretation (conditions + sentiment + topics)
      
      * Assigned the cluster labels back to the DataFrame.
      * Conducted exploratory data analysis per cluster to understand the characteristics of each group:
      
            Distribution of sentiment labels per cluster.
            Top drugs in each cluster.
            Distribution of topics per cluster.
            Top conditions in each cluster.
          
  ### Results and Conclusion

  For a quicker cluster comparison, ChatGPT was used to do a quick analysis based on the top 30 conditions in each cluster, and a detailed interpretation was provided:

  
  Cluster 0 — Neutral / Management-Oriented.
  
      Chronic mental health
      Chronic pain
      Women’s health
      Long-term condition management

  Cluster 0 reflects stable, long-term condition management characterized by predominantly neutral sentiment, suggesting routine and informational healthcare interactions.
  Users are engaged but not emotionally extreme — typical of maintenance care, refills, monitoring, and follow-ups.

  Cluster 1 — Negative / Acute Care
  
      Infections (UTI, sinusitis, bacterial)
      GI distress
      Episodic conditions

  Cluster 1 is characterized by acute and infection-related conditions accompanied by predominantly negative sentiment, indicating care-seeking behavior driven by discomfort and immediate symptom burden.
  Negative sentiment aligns with pain, urgency, and disruption, reinforcing the acute-care nature of this cluster.

  Cluster 2 — Positive / Preventive & Lifestyle

      Smoking cessation
      Weight loss
      Opiate dependence recovery
      Preventive and allergy care

  Cluster 2 is distinguished by predominantly positive sentiment, consistent with conditions associated with lifestyle improvement, preventive care, and behavioral change.
  Positive sentiment suggests perceived progress, success, or motivation, common in lifestyle change and recovery contexts.
      
      
      
