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
Each of the recommendations came up with different results. The most similar results are the recommendations given through content-based filtering, especially with the first and third methods. 
