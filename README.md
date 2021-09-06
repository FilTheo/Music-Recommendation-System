# Music Recommendation System

This work describes my project for the Data Mining course (MSc Data Science University of Skövde)

It presents a model which outputs a new playlist given an input song and its respective artist.
(The working version of the project updates the playlist as users pick extra songs)

The model returns a complete playlist instead of a single song to deal with the uncertainty originating from the unique musical taste of each individual.
It is very hard, even for a human, to perfectly recommend a single song given just one hint.
The idea is that by proposing a full playlist users will be forced to pick more songs providing additional information to the algorithm to improve its predictions
(Current version outputs a single library)

The recommendation system is based on a Hybrid Approach combining the advantages of both content-based and collaborative filtering techniques.
In particular, it combines information from three different sources.


#### DATA
First, tags giving a representative description of each artist available are scrapped from LastFM.
**Extensive feature engineer** (Noise removal, tags combination through similarity measures, hierarchical representations, Association Rule Mining) took place to reduce the number of total tags and convert them to informative values.
For details refer to supplementary material (report, presentation, code)

Second, metadata for each song is extracted from Kaggle. Metadata include values such as Energy, Loudness, Danceability, etc.

Lastly, for collaborative filtering, the total number of times 75.000 users streamed a collection of songs is also considered.

#### The Algorithm

A brief introduction to the algorithm used for recommending a playlist.

Step 1: Find the artists closer to the user's given artist
Most people prefer to stick to their selected music genre. A person picking a HipHop artist would not like a suggestion from a Metal band.
Thus, I first identify a candidate list with the most similar artists to user's preferences (in terms of most similar tags)

Step2: Filter out complete irrelevant songs based on the song's metadata.
For example, if a user picks a sad acoustic song he probably wants to stay in this mood (we filter out danceable, high energy songs)
A user picking a techno song does not want a rock ballad.

Step3: Item-Based Collaborative Filtering
Item-based similarity based on user reviews is considered and the top-20 songs are proposed.

#### Examples

Pop Recommendations:
![Χωρίς τίτλο5](https://user-images.githubusercontent.com/70523417/91743103-f894be80-ebbf-11ea-8040-c60e3536a745.png)
Classic Rock Recommendations:
![Χωρίς τίτλο9](https://user-images.githubusercontent.com/70523417/91743371-60e3a000-ebc0-11ea-9131-50a7fa4f4c98.png)
HipHop Recommendations:
![Χωρίς τίτλο6](https://user-images.githubusercontent.com/70523417/91743375-617c3680-ebc0-11ea-8bb3-1a91c382db14.png)
PostRock Recommendations:
![Χωρίς τίτλο7](https://user-images.githubusercontent.com/70523417/91743381-62ad6380-ebc0-11ea-9745-7def78c3bc8a.png)
Heavy Metal Recommendations:
![Χωρίς τίτλο8](https://user-images.githubusercontent.com/70523417/91743367-5fb27300-ebc0-11ea-8d24-8e6a80cd9592.png)


