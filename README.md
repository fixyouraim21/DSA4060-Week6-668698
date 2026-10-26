# DSA4060XA – Week 6: Evaluating Recommender Systems

**Name:** Amy Njenga
**Student ID:** 668698

## Lab Objective

The goal of this lab was to build three simple movie recommenders and compare them properly. I used a train/test split where each user's most recent rating is held out for testing. I then checked how well each model predicts ratings and how good its Top-3 recommendation list is.

## Dataset

- 12 users, 20 movies, 120 ratings (scale 1–5)
- Most common rating is 3. Only about 35% of ratings are 4 or 5.
- A held-out movie counts as "relevant" if its rating is 4 or 5.

## Models Compared

1. **Popularity Baseline:** predicts each movie's average training rating and recommends the highest rated movies.
2. **Content-Based:** builds a user profile from genres and recommends movies that match it.
3. **Item-Based Collaborative Filtering:** recommends movies similar to ones the user already rated, based on how other users rated them.

## Results

| Model | MAE | RMSE | Precision@3 | Recall@3 | NDCG@3 | Coverage | Novelty | Diversity |
|---|---|---|---|---|---|---|---|---|
| Popularity Baseline | 1.086 | 1.201 | 0.067 | 0.20 | 0.10 | 0.35 | 1.69 | 0.74 |
| Content-Based | 1.094 | 1.381 | 0.067 | 0.20 | 0.20 | 0.70 | 1.34 | 0.54 |
| Item-Based CF | 0.924 | 1.070 | 0.000 | 0.00 | 0.00 | 0.85 | 1.69 | 0.78 |

## Findings

**Best model for rating prediction:** Item-Based CF. It has the lowest MAE and RMSE, but the improvement over the baseline is small.

**Best model for ranking:** Content-Based. It has the highest NDCG@3 (0.20). Item-Based CF got no hits in its Top-3 lists.

**Coverage, novelty and diversity:**
- Popularity only reaches 35% of the catalogue because it gives almost everyone the same movies.
- Content-Based covers 70% of the catalogue but has the lowest novelty and diversity, since it keeps recommending similar genres.
- Item-Based CF has the best coverage (85%) and diversity, and its novelty is about the same as popularity.

**Extension (Option A, changing K):** Recall@K goes up or stays flat as K increases, while Precision@K tends to go down. The results are noisy because there are very few relevant test items.

## Final Recommended Model

**Content-Based.** The business wants users to find relevant movies without the same popular titles taking over every list. Content-Based had the best ranking score and doubled the coverage of the popularity baseline. The trade-off is lower diversity and novelty, and worse rating accuracy than CF.

## Limitations

1. The dataset is very small (12 users, 20 movies), so the results are not reliable.
2. Only one movie per user is used for testing, and only 5 of those are relevant. One extra hit changes the scores a lot.
3. Content features use genres only, which is a rough description of a movie.
4. The CF similarity treats missing ratings as 0, which can distort similarities.
5. This is an offline evaluation. It cannot show how real users would react to the recommendations.

## Files

- `DSA4060XA_Week6_Guided_Evaluation_Lab.ipynb`: the notebook
- `DSA4060_Week6_Movies.csv`: movie data
- `DSA4060_Week6_Ratings.csv`: ratings data
- `README.md`: this file

To reproduce: restart the kernel and run all cells from top to bottom.
