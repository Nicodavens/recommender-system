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


##A recommandation based on the structure of articles

This recommander system is based on three facts, which are generally true. A wikipedia article is divided into three parts :
-*the table of contents* : longer it is, more general the article is
-*the introduction*, in which the general concepts useful to understand the notion are given
-*the body*, in which details are given, the technical details and the application


We can thus assume that more precise articles are referenced in the body, whereas general ones are in the introduction. The goal will be to create an order over the article read by the user, under the relation *is more general than*.
A new node to this tree would be added each time the user reads an article. Once a "stationary state" will be reached, only referenced pages liked in already read articles.

The idea is that, if the user wants a more general article, or do not have the basics to understand one, the recommander system would branch on a page more general, which is either a page in the introduction of the current page, or in the body of the previous page. This is technically difficult, but a construction trying to avoid cycles is described here.
To recommand precise article, we need to search among the body of an "ancestor article", whereas for more general article, an article from the introduction of an ancestor will be chosen. The ancestor chosen would be chosen randomly, and the recommanded article chosen thanks to the neural network among the set of referenced articles, but not those already visited.

Each time an article will be read, 3 binary question will be asked to the user :
1. Is this article interesting ? -> to actualise the neural network
2. Is this article too precise ? -> to search among ancestors
3. Is the quality of this article good ? -> avoid to fool the neural system

This theory has some problems :
-cycles may appear
-the two fact are not true in general
-some "stared" articles have a long table of contents and are very complete, but we do not want to see them as very general
-cold start


The two first problems have to be tested, but we have no proof it will be efficient
The third one may be solved, assuming that stared articles are interesting, not depending on the fact there are general or not : even if the person knows what it is about, a stared article is still interesting because of its quality.
The fourth one is just solved by giving random 10 random article initially.

Two articles will be recommaded : one depending on the 'precise' wanted and another about serendipity which search deeper in the ancestors. 
