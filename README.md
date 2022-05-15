# Click-through-rate-predictor

## Description

**Goal**
<br> In programmatic advertising, ad space purchasing is automated. In some instances, a real-time bidding takes place where the price of the ad space is determined by the outcome of an auction. Advertisers will make bids for the ad space, the highest bidder wins the auction and their ad would be loaded to the space. This model produces a bid multiplier (which sets the bid of a given ad space). The bid multiplier is determined by the click through rate predicted by the model. 

<br> The aim of this model is therefore to correctly predicting whether or not an ad would have a high click through rate (CTR). A high CTR was defined here as >= 0.08 %. A bid multiplier is then assigned based on whether or not an ad is predicted to have a high CTR.
<br>

**Classifier**
<br> This notebook generates a binary classifier, which, for a given set of features, predicts whether an ad would have a high CTR or a low CTR. 
  - Labels: 
      - High CTR (i.e. >= 0.08 %): class 1
      - Low CTR (i.e < 0.08 %): class 0
  - Features:
      - Device type
      - Time of day (i.e. hour)
      - Day of week

**Evaluation metric** 
<br> The dataset was highly imbalanced with the majority (ca. over 90%) of the observations being in the low CTR class. Correctly predicting that an ad would have a high CTR is more valuable than correctly predicting an ad would have a low CTR. In other words, the cost associated with a false negative is greater than the cost associated with a false positive. 

<br> Accordingly, accuracy was not a useful metric, but instead  Recall of the high CTR class was the key metric which the classifier was evaluated on. It should be stated that a high Recall (80 %), came at the expense of a low precision (41 %). 


**Cost-sensitive learning**
<br> A weighted RandomForest was used due to its ease of implementation and since promising results of such prediction models for rare event detection have been demonstrated [here](https://www.sciencedirect.com/science/article/pii/S235291482100174X#bib40). To produce the weightings, a cost-sensitive learning approach was taken. This strategy ensures that the classifier does not consider all errors to be equal. For this classifier, different costs were assigned to false negative and false positive events, which were used to produce a cost factor. The cost factor was then used along with the number of observations in both classes to estimate class weightings to be assigned to the classifier. The methodology followed was taken from [here](https://link.springer.com/article/10.1007/s10994-016-5572-x#citeas) (equation 2). Other classifiers should be attempted which employs the cost-sensitive learning e.g. calibrated AdaBoost.

**Results**
- High CTR class: Recall ca. 80%, Precision: 40%
- Low CTR class: Recall ca. 59%, Precision: 91%
- Feature importance order: 
    - Device type 
    - Time of day
    - Day of week


## Remarks
I have written the code shown in this repository for a client as part of Pivigo’s Science to Data Science bootcamp (S2DS; https://www.s2ds.org/) in March and April 2022. The approach to this project was formulated by a 4-member team which I was a part of.   
The names of the advertising firm (who is also the copyright holder), the advertiser, and the product, as well as the place where the campaign was run are kept anonymous.
Samara Sadeek, 16th May 2022

# Copyright
Program to predict click through rate of an ad and allocate a bid weighting to inform bidding strategy for a programmatic advertising firm.

Copyright (C) 2022  Anonymous

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program.  If not, see <https://www.gnu.org/licenses/>
