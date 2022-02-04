# Predicting Accident Severity based on US Traffic data 

**data [link](https://www.kaggle.com/sobhanmoosavi/us-accidents/metadata)** from **kaggle**

### Aim : To analyze accident severity based on time, location, driving conditions attributes. 

Data has 50+ usable features. This analysis is done on a random sample of 200k values- >

       Original data has 4 severity levels, with most of the data in levels 2 & 3. 

       For prediction, we have bundled levels 1 & 2 into "Low" category, and 3 & 4 into
                                
       "High" category, as this skewing would affect the model's learning otherwise.
                                
                                

<img width="614" alt="Screen Shot 2022-01-15 at 9 58 33 AM" src="https://user-images.githubusercontent.com/96305841/149627920-44d26d81-62f8-4465-aa09-2acbc56d579f.png">
<img width="615" alt="Screen Shot 2022-01-15 at 9 58 39 AM" src="https://user-images.githubusercontent.com/96305841/149627934-3c2e62ee-c243-4523-8fb9-8cb39a40836d.png">

### Feature names:
<img width="601" alt="Screen Shot 2022-01-15 at 11 05 46 AM" src="https://user-images.githubusercontent.com/96305841/149628936-2613882d-381a-4182-bc42-16db64ac1474.png">


### Data Summary:

At the end of the table we see 2 variables which were created to get more out of our features. 

     1. ZipcodeLevels - Bins zipcode values to 10 bins 

     2. time diff min - Time it took for accident to be marked clear. 
                              
                        Created through time stamps of start and end time.  

<img width="506" alt="Screen Shot 2022-01-15 at 11 22 09 AM" src="https://user-images.githubusercontent.com/96305841/149629335-cd331eb2-24ea-4017-839c-cc5059f04bd3.png">


## Accident Data visualization for 2 severity levels:
<img width="565" alt="Screen Shot 2022-01-15 at 9 57 39 AM" src="https://user-images.githubusercontent.com/96305841/149628020-5e4b51a3-b5dc-4969-8200-625ed0ef6bd7.png">

## Checking NAs:

<img width="607" alt="Screen Shot 2022-01-15 at 11 03 55 AM" src="https://user-images.githubusercontent.com/96305841/149629054-7d8983a1-5fd2-4947-b10e-eff7d13b4394.png">

## Data types of features:
<img width="731" alt="Screen Shot 2022-01-15 at 11 05 12 AM" src="https://user-images.githubusercontent.com/96305841/149629061-322c6082-9fc6-405b-8c15-577386df766b.png">

<img width="685" alt="Screen Shot 2022-01-15 at 11 05 37 AM" src="https://user-images.githubusercontent.com/96305841/149629062-96c50599-25f1-47d5-9374-9e7de0b9b797.png">


## GGPairs for correlation between variables:
we find that wind chill and temparature are correlated and shouldn't be used in a model
together.

<img width="562" alt="Screen Shot 2022-01-15 at 9 58 15 AM" src="https://user-images.githubusercontent.com/96305841/149627982-c2cf2d0d-879a-4798-b336-907dfb8ea960.png">


### Random Forest results:

<img width="540" alt="Screen Shot 2022-01-15 at 9 57 58 AM" src="https://user-images.githubusercontent.com/96305841/149627963-a3e1eba0-99e4-459d-90e6-c39ed4c295be.png">

## Final GLM model:

after running **stepwise and partial f tests on model with all the data, we arrive at this Smaller, Simpler model** summarized below:

<img width="532" alt="Screen Shot 2022-01-15 at 9 59 34 AM" src="https://user-images.githubusercontent.com/96305841/149628054-09c0568d-fcee-4cdb-a9cb-08ee9c1caa20.png">

### Anova table for model:

<img width="581" alt="Screen Shot 2022-01-15 at 9 59 48 AM" src="https://user-images.githubusercontent.com/96305841/149628079-4f42f5fb-62e4-4579-8763-81836f088569.png">

### Model accuracy via Cross validation:
We get the same results splitting data into test-train manually (71.5%)

<img width="511" alt="Screen Shot 2022-01-15 at 10 51 52 AM" src="https://user-images.githubusercontent.com/96305841/149628159-9041b668-313e-4e18-8115-fcc289f1321e.png">

### AUC TEST showing predictive ability:

       AUC Test is done for categorical predictions, which tests True positives vs False positive.

<img width="307" alt="Screen Shot 2022-01-15 at 10 00 02 AM" src="https://user-images.githubusercontent.com/96305841/149628124-aee85046-9058-4706-8ab0-6bd003674c5b.png">

       We see model does not have great predictive ability. 
                                
       A good model has value closer to 1. Null model would have accuracy 0.5
                                
       Our model Area under curve value is 0.58 

### residuals 

<img width="462" alt="Screen Shot 2022-01-15 at 10 00 18 AM" src="https://user-images.githubusercontent.com/96305841/149628362-ce0edc9b-c9c2-4368-97af-f9c2e1cf7817.png">

       Looking at observations which produced outliers we see : 
       
       time.diffmin and visibility metrics for these data are > p = 0.95 , i.e extreme values.
          
- Removing these outliers and comparing old model

<img width="648" alt="Screen Shot 2022-01-15 at 11 36 06 AM" src="https://user-images.githubusercontent.com/96305841/149629887-a3e1c5ef-52a7-4ff6-815a-c78923147182.png">


### residuals after removing outliers: (does not affect model coefs or deviance, so it's allowed)

<img width="484" alt="Screen Shot 2022-01-15 at 10 00 35 AM" src="https://user-images.githubusercontent.com/96305841/149628376-191faab6-043b-47ec-ac1f-94895e3fe2c4.png">

### influence plot: 

- Points with high leverage (along x-axis) show more influence (size) than points with low leverage. 
- We see some fitted values have a large value for sqrt of cook's distance (size) and high residuals. 
- Not all leverage points are influential, only those that have high residuals.
- Adding weights to parameters using cooksd < 4/n * sample  &  residuals <3  worsens our model performance and plots. 

<img width="548" alt="Screen Shot 2022-01-15 at 10 00 44 AM" src="https://user-images.githubusercontent.com/96305841/149628411-a31f936a-cc5f-469a-b197-1d24dd9e6e44.png">



# Final conclusions from model summary :  

- Log odds of accident severity going from low to high, keeping all other independent variables constant,
  can be read from the coefficients of each predictor variable. 
  
- For categorical data this is in % change as levels change from base level.

- Model does not have a high utility. McFadden R^2 is very low, but the following trends were observed.

**1. Accident severity levels are high on interstate highways** 

<img width="687" alt="Screen Shot 2022-01-15 at 11 48 50 AM" src="https://user-images.githubusercontent.com/96305841/149630244-ed68ac86-14a3-468b-bdb3-382761251832.png">
                   
**2**. Most values are significant(p values) . Insignificant in Timezone level coefs could be explained by the skewing in timezone distribution.

  <img width="942" alt="Screen Shot 2022-01-15 at 10 03 49 AM" src="https://user-images.githubusercontent.com/96305841/149630616-981b252a-4d4e-40ff-b62a-268c695cb2c2.png">

  <img width="710" alt="Screen Shot 2022-01-15 at 11 56 34 AM" src="https://user-images.githubusercontent.com/96305841/149630584-36d665c8-7cf5-4027-9678-717012748dfb.png">
  
**3. zipcodelevels * side** - 

  **High severity cases** are more likely in zipcodelevels 2, 4, 5, 6 when **Driver drives on the Right (wrong) side of road**. 
  These zipcode levels are found in regions near Maryland(east), Kentucky (S.E) , Iowa (mid-W), Nebraska(mid-W) 
                       
**4. 1 min increase in time spent (accident) increases severity p by 0.002**
  
**5.** Time interval -  4 , 5, 6, i.e  10am - 10 pm  have a higher chance of accidents being severe as time interval changes from level ‘0’  i.e (10pm-12am)
     **This would mean that severe accidents occur more in the daytime than between the hours 10 pm to midnight.** 
  
**6. As Timezone changes from US/Central to US/Eastern** chances of severity being high increase by a 100% 

**7. Visibility beta is 0.97 i.e, as Visibility increases odds of severity (high) decrease**

