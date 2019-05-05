
# AYN-337
Ethan Holleman, Priya Patel, Collin Lorentzen
Group 4

STATS 337


For this project we used the lung dataset available from the survival package in R which includes observations of lung cancer patients and their outcomes, more information about the lung dataset can be found in the survival package documentation [here](https://cran.r-project.org/web/packages/survival/survival.pdf)

First, to visualize the predicted survival function we used the kaplan meier function found within the *survival* package. The solid red line shows the predicted survival curve and the dotted lines show the 95% confidence interval. 
![Rplotkm](https://user-images.githubusercontent.com/45807040/57195631-7daf8b00-6f1a-11e9-85bd-a441d9a59f0b.png)

We also plotted the cumulative hazard function which can be seen below, while the kaplan meier curve shows proportion of suviving patients at a given time, the hazard function shows the risk of the event(death) occuring as time goes on.
![ch](https://user-images.githubusercontent.com/45807040/57195773-0ed33180-6f1c-11e9-98c7-167bdf124c8f.png)

We also wanted to see what distrabution type would make the best smooth estimate of the survival curve.

![Screenshot from 2019-05-05 10-29-21](https://user-images.githubusercontent.com/45807040/57196256-c0746180-6f20-11e9-8ed9-b8296a71814e.png)

Based on AIC and log likelihood we found the generalized gamma curve to give the best results. 

Next, we wanted to determine if any of the predictors were significantly impacting patient outcomes based on the Kaplan Meier method. The results of three of these comparisons are shown in the three figures below. 

![Rplotage](https://user-images.githubusercontent.com/45807040/57195812-6bcee780-6f1c-11e9-98be-88edcb23f8af.png)
![Rplotsex](https://user-images.githubusercontent.com/45807040/57195821-7be6c700-6f1c-11e9-80af-75aa7dda5d64.png)
![Rplot](https://user-images.githubusercontent.com/45807040/57195824-86a15c00-6f1c-11e9-83e8-473bf5a529db.png)

Since Kaplan Meier will only tolerate categorical variables age and wt (weight loss) were transformed based on the mean of all observations. In both cases individuals above the mean were given the value 1 and those below 0. From these results we can see that sex is the only significant predictor, with females showing greater survivorship compared to male lung cancer patients. 

Next we constructed a cox proportional hazard model and used stepwise selection based on AIC to select the best model. The model summary is shown in the R output below. 

![Screenshot from 2019-05-05 10-08-17](https://user-images.githubusercontent.com/45807040/57195973-bdc43d00-6f1d-11e9-8f11-05135d2b7a11.png)

From the summary we can see that sex and ph.egog are the significant predictors in the model. 
This makes sense as sex was also significant in the Kaplan Meier model and ph.egog is a measure of overall patient health by a physician with a higher value indicating worse health. Looking at the coefficients we see that as this measure increases risk of death occurring greatly increases (2.1022)

Finally, we used a random forest model constructed from the ranger R package to round out our data analysis. The random forest model was constructed with 500 trees, and the rank of each covariante can be seen in the table 2 below. 

| Predictor | Weight |
| ------------- | ------------- |
| ph.ecog | 0.0213567476 |
| pat.karno | 0.0184760718 |
| sex | 0.0057961043 |
| wt.loss | 0.0026184009 | 
| age | 0.0001386971 |

Finally, we compared the predicted survival curves for all models used. This showed that the Cox PHM and Kaplan Meier curves gave very similar results while the random forest model provided a more optimistic estimate. The 95% confidence intervals for each model have been omitted for readability. 

![Screenshot from 2019-05-05 10-22-56](https://user-images.githubusercontent.com/45807040/57196168-cc135880-6f1f-11e9-854b-3d940a8c2ed6.png)


