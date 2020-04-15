# IPL-Predictor(Walkthrough into Deep Neural Network and tuning) 
Win Percentage Predictor for past IPL mathces(2007-2017)

Greetings!
Hope you all have seen pre-match predictor of Google.It displays win percentage for both the teams.Though I am not here to compete with it,I am trying to build my own version of it.


# Data collected and my methodlogy:-

The data I collected has two parts:-

1.Match data including the two teams,venue,date.(easily available online).

2.Player ICC T20 rankings of both teams playing as on match time.(http://www.relianceiccrankings.com/twenty20.php)

I have created some new variables by checking on their rankings and then removed some of the intermediate team matches like pune warriors etc and manipulated the rest of the variables for the best accuracy.I have attached the screenshots of the accuracy for the reference.I observed that deep neural network gave me the best accuracy.I have used tanh estimator(retains distribution well and takes care of outliers) to scale my variables for the other algorithms which finally gave me lower accuracy.I have removed the players name and in place of that created a rank variable for each player thereby creating 22 new variables.My network would predict the winning percentage of each teams prior the match.

![Final accuracy](https://github.com/themendu/IPL-Predictor/blob/master/Screenshot%20(26).png)


# Observations:-

1.My model is of no use if the accuracy metric(considering binary classes and no win percentage) is less than 0.5(human bias level).

2.By the initial impressions of train vs validation losses, I was getting two constant lines differing by a constant which is a sign of underfitting(even changing the learning rate didn't make any change).My model is not at all capable of learning and then I changed my learning rate and used a different optimizer(SGD) with increased layers and my batch size being 32(ideal number).This made my model do better.

3.In the proccess of my tuning I have a model where my training loss is higher compared to validation loss(considering binary cross entropy as my loss function).This may be due to the regularization I have applied at that time beacuse it penalizes the loss function by adding certain positive term to it.This may be due to my model which did not learn anything at all(which is the case here).This may be due to my easy validation dataset compared to trainnig set.

4.I could manage a model that can equally learn and test the data(ideal model for our data assuming our data is represent enough to predict).The underfit is due to less amount of USEFUL data that is available(which would be the final result as I can't fetch more useful features for my data).I finally acheived an accuracy of around 56%(which is permissible).But it is evident that I did not overfit from seeing the loss functions.

5.Note that if our model validation loss decreases and then increase while our training loss keeps decreasing that is a sign of overfit.A perfect fit is where our losses are comparable and we get our training loss slightly lower(obvious reasons) than validation loss.Here in my case may be the model is leaening the statistical noise of the data instead of generalization of it.

6.By performing the grid serch on other algorithms gave me lower accuracy than DNN.


![train versus validation loss curves](https://github.com/themendu/IPL-Predictor/blob/master/Screenshot%20(27).png)



# Files descriptions in the repository:-

1.2009.csv contains top 100 T20 players list(both batting and bowling) at match time.

2.The two notebooks with one containing data preparation and the other the DNN modelling which I used in a google colab. 

3.The two screenshots I have provided.

4.The two csv files containing match data and players list for a particular t20 match.

