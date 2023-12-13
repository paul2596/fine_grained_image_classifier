# Fine-Grained Classification
## Preprocessing:

The dataset was split into a train and test set based on the is_train Boolean value provided. Further, a validation set was taken from the training dataset with a split ratio of 9:1. The images were normalized using the maximum pixel value of 255. For data augmentation a zoom range of 0.2 was used with random horizontal flip and random rotation range of 25. The batch size taken was 32. The images were resized to 299x299 to match the input layer of Xception architecture.

## Modelling: 

Different models were considered for the fine-grained task initially InceptionV3 and Bilinear-CNN using 2 VGG16 were tried out but I could not effectively reduce the overfitting. Further, Xception model which uses depthwise separable convolution layers which has lesser parameters to compute and is less prone to overfitting. The base model used was a Xception model initialized with pretrained weights from ImageNet followed by a Fully connected layer that consists of a dense layer of 1024 units with relu activation, a dropout layer was used to reduce overfitting and connected to an output layer with a size of 200. An SGD optimizer was used to progress towards minimal loss. 
## Training and Hyperparameter Tuning: 

Initially all the layers of the based model were frozen, and the fully connected layer was tuned for 30 epochs starting with a learning rate of 1e-2 and reducing at 10th and 15th epoch by 0.1 to reduce overfitting. Once the features were extracted using the pretrained weights, all the layers were made trainable with learning rate 1e-3 and a gradual weight reduction. Different experiments were carried out to tune the model such as changing the activation function to swish and tanh. The dropout value was altered to increase the random noise so new values can be learned. Adam was the first choice for optimizing the loss, but SGD performed better and had better control to progress towards the minima by altering the momentum and learning rate

## Evaluating Results:
![image](https://github.com/paul2596/fine_grained_image_classifier/assets/71576923/e2bdc5b2-0dc4-4e2d-ba05-504fd8656692)

From the table above, we see the f1-score 
is 0.77, indicating the false 
positives are low, and this can be 
noted from the precision value, 
which is 0.77. The average recall for 
multiple classes is 0.77

![image](https://github.com/paul2596/fine_grained_image_classifier/assets/71576923/49f8d1a7-d337-4621-b4ea-5e840d4fcfae)

From the heatmap of the confusion matrix above we can see that the number of misclassifications is less. We can see that 
there are few clusters of misclassifications such as the one near 141. This could be because of the close feature 
relation between these sets of species with minimal feature differences
