#**Instagram Post Prediction**

##**Description of the dataset **

The dataset contains two data files
###**Instagram_profiles.csv**

['ig_id', 'username', 'metadata', 'followers', 'follows',
       'total_post_count', 'crawled', 'created_at', 'updated_at',
       'app_crawled']

•	Number of rows : 537
###**Instagram_post_profile.csv**

['ig_id', 'post_id', 'permalink_url', 'metadata', 'comments', 'likes',
       'crawled', 'created_at', 'updated_at', 'slug', 'views', 'plays',
       'hashtags']

No of rows: 6372 


###**Merging the two dataset**
In order to do analysis of  the data both the dataset were merged on the column “Id_id”

###**Bivariate analysis and Feature engineering** 

Following new features were created from the dataset :
1.	Time_of_day : After extracting hours from timestamp , time is classified into morning ,afternoon ,evening , late evening , night 
2.	Type_of_post: Extracting the information from Metadata , type of post includes value – story , video , image, caserol 
3.	Day_of_Week : Using Timestamp , classifying the post on the day it was posted . eg – Sunday (0)
4.	Average_Likes: Total no of likes of each username / Total post in the dataset 
5.	Average_Comments : Total no of likes of each username / Total post in the dataset 
6.	Is_Reel : a post is a reel or not 
7.	Sentiment_in_caption : Using NLP extracting the sentiments in the caption without hashtags
8.	No_of_Hashtags: The no of hashtags used in the caption 




##**Image Features**

Following new features were created using the images /reels download for the post :
Dataset collection : Downloaded post from within the dataset mentioned post .
Using image/video for each user  

9.Humans_present_in_post = Detection of faces in the image/videos using cv2
10.Brightness_of_image= checking if image quality – bright image / non bright image based on a threshold of 0.75 using cv2 library 

Note :The whole dataset couldn’t  be downloaded , due to memory and time restrictions . The missing values are treated by mode of the value for the above two features. For each user min 20 post were downloaded .



 
##**Model Building**

The following steps were taken built the model for the 1st Problem statement :
1st Problem statement :

To predict the engagement (likes and comments) of future posts.
Predicting the like of Instagram post
1.	Label Encoding : Encoding Categorical variables 
2.	Scaling the data : Arranging all the columns within the same range so that they can be compared and understood by the model .
3.	Dropping uncesseray columns 
4.	Selecting features after evaluating through co-relation matrix 
5.	Splitting the data into train test split  
6.	Features
'No_of_Hashtags','day_of_week',  'Post_Sentiments','Time_of_day','post_type','followers','brightness','face_detection'
Target variable: likes
7.	Model Selected : Random Forest 

Reason for selecting random forest : Building a supervised learning regression model for predicting the likes of an Instagram post . The random forest removed the overfitting issue faced in previous model which were initially tried to fit  eg linear regression , XGboost ,Decsion tree .

##**Predicting the comments of Instagram post**

Same Initial steps as above 

###**Features**

'No_of_Hashtags', 'followers', 'day_of_week', 'username', 'Avg_comments', 'Post_Sentiments','Time_of_day','post_type','brightness','face_detection'
Target_value: Comments

Model Selected : Random Forest 

###Reason for selecting random forest : 
Building a supervised learning regression model for predicting the likes of an Instagram post . The random forest removed the overfitting issue faced in previous model which were initially tried to fit  eg linear regression , XGboost ,Decsion tree .


##**2st Problem statement**

##**To predict the engagement (views and plays) of future reels.**

Predicting the views of Instagram Videos
1.	Label Encoding : Encoding Categorical variables 
2.	Scaling the data : Arranging all the columns within the same range so that they can be compared and understood by the model .
3.	Dropping uncesseray columns 
4.	Selecting features after evaluating through co-relation matrix 
Features
'Avg_likes','plays', 'No_of_Hashtags','No of Videos', 'day_of_week', 'username', 'Post_Sentiments','Time_of_day','followers','brightness','face_detection'
Splitting the data into train test split
5.	Filtering the dataset with post which were of type video 
6.	Using the records whose views were non zero for train and validation by splitting it 70:30 ratio 
7.	For testing taking the records views/plays are zero to predicts their views with help of model
##Model Building : XGBoost
-To boost weak variables and increase the accuracy of the model 


##Predicting the plays of Instagram Video
Same Initial steps as above 

Features
'Avg_likes', 'No_of_Hashtags','No of Videos', 'day_of_week', 'username', 'Post_Sentiments','Time_of_day','followers','brightness','face_detection'
Model Selected : XGBoost
- To boost weak variables and increase the accuracy of the model

