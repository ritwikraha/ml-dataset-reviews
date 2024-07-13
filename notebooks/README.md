# RecSys

## Introduction 

The RecTour 2024 Challenge presents a complex, multi-faceted problem that combines elements of personalization, review ranking, and multi-modal data analysis. 
It requires participants to develop sophisticated models that can effectively process and leverage a rich, diverse dataset to create a personalized review ranking system. 
The challenge's structure and evaluation method encourage the development of practical, implementable solutions that could have significant real-world impact in the travel and hospitality industry.

1. Challenge Focus:
   The challenge centers on ranking reviews for accommodations, which is crucial in influencing users' decision-making process when booking. This task goes beyond simple ranking methods like sorting by review scores or timestamps, aiming to create a more personalized and relevant review presentation system.

2. Problem Statement:
   The core task is to match given accommodations and users to their respective review IDs.
   This approach allows for a dynamic review display system that considers both the review content and the characteristics of the user and accommodation when a potential customer is browsing.

4. Dataset Structure:
   The dataset is comprehensive, containing 1.6 million reviews based on real, anonymized bookings. It's divided into three main components:
   a) Users file: Contains information about users and accommodation features.
   b) Review file: Holds detailed information about the reviews.
   c) Matches file: Provides true labels connecting `user_id`, `accommodation_id`, and `review_id` (positive examples only).


5. Feature Rich Data:
   The dataset includes a wide array of features, such as review content (positive and negative), guest scores, helpful votes, guest types, countries, accommodation details, and location characteristics. This rich feature set allows for complex modeling approaches that can leverage various aspects of the booking experience.

6. Evaluation Metric:
   The challenge uses Mean Reciprocal Rank at 10 (MRR@10) as the performance metric. This choice emphasizes the importance of ranking the most relevant reviews at the top of the list.

7. Submission Format:
   Participants must submit predictions in a specific format:
   - 12 columns: `accommodation_id`, `user_id`, and top 10 `review_ids`.
   - Reviews must be ranked according to the model's predictions.

8. Unique Aspects:
   a) Minimum Review Threshold: Each accommodation has at least 10 unique reviews, ensuring a baseline for comparison.
   b) Review Quality: Reviews are pre-filtered to ensure each contains at least 3 different topics, based on the Text2Topic paper. This ensures informative content.
   c) Negative Sampling: Participants are encouraged to create their own negative labels using the Matches file, adding an element of creativity and strategy to the modeling process.

9. Research Integration:
    The challenge incorporates recent research, specifically the Text2Topic paper for topic detection, showcasing its relevance to current trends in NLP and recommendation systems.

10. Real-World Application:
    This challenge closely mimics a real-world scenario in the travel industry, where personalizing review presentations can significantly impact user experience and booking decisions.

11. Complexity and Innovation:
    The challenge encourages participants to go beyond traditional ranking methods (like helpfulness votes) and address issues such as presentation bias, pushing for innovative solutions in review ranking and personalization.


## Data Exploration
- [ ] TODO - Fill This Later

This recommendation system implements a hybrid approach combining content-based filtering and collaborative filtering. Here's a breakdown of how it works:
## Algorithm 

1. Data Preprocessing:

  - Combines positive and negative reviews
  - Preprocesses text (lowercase, remove special characters, tokenize, remove stopwords)
  - Creates TF-IDF vectors for the reviews
 -  Normalizes numeric features (review_score, review_helpful_votes, room_nights)


2. Similarity Calculation:

  - Calculates cosine similarity between reviews based on TF-IDF vectors
  - Computes a weighted score for each review based on normalized features


3. Recommendation Function:

For each accommodation-user pair:

  - If the user has no reviews, it recommends based on the weighted score
  - If the user has reviews, it calculates the similarity between the user's average features and each review
  - Combines content-based (weighted score) and collaborative filtering (user similarity) scores
  - Sorts and selects the top 10 review IDs

Submission Generation:

Creates a DataFrame with accommodation_id, user_id, and the top 10 recommended review_ids
Saves the results to a CSV file named 'recommendation_submission.csv'

## Submission

The submission needs to meet the criteria

12 columns: `accommodation_id`, `user_id`, and 10 columns for the top recommended `review_ids`
Reviews are ranked according to the model's predictions
