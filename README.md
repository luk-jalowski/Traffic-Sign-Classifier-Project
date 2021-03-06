# Traffic-Sign-Classifier-Project
Convolutional neural network capable of classifying german traffic sign images

## Writeup


**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

* The size of training set - 34799
* The size of the validation set - 4410
* The size of test set - 12630
* The shape of a traffic sign image - 32x32x3
* The number of unique classes/labels in the data set - 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set.
Distribution of examples per label in:
* Train set 
![alt text](./example_images/trainLabels.png)

* Test set
![alt text](./example_images/testLabels.png)

* Valid set
![alt text](./example_images/validLabels.png)

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

I decided to convert the images to grayscale and then normalize it.
* Original image
![alt text](./example_images/sign.jpg)
* After grayscaling
![alt text](./example_images/signGrayscale.jpg)
* After normalizing
![alt text](./example_images/signNormalize.jpg)

### To generate additional data I decided to add more examples to classses with the lowest number of examples. 
To add more data I'm augmenting existing data by scaling it and then translating the image in x and y axis by -5 to 5 pixels. 

* Effects of random scaling
![alt text](./example_images/signScaled.jpg)

* Effects of random translating
![alt text](./example_images/signTranslate.jpg)

* "Enhanced" image, after grayscaling and normalizing and then translating and scaling
![alt text](./example_images/signFinal.jpg)

#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

1. 5x5 convolution (32x32x1 in, 28x28x48 out)
2. ReLU
3. 2x2 max pool (28x28x48 in, 14x14x48 out)
4. 5x5 convolution (14x14x48 in, 10x10x96 out)
5. ReLU
6. 2x2 max pool (10x10x96 in, 5x5x96 out)
7. 3x3 convolution (5x5x96 in, 3x3x172 out)
8. 2x2 max pool (3x3x172 in, 2x2x172 out)
9. Flatten
10. ReLu
11. Fully connected layer (688 in, 84 out)
12. ReLu
13. Dropout layer
14. Fully connected layer (84 in, number of classes(43))


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used:
* Adam optimizer
* number_epochs: 10
* batch_size: 128
* learning_rate: 0.001
* Keep probability: 50%

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* test set accuracy of 95.4%
* validation set accuracy of 97.8% 

If an iterative approach was chosen:
1. What was the first architecture that was tried and why was it chosen?
* I've started with LaNet architecture.
2. What were some problems with the initial architecture?
* It only got around 70% accuracy on validation set.
3. How was the architecture adjusted and why was it adjusted? Typical adjustments could include choosing a different model architecture, adding or taking away layers (pooling, dropout, convolution, etc), using an activation function or changing the activation function. One common justification for adjusting an architecture would be due to overfitting or underfitting. A high accuracy on the training set but low accuracy on the validation set indicates over fitting; a low accuracy on both sets indicates under fitting.
* At first I've tried adding 3x3 convolutional layer and one more fully connected layer, but accuracy went down after. Then I've removed previously added fully convolutional layer and accuracy went up to above 90%. 

If a well known architecture was chosen:
1. What architecture was chosen?
* I've chosen LaNet architectture.
2. Why did you believe it would be relevant to the traffic sign application?
* It's a well known and reliable architecture for image classification.
3. How does the final model's accuracy on the training, validation and test set provide evidence that the model is working well?
 

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text](./my_signs/1.png) ![alt text](./my_signs/2.png) ![alt text](./my_signs/3.png) 
![alt text](./my_signs/4.png) ![alt text](./my_signs/5.png) ![alt text](./my_signs/6.png)

* None of this signs really stand out, but on two of these images there is a lower part of different sign in the frame.

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

The model was able to correctly guess all the traffic signs.

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)


![alt text](./example_images/Sign1Pred.PNG)

![alt text](./example_images/Sign2Pred.PNG)

![alt text](./example_images/Sign3Pred.PNG)

![alt text](./example_images/Sign4Pred.PNG)

![alt text](./example_images/Sign5Pred.PNG)

![alt text](./example_images/Sign6Pred.PNG)


* Model was able to correctly predict 5/6 images with 100% accuracy. Only exception was "No vehicles" sign, where model was only around 60% sure what sign it is.

