# Music Recommendation System
The project will be about a model that  creates a new playlist for the user, based on his music taste. 
As every individual has a unique music taste and making accurate propositions based on a single input song is tricky, and after considering the huge amount of different songs and music types that do exist, instead of a single recommendation, a whole playlist is being generated and recommended

A simple example is when person A and person B both like a particular song. If the system proposes a single song, there is a big possibility person A would like the song, while person B will not.

By proposing a playlist of 20 songs:
* User can choose which song he likes, or even listen the whole playlist
* User is "forced" to pick more songs out of the proposed playlists, so more data about his preferences are gathered in order for the system to make better recommendations.

## Recommendation System(RS) Approach
The designed model uses a hybrid approach which is a combination of content based and collaborative filtering. 
#### Content Based Approach
As far as content based approach is concerned, recommendations are being produced based on similarities between items, songs. Each songs, contains unique attributes, metadata, such as energy, accousticness, loudness and valence. In addition, as plenty of music genres do exist and every artist has a unique identity based on the music type he plays, unique keywords/tags which describe every respective artist are also taken into account. The most similar with the user's input songs, are recommended.

**Limitations:**
* Generating enough attributes for all items is complicated
* Measuring similarity of songs based on metadata such as energy and loudness might lead to inaccurate recommendations 
* Overspecialization: Model might recommended the same type of items
* No feedback, and hence, not possible to rate the recommendations

#### Collaborative Filtering
On the other hand, a RS based on Collaborative Filtering, finds other users that have similar preferences to the target user and recommends songs the majority of the extracted subset of users like. There is no requirement for any information about the items or the users themselves. An item-based approach is selected, where the similarity between songs, based on users reviews, will be measured and the songs closer to user's selection will be recommended. 

**Limitations**
* Sparsity Problem: As plenty of songs and user do exist, the Utility Matrix used to find the closer songs to user's like might end up being too sparse
* Popularity Bias: Certain Items are very highly rated and hence system tends to over-recommended them("Harry Potter" problem)
* Changes on users' preferences over time

#### Hybrid Approach
A Hybrid Approach was selected as it hides the major limitations of the aforementioned approaches. Proposing songs based on both similar metadata, such as music attributes and music genres , in addition to songs that got streamed a lot, by people with similar music taste would result in far more accurate results.

## Datasets Used

For the Content Based method, two different datasets containing completely different features were selected. 
Firstly a dataframe with over 10.000 unique Artists, along with the 4 most descriptive tags for each respective artists was scrapped from https://www.last.fm/ 
When the dataframe was obtained, it had over 2100 different tags in total.  A number that would create many sparse issues and bad recommendations. After applying different techniques and algorithms, the total number of tags was reduced to 432. Tags include properties such as "big" music genres like Rock, Pop, HipHop, or genres which are more desriptive like Punk, Post, or Industrial. **More details are given on the uploaded notebook.**

Moreover, the second dataframe regarding the content based approach contains over 232.000 songs, from different music types, where each song had over 12 features. These features are continuous values which describe a specific metric of each song. These metrics include loudness in decibels, valence, which described the musical positiveness of a track, energy and others. **A detailed explanation of what each feature describes is included on the uploaded notebook**. 

Second dataset: https://www.kaggle.com/zaheenhamidani/ultimate-spotify-tracks-db

Finaly the third dataset which is used for the collaborative filtering method is taken from kaggle too,( https://www.kaggle.com/anuragbanerjee/million-song-data-set-subset) and contains 76,353 unique user IDs and the total number of times they have streamed every one of the 76.000 songs.

![GitHub Logo](C:\Users\Φιλωτας Θεοδοσιου\Desktop)
Format: ![Alt Text](url)
