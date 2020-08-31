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

The Final format of the first Dataset:

![First Dataset](https://user-images.githubusercontent.com/70523417/91741199-0a289700-ebbd-11ea-967a-a3f23245ef01.png)


Moreover, the second dataframe regarding the content based approach contains over 232.000 songs, from different music types, where each song had over 12 features. These features are continuous values which describe a specific metric of each song. These metrics include loudness in decibels, valence, which described the musical positiveness of a track, energy and others. **A detailed explanation of what each feature describes is included on the uploaded notebook**. 

The format: 

![Second Dataset](https://user-images.githubusercontent.com/70523417/91741444-65f32000-ebbd-11ea-9b34-0a2e219db539.png)


Second dataset: https://www.kaggle.com/zaheenhamidani/ultimate-spotify-tracks-db

Finaly the third dataset which is used for the collaborative filtering method is taken from kaggle too,( https://www.kaggle.com/anuragbanerjee/million-song-data-set-subset) and contains 76,353 unique user IDs and the total number of times they have streamed every one of the 76.000 songs.

Third Dataset:

![Third Dataset](https://user-images.githubusercontent.com/70523417/91741456-6a1f3d80-ebbd-11ea-8ffd-8566e55b8d1b.png)

## System's Architecture

After considering that most people prefer to stick to a certain music type at each specific moment, a hierarchical approach was implemented to combine all three methods. It was prefered from other approaches, like creating a playlist which is on average "more similar" to the initial input song. A person who loves rock music and chooses a rock song as his input song, would prefer to get a rock playlist, instead of a playlist with mixed electronic, rock and hip hop music. Similarly ,a user who loves Hip Hop music wont be interested in a black metal recommendation, just because a hip hop and a black metal song might have similar features.

First step’s is applied on the artists dataset. A list of the artists with have tags "closer" to user’s preferred artist, is produced. These artists play the same music type and share the most common tags with the user’s pick. 
What is more, all of songs of these proposed artists,which are included on the rest of the datasets, are gathered and are “filtered” through the second content based dataset, with the song features.With this approach, all songs that are totally unsimilar with the user’s prefered song would be removed.

For example, a user that picked an acoustic, sad song from a Rock Artist would most likely prefer a calm ,acoustic,low on valence playlist. Filtering the songs of the closest Rock artists through the metrics dataset would only keep these kind of songs. Similarly, if a person chooses an energetic, danceable, pop song, the model will extract the danceable energetic songs from the most similar pop artists.

Last but not least, item based collaborative filtering will be used and out of the songs produced by the second method, a playlist of songs that are mostly liked by users, who liked the input song , will be produced. 
Another reason φορ choosing collaborative filtering as the last method is its high sparsity. Getting slow recommendations would be a major setback. Preparing recommendations from a less sparce Utility matrix would highly improve the calculation time.

**Note**
It should be pointed out that if the input artist is not found on all datasets, the system will ask for another artist. What is more, if the artist is matched but the song is not included on all datasets, all the songs from the desired artist which are included on all datasets would be proposed to the user so he can change his initial choice. 

For example:

![Not matched](https://user-images.githubusercontent.com/70523417/91742656-41984300-ebbf-11ea-9bd1-b6757b42bc01.png)

## Performance

The algorithm excelled in pop and Hip Hop music and produced some pretty good recommendations. On the other hand, as far as rock music is concerned, because of the small number of the common artists in all three datasets in comparison to the individual number each one contained, in addition to including plenty of common songs from specific artists but not from most of the rock artists, resulted in recommendations being rather general than specialized. 

Despite the approaches made to increase the number of common artists, the results were still not perfect. In some future work, the same hybrid method will be used, but datasets would be acquired from the same source, so artists names and songs will be similar. As a result, a larger collection of songs will be available to be proposed and the recommendations will be more accurate.

Some recommendations:

![Χωρίς τίτλο5](https://user-images.githubusercontent.com/70523417/91743103-f894be80-ebbf-11ea-8040-c60e3536a745.png)
![Χωρίς τίτλο9](https://user-images.githubusercontent.com/70523417/91743371-60e3a000-ebc0-11ea-9131-50a7fa4f4c98.png)
![Χωρίς τίτλο6](https://user-images.githubusercontent.com/70523417/91743375-617c3680-ebc0-11ea-8bb3-1a91c382db14.png)
![Χωρίς τίτλο7](https://user-images.githubusercontent.com/70523417/91743381-62ad6380-ebc0-11ea-9745-7def78c3bc8a.png)
![Χωρίς τίτλο8](https://user-images.githubusercontent.com/70523417/91743367-5fb27300-ebc0-11ea-8d24-8e6a80cd9592.png)


