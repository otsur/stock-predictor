# Stock_Market_Predictor
Made a model that predicts next day's close price given the current day's open, high ,low ,Adj close and volume. Used LSTM and Linear Regression to do the above time series analysis to get good results! 


Due credit has been given to all the references in comp4-finalday.ipynb
There are 3 pynb files which we have submitted. The 4 files are as follows :
1) comp4-finalday.ipynb
2) comp3-finalday.ipynb
3) comp2-finalday.ipynb
Use comp4-finalday as reference because it was mainly used to comment.
At start of the come we added test dataset with traindataset with close = 0 for test dataset
(never used , just to put a value)
We decided to use weighted LSTM with Linear regression. Linear regression code is
straightforward. LSTM and LSTM + LR code is little hard to understand to their brief overview is
given below :

##LSTM
LSTM is a RNN technique which has some memory basically. It takes a bunch of clusters from
past to predict a value in future usually in time series.
 
 ![LSTM](https://github.com/SreehariC/Stock_Market_Predictor/assets/95119050/61341ee4-80ca-475c-96b3-2e5f026f6fd6)

Here basically what we are doing is that making chunks of 60 i.e. 0 to 59 for i=0 for x_train and
then predicting y_train which is at 59th index i.e. the next day close.

![LSTM-2](https://github.com/SreehariC/Stock_Market_Predictor/assets/95119050/17a35c21-c508-4008-8b36-73e04ac17b11)

For testing we are taking 59 elements from the training set and 1 from the current set whose
next day close needs to be predicted. This is depicted above in the code

##LSTM + LR
 Here we basically used LR and LSTM combined. Mainly LSTM is called again and again to
calculate the next day value and then add this value in the data and again retrain the model.
This took most time and we used 3 files each for company 2,3,4. To get the final csv , calculate
the comp4_633.csv , comp3_633.csv and comp2_633.csv (names might be different) and
comp1_LR.csv and combine them.

The above idea is briefly mentioned in the code below:-
  
  ![LSTM-3](https://github.com/SreehariC/Stock_Market_Predictor/assets/95119050/7fb98c6c-e599-4954-80c7-71e41e391bab)
 
Here we basically changed the close value from 0 to the calculated value in previous iteration.
Rest all the code is same as LSTM
