### Dataset Description

The dataset consists of metadata for a collection of movies obtained from Kaggle. It contains structured and textual attributes describing various aspects of each movie, such as plot summary, thematic tags, and audience ratings.

For this assignment, only the following fields were used:

- `overview`: A textual plot summary describing the main storyline of the movie.
- `tagline`: A short promotional sentence summarizing the movie.
- `keywords`: A set of descriptive terms associated with the movie’s themes or elements.
- `genre`: The genre labels assigned to the movie. A movie may belong to multiple genres (multi-label setting).
- `voting_average`: The average audience rating score assigned to the movie (continuous value).

The dataset includes movies spanning multiple genres such as Action, Comedy, Drama, Romance, Horror, Science Fiction, and others. Since movies can belong to more than one genre, the genre prediction task is formulated as a multi-label classification problem.

The textual fields (`overview`, `tagline`, `keywords`) vary in length and level of detail. The `overview` field typically contains the richest semantic information, while `tagline` is shorter and more promotional in nature. This variation allows comparison of predictive performance across different types of text inputs.

Before modeling, the dataset was cleaned and preprocessed to ensure consistency and reproducibility.  
