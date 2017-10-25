# Outline


# Our recommender system

Based on the history of the articles the user read:

    1. one trains the neural network on the articles already read
    2. one defines a neighborhood of wikipedia articles "nearby"

        - custom distance: increases with the distance in the graph, decreases with the popularity
        - Millions of articles ⟹ intractable to score each nearby articles within a reasonable time (hundreds of milliseconds).

            - ⟶ pre-processing of articles needed: *retrieval*
    3. one submits these nearby articles to the neural network


# Wide and deep neural network


*Problem*: find a tradeoff between

- memorization (to find articles close to what the user is known to appreciate)
- generalization (to suggest articles to which the user is not accustomed: *serendipity*)

⟶ Use of wide and deep neural networks cojointly

## Wide NN

Generalized linear model:

$$y ≝ w^T x + b$$


# Retrieval of wikipedia articles
