Can we predict IMDB movie and tv show scores?
What makes a good show or movie? Is it genre? Runtime? Internet upvoting?
Author:  Mike Fiddler

Business problem:
Can we predict how well a movie or show is going to rated based on past movies performance and therefore know what types of shows or movies we should be making?

Data: https://www.kaggle.com/datasets/victorsoeiro/netflix-tv-shows-and-movies
Our data comes from the kaggle website and we start with fifteen features to analyze.  
Data Dictionary (only of the columns we use):
Type: Show or Movie
Release Year = The release year
Runtime: Length of the film in minutes
Genres: The genre the film belongs to
IMDB Score: Score on IMDB
IMDB Votes: Votes on IMDB
TMDB Popularity on TMDB
TMDB Score: Score on TMDB

Methods
I started by checking the shape (5806,15) of the data set and checked for missing values.  I checked for duplicates then began dropping columns with useless information.
I ended up dropping seven of the fifteen columns.  Next i began exploring the data looking for incorrect or inconsistant data.

![image](https://user-images.githubusercontent.com/105397828/181585897-8970ac7b-e761-4541-8bb7-ae93a0a60dd7.png)
Here you can see we had alot of outliers in the imdb_votes column so that made me realize that when imputing the data for that column I should use median and not mean
values to prevent all these outliers from skewing my imputations.
Next I looked into the genre feature and found it had 1626 unique values.  The reason for this is that most movies and shows fit into multiple categories. Not only does that make
for bad OHE it also gives to broad a range for the actual genre category.  So I decided to just use the first two genres listed (if they had two). 

![image](https://user-images.githubusercontent.com/105397828/181587600-f07a617c-2244-4081-a40d-6e80896cdc16.png)
Here we can see the spread of the imdb scores for every show and movie in our set.  Notice not alot of low scores and not alot of really high scores either.  They're generally in the range of 6-8.
After a few more visuals to help understand my data I moved on to machine learning.
![image](https://user-images.githubusercontent.com/105397828/181632576-a5d5f427-a739-46a3-b87e-4cab5a1d421d.png)

My first ML was the unsupervised KMeans which gave me this nice plot showing us that runtime does not have a huge effect imdb score.  Cluster 1 is all the shows in this data set and the mean imdb score for both cluster 0 and 1 are almost identical.

Next I went onto supervised learning and started with a bagging regressor.  90% fit on the training set but only 49% on the test set for our base model.  I went on to tune the number of estimators and was able to impove the train and test scores to 93% and 55% respectivly.
My forest regressor started out better then the bagging model with a 54.5% test score.  I went on to tune the depths and estimators.  However even with tuning my test score only increased by .002%.

Unfortunately the ability of my models to successfully predict a corret outcome is very low.  The best we got was a dismal 55% accuracy on the test set.
With that in mind if one model had to be chosen I would advise the random forest tuned model bringing back that 55% over the bagging model that was at 54%.

I believe that with more relevant data (such as money grossed or times watched) it could be possible to create a better model. 

For further information
For any additional questions, please contact me via email fid2445@hotmail.com
