# Image_recognition
Classifying and comparing the performance of different machine learning algorithms based on the data structures produced

Classify the symbols images using the choice of machine learning techniques in python.
1.Three classifiers used
Support Vector Machines (SVM) are supervised machine learning algorithms that analyse data for classification and regression. Datapoints are separated using a hyperplane with the highest margin and then finds the optimal hyperplane to classify unseen data and they are also known as discriminative classifier. Kernels are used to transform input data into the required form. The kernel is the main hyperparameter that can be tuned to meet the requirement of the type of dataset and output required. There are several types of kernel that can be used.

Random forest classifier (RF) was also used as another supervised learning used in both regression and classification problems. It is a meta estimator which fits a number of decision trees classifiers and take the average to predict accuracy. Taking the average predictions of the trees will protect from the individual errors making it highly accurate and robust. Since it takes the average of all the predictions, it avoids the problem of overfitting. However RF can be slow to generate due to multiple decision trees.

Artificial Neural Network: Artificial Neural Network (NN) is a supervised learning classification algorithm. It is known to be inspired by how the neurones work in a brain. Neurones are the basic component of NN. It is a type of machine learning where the computer can learn on the training data by performing deep learning and mostly used successfully in object recognition. When a large number of certain type objects are presented to NN, the computer learns from it and can successfully learn to categorise new images based on its learning. Training will include providing a large number of data with the corresponding output so the machine will learn to create the output on the new set of unseen data.

ANN architecture: In general there are three layers in ANN. The first layer is the input layer where the features are provided. The hidden layer will contain neurones that will fit the functions required to predict and is the bridge between the input and the output. The features are connected to all the neurones which make them fully connected. The final layer will be the output layer.

Convolutional Neural Network (CNN): Deep learning has been very popular in recent years and one of the great ways to use deep learning for image classification is using a convolutional neural network (CNN).CNN learns the internal features looking at both local and global features making them more efficient in image recognition. The first layer in CNN is always a convolutional layer to extract features from an imput image and the filters are feature identifiers. Stride is the number of pixel shifts over the input matrix. If the images are too big, pooling layer reduces the number of parameters. After the features identification, there is a fully connected layer at the end of the network where it takes an input volume and outputs an N dimensional vector where N is the number of classes. The convolutional layers detects the same patterns in different parts of the image and the pooling merges similar features. This makes them more efficient by being able to detect features anywhere.

2. How the test was run
Each dataset is an experiment. There are five experiments in total for five datasets. For each dataset, the the training and testing sets were split into 80:20 ratio with 80% of the data for training and 20% for testing for all experiments. However, this might not be the most efficient way due to sample variability int he training and testing sets. The training sets chosen could be biased and can give better prediction on training sets but not on the testing sets causing overfitting.

For bigger dataset, kfold cross validation could be used where the dataset is randomly divided into k folds. One of the folds is kept for testing and the rest for training which is repeated k times and each time the validation groups changes. This can be more unbiased and efficient method for prediction. I got errors when trying to do use kfold cross validation.

SVM: In these experiment linear kernel was used. Linear kernel is used as a product of two different observations. SVM classifier gives good accuracy and offer faster prediction. However, it might not be so useful for very large dataset and it does not work well when the classes are overlapping. Accuracy in percentage was chosen as the metrics.

RF: In these experiments, RF with 500 decision trees were used.Percentage accuracy was chosen as the metrics.

ANN: ANN was carried out using keras sequential (left to right) model. The first layer was the input layer. The dense layer contains the number of neurones and the activation units. In this experiments, for both pixel (pix) and class decomposed (pix_cd) datasets, Rectified Linear Unit (relu) with default settings was used. Relu is used in most neural networks and are computionally simpler compared to other sctivation functions.It can output a true zero value causing sparse representation which can speed up learning process and simplify the model (Krizhevsky et al., 2012). However, it might not be the most efficient when there are lots of layers.

The final layer is the output and contains the output value or class (39 for pix, hog, hog_ros and lbp dataset and 65 for pix_cd dataset) and softmax activation. Softmax makes sure that all probability values are between 0 and 1. In these experiments, only one hidden layer was used used but for more complex data layers can be added to increase the performance of the model.

There are several optimisers which can be used and are one of the hyperparameters that can be tuned. In this experiment, to compile the model, adam optimiser was used with default settings as described by Kingma and Ba (2015). I have tried to test other optimisers like 'rsmprop' in some cases.

Since our target labels were changed to categorical with more than two classes, categorical_crossentropy was used. The goal of the model building is to reduce the loss as much as possible. The metrics used was accuracy which measures how accurately, the model does the classification on the testing sets. Accuracy alone might not be a good indicator. The loss function should also indicate the loss decreasing. These hyperparameters can be changed and tuned to get the best model performance.

