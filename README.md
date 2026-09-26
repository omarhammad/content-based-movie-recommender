# Content-Based Movie Recommender

A Jupyter notebook project that recommends movies with similar plot descriptions. It enriches a 10,000-row movie dataset with overviews from The Movie Database (TMDb), represents those overviews with TF-IDF, and ranks candidates using cosine similarity.

## How it works

1. `data_preprocessing.ipynb` reads `themoviedb.org.csv`, requests an overview for each title from TMDb, and writes `themoviedb_with_overviews.csv`.
2. `movies_recommendar.ipynb` replaces missing overviews with empty text and builds a TF-IDF matrix with English stop words removed.
3. The notebook calculates pairwise cosine similarity and defines `recommend_movies(title, top_k_recommendations=5, similarity_threshold=0.2)`.
4. The function selects the most similar movies above the threshold, then displays the selected titles ordered by release date, with overview, rating, genre IDs, and date.

The similarity ranking is based only on overview text. Ratings and genres are displayed in the result but are not used to compute similarity. This is a content-based demonstration, not a personalised recommender trained on user activity.

## Repository structure

| File | Purpose |
| --- | --- |
| [`data_preprocessing.ipynb`](data_preprocessing.ipynb) | Retrieves movie overviews from TMDb and produces the enriched CSV. |
| [`movies_recommendar.ipynb`](movies_recommendar.ipynb) | Builds TF-IDF features and returns similar movies. |
| [`themoviedb.org.csv`](themoviedb.org.csv) | Source dataset with 10,000 movie rows. |
| [`themoviedb_with_overviews.csv`](themoviedb_with_overviews.csv) | Dataset enriched with an `overview` column. |
| [`requirement.txt`](requirement.txt) | Listed Python dependencies. |

## Run the recommender

1. Set up a Python environment with Jupyter, pandas, scikit-learn, and IPython.
2. Open `movies_recommendar.ipynb` from the repository root and run the cells in order. The enriched CSV is already included, so TMDb access is not needed to try the recommender.
3. Change the `title`, `top_k_recommendations`, or `similarity_threshold` values in the example cell to explore the results.

To regenerate the enriched dataset, `data_preprocessing.ipynb` also needs `requests` and a valid TMDb API key. Replace the hard-coded key in that notebook with a private configuration value before publishing or running it. Search results by title may not always match the intended movie when titles are ambiguous.

## Technology

Python · Jupyter Notebook · pandas · scikit-learn · TF-IDF · cosine similarity · TMDb API

## Limitations

There is no user preference model, offline recommendation metric, or application interface. The notebook computes a full pairwise similarity matrix, which becomes costly as the dataset grows. Recommendations depend on the quality and availability of movie overviews.
