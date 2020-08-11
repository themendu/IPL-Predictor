# IPL-Predictor(Walkthrough into Deep Neural Network and tuning) 
Win Percentage Predictor for past IPL mathces(2007-2017)


Pre-match predictor of Google is well known.It displays win percentage for both the teams prior to the match occurence.Though I am not here to compete with it,I am trying to build my own version of it.


# Data collected and my methodlogy:-

The data collected has two parts:-

1.Match data including the two teams,venue,date.(easily available online).

2.Player ICC T20 rankings of both teams playing as on match time.(http://www.relianceiccrankings.com/twenty20.php)

Some new variables are created by checking on their rankings and then removed some of the intermediate team matches.Deep neural network gave the best accuracy.Tanh estimator(retains distribution well and takes care of outliers) is also used to scale my variables for the other algorithms which finally gave me lower accuracy.Players name is removed and in place of that created a rank variable for each player thereby creating 22 new variables.The network would predict the winning percentage of each teams prior the match.

![Final accuracy](https://github.com/themendu/IPL-Predictor/blob/master/Screenshot%20(26).png)


# Observations:-

1.Model is of no use if the accuracy metric(considering binary classes and no win percentage) is less than 0.5(human bias level).

2.By the initial impressions of train vs validation losses, I was getting two constant lines differing by a constant which is a sign of underfitting(even changing the learning rate didn't make any change).My model is not at all capable of learning and then I changed my learning rate and used a different optimizer(SGD) with increased layers and my batch size being 32(ideal number).This made the model do better.

3.[TabNet](https://arxiv.org/pdf/1908.07442.pdf) is applied along with artificial neural net but no better accuracy is acheived.

4.In the proccess of my tuning we have a model where the training loss is higher compared to validation loss(considering binary cross entropy as my loss function).This may be due to the regularization I have applied at that time beacuse it penalizes the loss function by adding certain positive term to it.This may be due to my model which did not learn anything at all(which is the case here).This may be due to my easy validation dataset compared to trainnig set.

5.A model that can equally learn and test the data(ideal model for our data assuming our data is represent enough to predict) is achieved.The underfit is due to less amount of USEFUL data that is available(which would be the final result as I can't fetch more useful features for my data).Finally an accuracy of around 56%(which is permissible)is achieved.

6.Note that if our model validation loss decreases and then increase while our training loss keeps decreasing that is a sign of overfit.A perfect fit is where our losses are comparable and we get our training loss slightly lower(obvious reasons) than validation loss.Here in my case may be the model is learning the statistical noise of the data instead of generalization of it.

7.By performing the grid serch on other algorithms gave lower accuracy than DNN.


![train versus validation loss curves](https://github.com/themendu/IPL-Predictor/blob/master/Screenshot%20(27).png)



# Files descriptions in the repository:-

1.2009.csv contains top 100 T20 players list(both batting and bowling) at match time.

2.The three notebooks with one containing data preparation and the other two for modelling. 

4.The two csv files containing match data and players list for a particular t20 match.