CNN: Since CNNs extract their own features, the original pixel dataset (pix) and the class decomposed pixels dataset (pix_cd) were used to run the CNN classifier. CNN architecture contained the input layer of the pixels which were (100 X 100); convolutional layer of 32 (5 x 5) filters or (3 X 3); relu activation; max pooling layer (2,2) followed by fully connected layer and an output layer with softmax activation function. Compilation of the model was used as in ANN and loss and accuracy was recorded. Hidden layer of 300 for pix data and 500 for pix_cd dataset was described by Elyan et al.(2018).
Results
Experiment 1 (pix dataset)

For the original pixels dataset, all classifiers were conducted. The SVM and RF gave an accuracy of 92.6% and 92.8% respectively. The accuracy results were not that different, so SVM and RF can both be used here. ANN for pix dataset gave an accuracy of 83.5%. In the training data the accuracy was 88% when using 5 epochs. 83.5% on the testing data is quite good. CNN gave an accuracy on the testing data was 87.6% with a loss of 0.6 even though the accuracy on training data was 99% with 5 epochs. SVM and RF seem to be the most efficient classifier for this dataset.

Experiment 2 (pix_cd dataset) Class decomposition (cd) is the process by which the labels are further classed into subclasses by applying kmeans clustering forming more classes. Class decomposition is normally done to solve the problem of low variance classification method. Having many subclasses should have increased efficiency of the models used by identifying hidden patterns within the classes.

Experiment 2 was conducted on pix_cd dataset with all classifiers. SVM and RF gave accuracy of 85% and 82% respectively. ANN gave an accuracy of 4.5% for pix_cd dataset. CNN gave an accuracy of 71.6%. For CNN, performance was lower (37%) when the n was 100. Accuracy was significantly increased to 71.6% when n was increased to 1000 using 5 X 5 filter. In addition the loss also went down. When 3 X 3 filter was used, performance of CNN also increased and gave an accuracy of 72 %. For pix_cd dataset, SVM and RF gave higher accuracies compared to other classifiers. However, various hyperparameters such as optimisers and activation functions could be tuned to increase the performance of the low performing classifiers. However, for ANN with pix_cd, even when changing the optimisers or N had no effect on accuracy. Lots of other hyperparameters could be tuned to make it perform better.

Experiment 3 (hog dataset) Histogram of Oriented Gradients (hog) is one of the feature descriptor used in image processing. This method is used for object detection. It extracts features out of the pixels. Hog descriptor and Linear support vector machine has been widely used to accurately train to classify objects (Dalal and Triggs, 2005).

Hog dataset was used to perform the classifiers except CNN. SVM and RF gave accuracy of 94.8% and 94% respectively. ANN gave an accuracy of 93.2% for hog dataset. Accuracy on the testing set was 100%. For this dataset, any of the classifiers is good in terms of prediction accuracy. Hog goes through the image and look at gradients and converts the image into feature vectors.

Experiment 4 (hog_ros dataset) Random oversampling is normally carried out for imbalanced data. Oversampling helps the minority data by duplicating the minority data to balance the classes. However, in some models, this might cause overfitting. Random oversampling also reduces the majority class but this might cause the important information to be lost.

For hog_ros dataset, SVM, RF and ANN was tested. Both SVM and RF gave an accuracy of 99.9%. ANN also gave accuracy of 99.9% on both training and testing dataset making all classifiers as the best performing one for this dataset. Random oversampling balances the classes by duplicating the minority class. This technique affects some machine learning algorithms and influence the fit of the model causing the overfitting of the model. Keeping record of the performance on training as well as testing data is useful in this context.

Experiment 5 (lbp dataset) Local binary patterns (LBP) is a method of texture or pattern descriptor where the pixels of an image are changed into binary patterns making them computationally efficient to work on (Ojala et al., 2002). Each pixel is compared to its neighbouring pixels and a local representation of texture is computed. This allows to capture very fine-grained details of the image which also has its own limitation.

For lbp dataset, SVM, RF and ANN was carried out. SVM gave an accuracy of 46.2% but RF performed well with 98.1% accuracy. Accuracy of lbp was 70% with ANN and did not change much when the optimiser was changed to ‘rmsprop’. Accuracy in training and testing data was also not much different. More parameter tuning and changing the number of epochs could have changed the accuracy for this classifier.

Conclusion
Conclusion In these experiment, it can be seen that for hog_ros dataset, any of the classifier can perform well with an accuracy of almost 100%. For all the classifiers and datasets, it is possible to improve the performance of the models by tuning the hyper parameters (optimisers, activation function and learning rates) and improving the validation framework. Splitting the datasets could be improved by further splitting the training sets into validation set to validate the model’s performance on unseen data or using k-fold cross validation and looking at performance on each fold. Other metrics such as error rates could also be useful in deciding the best classifier as accuracy alone cannot be the perfect measure of the performance. Other measures such as precision, sensitivity and specificity might also be useful and looking at the statistical significance of the accuracy and loss of each of the classifiers would also be important.


