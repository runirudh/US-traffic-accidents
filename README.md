# Predicting Accident Severity based on US Traffic data 

**data [link](https://www.kaggle.com/sobhanmoosavi/us-accidents/metadata)** from **kaggle**

### Aim : To analyze accident severity based on time, location, driving conditions attributes. 

Data has 50+ usable features - >

                                Original data has 4 severity levels, with most of the data in levels 2 & 3. 

                                For prediction, we have bundled levels 1 & 2 into Low category, and 3 & 4 
                                
                                into High category, as this skewing would affect the model's learning otherwise.
                                
                                

<img width="614" alt="Screen Shot 2022-01-15 at 9 58 33 AM" src="https://user-images.githubusercontent.com/96305841/149627920-44d26d81-62f8-4465-aa09-2acbc56d579f.png">
<img width="615" alt="Screen Shot 2022-01-15 at 9 58 39 AM" src="https://user-images.githubusercontent.com/96305841/149627934-3c2e62ee-c243-4523-8fb9-8cb39a40836d.png">

### Feature names:
<img width="601" alt="Screen Shot 2022-01-15 at 11 05 46 AM" src="https://user-images.githubusercontent.com/96305841/149628936-2613882d-381a-4182-bc42-16db64ac1474.png">


### Data Summary:

Summary shows the 2 new variables which we created at the end of the table to get more out of our features. 

                              1. ZipcodeLevels - Bins zipcode values to 10 bins 

                              2. time diff min - Time it took for accident to be marked clear. 
                              
                                                 created through time stamps of start and end time.  


<img width="942" alt="Screen Shot 2022-01-15 at 10 03 49 AM" src="https://user-images.githubusercontent.com/96305841/149627951-964cf550-ffbb-467d-ae21-d8b57c70bea0.png">

## Accident Data visualization for 2 severity levels:
<img width="565" alt="Screen Shot 2022-01-15 at 9 57 39 AM" src="https://user-images.githubusercontent.com/96305841/149628020-5e4b51a3-b5dc-4969-8200-625ed0ef6bd7.png">

## Data types of features:



## GGPairs for correlation between variables:
<img width="562" alt="Screen Shot 2022-01-15 at 9 58 15 AM" src="https://user-images.githubusercontent.com/96305841/149627982-c2cf2d0d-879a-4798-b336-907dfb8ea960.png">


### Random Forest results:

<img width="540" alt="Screen Shot 2022-01-15 at 9 57 58 AM" src="https://user-images.githubusercontent.com/96305841/149627963-a3e1eba0-99e4-459d-90e6-c39ed4c295be.png">

## Final GLM model:
#### after running stepwise and partial f tests on model with all the data, we arrive at this smaller, simpler model summarized below:
<img width="532" alt="Screen Shot 2022-01-15 at 9 59 34 AM" src="https://user-images.githubusercontent.com/96305841/149628054-09c0568d-fcee-4cdb-a9cb-08ee9c1caa20.png">

### Anova table for model:

<img width="581" alt="Screen Shot 2022-01-15 at 9 59 48 AM" src="https://user-images.githubusercontent.com/96305841/149628079-4f42f5fb-62e4-4579-8763-81836f088569.png">

### Model accuracy:
<img width="511" alt="Screen Shot 2022-01-15 at 10 51 52 AM" src="https://user-images.githubusercontent.com/96305841/149628159-9041b668-313e-4e18-8115-fcc289f1321e.png">

### AUC TEST showing predictive ability:

AUC Test is done for categorical predictions, which simply tests True positives vs False positive, i.e Sensitivity vs Precision 

by finding an f score. 

<img width="307" alt="Screen Shot 2022-01-15 at 10 00 02 AM" src="https://user-images.githubusercontent.com/96305841/149628124-aee85046-9058-4706-8ab0-6bd003674c5b.png">

                                We see model does not have great predictive ability. 
                                
                                A good model has value closer to 1. Null model would have accuracy 0.5
                                
                                Our model Area under curve value is 0.58 

### residuals 
<img width="462" alt="Screen Shot 2022-01-15 at 10 00 18 AM" src="https://user-images.githubusercontent.com/96305841/149628362-ce0edc9b-c9c2-4368-97af-f9c2e1cf7817.png">

### residuals after removing outliers: (does not affect model deviance, so good)

<img width="484" alt="Screen Shot 2022-01-15 at 10 00 35 AM" src="https://user-images.githubusercontent.com/96305841/149628376-191faab6-043b-47ec-ac1f-94895e3fe2c4.png">

### influence plot: 

<img width="548" alt="Screen Shot 2022-01-15 at 10 00 44 AM" src="https://user-images.githubusercontent.com/96305841/149628411-a31f936a-cc5f-469a-b197-1d24dd9e6e44.png">

## Final conclusions :  

                       1.
                       
                       2.
                       
                       3.
                       
                       4.
                       
                       5.
                       
                       



