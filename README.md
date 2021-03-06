# Ruby Talk Material
## Data and Scripts for RubyTalk

To follow the exercise in class, you can install R https://cran.r-project.org/ (and RStudio https://www.rstudio.com/ recommended for Win/Mac) or try to use RinRuby from your Ruby console and download the following files from the folder

 :floppy_disk: train.csv and  :floppy_disk: test.csv

Two files with 70% (train) and 30% (test) of the data on flight delays. The data looks like this:

ARR_DEL15| DAY_OF_WEEK |CARRIER| DEST| ORIGIN| DEP_TIME_BLK
 ------------ | ------------ | ------------ | ------------ | ----------- | -------------
      0|           2|      AA|  LAX   | JFK   | 0900-0959
      0|           2|      AA|  LAX    |JFK    |1200-1259
      0|           2|      AA|  SFO    |JFK   | 0700-0759
      1|           2|      AA|  JFK    |SFO  |  1100-1159
      0|           2|      AA|  SFO    |JFK |   0800-0859
......

 :page_facing_up: predict_flightdelays.RMD is a R html markup file with the code to readin the data, train a model, test it on the test dataset and evaluate the statistics. If you don't have R, you can go to https://github.com/mbbrigitte/Ruby_Talk_Material/blob/master/predict_flightdelays.md to see the mark up online (or http://rpubs.com/mbbrigitte/ML_FlightDelayPrediction).


Data you don't need but are used in the talk

1. Original_data.zip obtained from http://1.usa.gov/1KEd08B
2. prepare_flightdata.RMD is the code to clean and tidy the data and split them into train and test, and save them as csv
3. Cluster_presentation.RMD is the short code presented to perform hierarchical clustering on random data.

EOF
