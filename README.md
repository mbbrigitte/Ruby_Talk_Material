# Ruby_Talk_Material
## Data and Scripts for RubyTalk

To follow the exercise in class, you need the following files from the folder

train.csv and test.csv
Two files with 70% (train) and 30% (test) of the data on flight delays. 

   X |ARR_DEL15| DAY_OF_WEEK |CARRIER| DEST| ORIGIN| DEP_TIME_BLK
   ------------ | ------------ | ------------ | ------------ | ------------ | ----------- | -------------
1  1|         0|           2|      AA|  LAX   | JFK   | 0900-0959
2  3|        0|           2|      AA|  LAX    |JFK    |1200-1259
3 10|         0|           2|      AA|  SFO    |JFK   | 0700-0759
4 12|         1|           2|      AA|  JFK    |SFO  |  1100-1159
5 13|         0|           2|      AA|  SFO    |JFK |   0800-0859
......

predict_flightdelays.RMD is a R html markup file with the code to readin the data, train a model, test it on the test dataset and evaluate the statistics. If you don't have R, you can go to ...... to see the html document to follow.


Data you don't need but are used in the talk
1) Original_data.zip obtained from http://1.usa.gov/1KEd08B
2) prepare_flightdata.RMD is the code to clean and tidy the data and split them into train and test, and save them as csv
3) Cluster_presentation.RMD is the short code presented to perform hierarchical clustering on random data.

