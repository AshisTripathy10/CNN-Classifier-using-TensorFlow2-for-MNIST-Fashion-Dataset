Introduction: In this project, we use the Fashion-MNIST dataset, containing 60,000 training images and 10,000 test images of Zalando's fashion items, to classify different fashion products. Each image is a 28x28 grayscale picture labeled with the type of fashion article it represents. To achieve this, we build a Convolutional Neural Network (CNN), a specialized deep learning model designed to automatically learn and recognize patterns and features in images by processing them through multiple layers. We use TensorFlow 2, an advanced framework for developing and training deep learning models, which helps us efficiently implement and optimize our CNN

Importing the Modules: We import numpy for numerical operations and tensorflow for deep learning. We also import keras from TensorFlow, which provides high-level APIs for building and training neural networks. Matplotlib.pyplot is imported for plotting and visualizing our data. Finally, we set the random seed for both NumPy and TensorFlow to ensure that our results are reproducible.

Loading the Dataset: We get the Fashion-MNIST dataset module from Keras using keras.datasets.fashion_mnist. We load and sort the data into training and test sets with the load_data() function. We then check the shape of the training dataset, which shows that it contains 60,000 grayscale images, each with a size of 28x28 pixels.

Splitting the Data: We display an image from the dataset using plt.imshow, which shows an "Ankle Boot," and confirm its label as 9. We then slice the first 55,000 samples from X_train_full to create X_train, and the corresponding labels are stored in y_train. The remaining samples are assigned to X_valid and y_valid, creating our validation dataset. Finally, we print the shapes of our datasets, revealing that X_train has 55,000 images, X_valid has 5,000 images, and the test set X_test contains 10,000 images.

Normalizing the Features: We first compute the mean (X_mean) and standard deviation (X_std) of X_train along the axis=0, while preserving the shape of the data. We then normalize X_train, X_valid, and X_test by subtracting the mean and dividing by the standard deviation to standardize the pixel values. A convolutional layer in a neural network expects inputs in four dimensions: batch size (the number of images processed at once), height and width (the dimensions of each image), and channels (the number of color channels, which is 1 for grayscale images). We adjust our data by adding a new axis with np.newaxis to meet this requirement. This transformation converts our data into a shape suitable for the convolutional layer, with dimensions (55,000, 28, 28, 1) for training, (5,000, 28, 28, 1) for validation, and (10,000, 28, 28, 1) for testing.

Building and Fitting the Model: We import the partial function from functools to create a customizable version of keras.layers.Conv2D, which we name DefaultConv2D. By setting default parameters like kernel_size=3, activation='relu', and padding='SAME', we allow flexibility to adjust these parameters later if needed. We then use DefaultConv2D along with other layers, such as keras.layers.MaxPooling2D and keras.layers.Dense, to build a convolutional neural network (CNN) model. This model starts with a convolutional layer using DefaultConv2D with 64 filters and a kernel size of 7, followed by several more convolutional layers, pooling layers, and fully connected layers, ending with a softmax output for classification. The model is compiled with sparse_categorical_crossentropy loss, the nadam optimizer, and accuracy as a metric. Finally, we train the model using the fit method on X_train and y_train, validating on X_valid and y_valid.

Evaluating the Model Performance: We use model.evaluate on X_test and y_test to measure the test data prediction accuracy, which yields an accuracy of approximately 0.886. We then select 9 test samples starting from index 10, slice these samples from X_test into X_new, and obtain predictions using model.predict. The predicted classes for these samples are extracted using np.argmax, and the output shows the predicted classes as [4 5 7 3 4 1 2 4 8]. We also compare these predictions with the original classes from y_test, which are [4 5 7 3 4 1 2 4 8].
