# lunch-classifier
## Dataset
### Fifty most often cuisine in Taiwan school meal:
The training set consists of 27,903 samples, further divided into an 80:20 ratio for training and validation sets.  

There are 7,002 samples in the test set.  

Additionally, there is a small training set of 200 sets, each containing 50 samples, intended for fine-tuning testing.
![image](https://github.com/kuku000/lunch-classifier/assets/93827182/1e362b93-d538-41fd-a9ce-b6e523e63d9d)

## Data preporcessing
Using the ImageDataGenerator, resize all photos to 300x300 and perform augmentation on the training data.
## Models
1. Resnet101v2  

2. Xception  

3. Effcientv2L  

**4. Xception + Efficientv2L(main)**  

5. Efficientv2L + Resnet50  

### Unfreeze layers setting: 
* Xception last 10 layers
* Efficientv2L last 7 layers


![image](https://github.com/kuku000/lunch-classifier/assets/93827182/aa27ab33-91ad-4767-b5d3-3ec7ebd256b2)
## Parameter setting
* batchsize: 64  

* initial learning rate: 0.01  

* epoch: 20  

* decay epochs: 5  

* decay factor: 0.1  

* loss function: categorical cross-entropy  

Optimizer: Nadam[(Nesterov-accelerated Adaptive Moment Estimation)](https://keras.io/api/optimizers/Nadam/)  


## Adjusting the loss function to address data imbalance issue
Using class weights to adjust the proportion of increased loss when different labels are misclassified.  

![image](https://github.com/kuku000/lunch-classifier/assets/93827182/10a5c340-5311-4c48-a5f9-2f702a90e46b)
## Performance
### Test set:
* accuracy: 84.604%  

* prediction time per photo(300*300): 0.015s  

![image](https://github.com/kuku000/lunch-classifier/assets/93827182/2184da62-17b0-4dc1-ae3d-7e40e050e319)  

![image](https://github.com/kuku000/lunch-classifier/assets/93827182/6dc77901-c58d-4273-929b-e6f0c3999e4a)  

##  Discussion
### Confusion Matrix
![image](https://github.com/kuku000/lunch-classifier/assets/93827182/fef2ccc0-96e1-46e9-a2ca-dfee2668a86e)  

Unable to effectively distinguish between rapeseed(油菜), komatsuna (小松菜), and Chinese spinach(青松菜)。  

![image](https://github.com/kuku000/lunch-classifier/assets/93827182/d7e6a439-5fd2-4285-9388-42c19a5dfb5b)  


### Classification Report
![image](https://github.com/kuku000/lunch-classifier/assets/93827182/741fa9dd-a595-4940-86a6-6ec287280d23)

It is difficult to distinguish between Satay Beef Slices, Sliced Pork with Garlic Sauce, and Black Pepper Pork.
Fushan lettuce: With a small amount of data, precision (TP / TP + FP) is easily influenced.

### Model Performance Comparison
![image](https://github.com/kuku000/lunch-classifier/assets/93827182/36d9077b-70b6-4957-a4a3-68f676275edd)

### How does fine-tuning perform with a small dataset?
Selecting 200 images randomly for each label from the large supplementary dataset to create a small dataset, totaling 10,000 images (8,000 for training and 2,000 for validation).  

Experimental setups:  

1. Unfreeze top 7 layers for EfficientNet and top 10 layers for Xception.  

2. Unfreeze top 3 layers for EfficientNet and Xception.  

3. Freeze all layers except the final fully connected layer.  


#### Results (Test):
* EFF 7 layers, Xception 10 layers accuracy: 83.81%
* EFF 3 layers, Xception 3 layers accuracy: 83.9%
* All Freeze accuracy: 83.73%

It may be related to the imbalance in the test data itself, or it could be due to the suboptimal extraction of the small dataset.
