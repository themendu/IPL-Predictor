# IPL-Predictor
Win Percentage Predictor for past IPL mathces(2007-2017)

Greetings!
Hope you all have seen pre-match predictor of Google.It displays win percentage for both the teams.Though I am not here to compete with it,I am trying to build my own version of it.

Data collected and Summary:-

The data I collected has two parts:-
1.Match data including the two teams,venue,date.(easily available online).
2.Player ICC T20 rankings of both teams playing as on match time.(http://www.relianceiccrankings.com/twenty20.php)

I have created some new variables by checking on their rankings and then removed some of the intermediate team matches like pune warriors etc and manipulated the rest of the variables for the best accuracy.I have attached the screenshots of the accuracy for the reference.I observed that deep neural network gave me the best accuracy.I have used tanh estimator(retains distribution well and takes care of outliers) to scale my variables for the other algorithms which finally gave me lower accuracy.The errors in some notebooks

![alt text](http://url/to/img.png)
![alt text](http://url/to/img.png)

Files names collected:-

1.2009.csv contains top 100 T20 players list at match time.
2.The two notebooks with one containing data preparation and the other 
3.The two screenshots I have provided.


Observations:-

1.My model is of no use if the accuracy metric(considering binary classes and no win percentage) is less than 0.5(human bias level).
2.By the initial impressions of train vs validation losses, I was getting two constant lines differing by a constant which is a sign of underfitting(even changing the learning rate didn't make any change).Then I modified my network
3.The underfit is due to less amount of USEFUL data that is available(which would be the final result as I can't fetch more useful features for my data) .Even removing dropout,increasing layers did not help.I finally acheived an accuracy of around 58%(which is permissible).
4.By performing the grid serch on other algorithms gave me lower accuracy than DNN.
