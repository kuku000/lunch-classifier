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
1.Resnet101v2
2.Xception
3.Effcientv2L
**4.Xception + Efficientv2L(main)**
5.Efficientv2L + Resnet50
![image](https://github.com/kuku000/lunch-classifier/assets/93827182/aa27ab33-91ad-4767-b5d3-3ec7ebd256b2)
## Parameter setting
batchsize: 64
initial learning rate: 0.01
epoch: 20
decay epochs: 5
decay factor: 0.1
loss function: categorical cross-entropy
Optimizer: Nadam[(Nesterov-accelerated Adaptive Moment Estimation)](https://keras.io/api/optimizers/Nadam/)
## Adjusting the loss function to address data imbalance issue
Using class weights to adjust the proportion of increased loss when different labels are misclassified.
![image](https://github.com/kuku000/lunch-classifier/assets/93827182/15a30790-a7fd-4839-a3d1-b03fec4d61bd)
![image](https://github.com/kuku000/lunch-classifier/assets/93827182/10a5c340-5311-4c48-a5f9-2f702a90e46b)
## Performance
	train	val
Loss	0.3285	0.4287
Top1 accuracy	89.07%	85.72%
Top5 accuracy	99.50%	99.02%

![image](https://github.com/kuku000/lunch-classifier/assets/93827182/6dc77901-c58d-4273-929b-e6f0c3999e4a)

