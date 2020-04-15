DS4300 Project Final Report
Boyuan Li, Xiang Zhu, Tanner Lederman

Project Topic: Use a graph database to build a recommendation engine for movies

Goals:
Our goal for this project was to create a recommendation engine for movies. We decided to create recommendation engines through two different approaches: content-based filtering and collaborative filtering. 

Motivation:
We want to explore the capabilities of graph databases in recommendations and
networks. We found a big dataset of movies, ratings, and tags for categories. This gives
us plenty of room to play around and understand how to fine tune recommendations to
a user and also have the flexibility to deal with multiple parameters for
recommendations at once.

Significance:
Recommendations are becoming more and more important and accurate as there is more data available. Learning what goes into these recommendations is very useful as future data scientists. This gives us the ability to make easily scalable and useful recommendation systems for any project we choose to take up in the future. On the other hand, we also learned the limitations that recommendations currently have, as well as the challenges in perfecting the recommendations. 

System Architecture:
- Basic Structure of database:
We used Neo4j to create a graph database. We have three main node types in our graph: A "User" type node, a "Movie" type node, and a "Genre" type node. There are two relationships in this graph: a "rated" relationship and an "in_genre" relationship. The "rated" relationship goes from the "User" type to the "Movie" type, and the "in_genre" goes from a "Movie" type to a "Genre" type. 

All the movie type and genre type nodes were preloaded into the graph, with the "in_genre" relationships made as well. We do not add any extra nodes or relationships of this type with our code. 

- Adding Users:
When they open our application, we prompt them their name and ask them to rate their favorite movie. A User node has a name property value associated with it. 

- Algorithms:
We have two main categories of algorithms for this project: Collaborative Filtering and Content-Based Filtering. 
Collaborative Filtering filters items for a user based on the reactions of similar users. We used three different approaches for collaborative filtering:
1.	 A simple approach which only took genre into account.
2.	An approach that used a cosine similarity which uses the user’s rating on the same movie to a different user’s rating on that movie and selects based on the other user’s preferences.
3.	An approach that used k clustering, adjusted based on the Pearson similarity, or the preferred average rating of each user.

Content-based Filtering filters items for a user based on the properties of the movies the user rated. We used four different approaches for content-based filtering:
1.	A simple approach which filters movies in the graph based on the genres they are in.  * Note * this approach is not personalized and displays aggregate information from all user ratings in the database.
2.	A simple approach which filters movies in the graph by the user’s favorite genre.
3.	An approach that filters with a weighted value consisting of the movie’s genres, actors and directors that the user rated.
4.	An approach that uses the Jaccard Index to track similarity between the user’s rated movies and the movies in the database. The Jaccard Index is calculated by dividing the Intersect of the two sets by the union of the two sets.

All of the algorithms are described in more detail in their Jupyter notebooks. 

Analysis/Conclusions:
Each of the recommendations came up with different results. Since these two algorithms work on the different ways. One is focusing on users, The most similar results are the recommendations given through content-based filtering, especially with the first and third methods. 

Compare and Contrast of the Content-Based Filtering (CB) and Collaborative Filtering (CF):
1. CB advatage-User Independence: Since each user's profile is obtained based on his own preference for the item, it naturally has nothing to do with the behavior of others. And CF is just the opposite, CF needs to use many other people's data. A significant benefit of this user independence of CB is that others will not affect themselves no matter how they cheat on the item.
2. CB advatage-Transparency: If you need to explain to the user why these products were recommended to him, you only need to tell him that these products have certain attributes, which match your tastes and so on.
3. CB advantage-New Item Problem: As long as a new item is added to the item library, it can be recommended immediately. The chance of being recommended is the same as the old item. CF is very helpless for new items. Only when this new item is liked (or rated) by some users, it may be recommended to other users. Therefore, if a pure CF recommendation system, newly added items will never be recommended.
4. CB disadvantage-Limited Content Analysis: In many cases, it is difficult to extract the characteristics of the item from the item. In fact, in almost all practical situations, the item features we extract can only represent some aspects of the item, and cannot represent all aspects of the item.
5. CB disadvantage-Over-specialization: Since the recommendation of CB only depends on the user's past preferences for certain items, the recommendations it generates will also be similar to the items the user liked in the past. If a person has only read articles related to recommendations before, CB will only recommend him more articles related to recommendations. It will not know that users may still like digital.
6. CB disadvantage-New User Problem: The new user has no history of preferences, and naturally cannot obtain his profile, so he cannot generate recommendations for him. Of course, this problem CF also has.
