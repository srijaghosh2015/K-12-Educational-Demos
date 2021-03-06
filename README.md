# K-12-Educational-Demos
K-12-AI-Demos| Doodle Net Drawing Classifier

It is a web-based application that recognizes the drawings of cat, sheep, dog, bear, cow, and triangle made on canvas.

Dataset

The data used is taken from the Quick Draw Dataset that is in NumPy format that is pre-processed to 28*28 grayscale images . Subset of this dataset has been used i.e., 50000 images for every class (total 6 classes). 


<img src="readMePictures/pic0.png">

Data is split into training and testing in 60and 40 ratios respectively.


<img src="readMePictures/pic1.png">

Data is loaded as shown below:

<img src="readMePictures/pic2.png">

Labels are added for all the classes in following way:

<img src="readMePictures/pic3.png">

Print some of the drawings for each class to see how they look. 

<img src="readMePictures/pic4.png">

It would give output similar as below:

<img src="readMePictures/pic5.png">

<img src="readMePictures/pic6.png">

<img src="readMePictures/pic7.png">

Data is merged for all the classes together taking 50000 images for each class and data is shuffled.

<img src="readMePictures/pic8.png">

Divide this data in two different arrays X consisting of pixel data and Y consisting of labels.

<img src="readMePictures/pic9.png">

Split the dataset into training dataset and testing dataset 

<img src="readMePictures/pic10.png">

Images are normalized, so that values are between 0 and 1 to make the training easier

<img src="readMePictures/pic11.png">

Reshape the images to 28*28 size

<img src="readMePictures/pic12.png">

Training Model
 It is a type of classification problem where there are 6 classes - cat, sheep, dog, bear, cow, and triangle and one class is predicted when an image is drawn on the canvas.

Model has been trained using CNN model with Keras and then converted into model. Json file using tensorflow.js converter.
Keras is a deep learning API written in Python, running on top of the machine learning platform TensorFlow. 


CNN Model(Convolution Neural Network Model) – 10 layers are added to train this model
First is Convolution layer with 64 filters of 5*5 size and activation function is ReLU(Rectified Linear Unit)
Max Pooling Layer is added with pool size of 2*2.(It is used to compress the image)
Another is Convolution layer with 64 filters of 3*3 size and activation function is ReLU(Rectified Linear Unit)
Max Pooling Layer is again added with pool size of 2*2
Convolution layer with 128 filters of 3*3 size and activation function is ReLU(Rectified Linear Unit) is added
Max Pooling Layer is added with pool size of 2*2
Flatten Layer is added to flatten the square images into 1 dimensional
Another Layer is Dropout Layer with probability of 0.2
Dense Layer (Fully Connected Layer) is added with 256 neurons and ReLU activation function
Output Layer/Softmax Layer is added where number of neurons is equal to number of classes i.e., 6 (Softmax Layer will take probabilities for each class and choose the one with the highest probability)





Model is defined in following way:

<img src="readMePictures/pic13.png">


Model is compiled in following way:

<img src="readMePictures/pic14.png">

Print the summary of model in following way:

<img src="readMePictures/pic15.png">

Summary for the model will be printed in this way:


<img src="readMePictures/pic16.png">

Model is fit in following way:

Here, the neural network will learn the relationship between X and y where X is the pixel data for drawings and y is the label for all the images . Epoch is equal to 20 as accuracy is not increasing after that, and batch size is 200

<img src="readMePictures/pic17.png">

Evaluation of model is done in following way:

<img src="readMePictures/pic18.png">

Accuracy can be printed in following way:

<img src="readMePictures/pic19.png">

Accuracy for this model is 92.13%

<img src="readMePictures/pic20.png">

Prediction can be made as shown below:

<img src="readMePictures/pic21.png">

model.predict returns the probability for each class and argmax returns the class with the highest probability.

Accuracy can also be calculated in following way:

<img src="readMePictures/pic22.png">


Print the confusion matrix as shown below:

<img src="readMePictures/pic23.png">

Confusion matrix describes the performance of the model. It is a matrix that contains the count of correct and incorrect predictions made by the model. It will be printed similar to the below image:

<img src="readMePictures/pic24.png">

Classification report can be printed in following way:

<img src="readMePictures/pic25.png">

Classification report will return the classification metrics like precision, recall and F-1 score. It will be printed as shown below.

<img src="readMePictures/pic26.png">

Model is first saved as keras.h5. The Keras.h5 file contains the model’s architecture, weights values and compile information. 
It is then converted to .json format using tensorflow.js converter in the following way so that it is compatible with the javascript code.

<img src="readMePictures/pic27.png">

The code above will create a folder entitled model, which holds a file called class_names.txt, which contains all of the classes that a sketch can be classified as. The folder also contains a file entitled group1-shard1of1.bin. The file is utilized in our model.json (Javascript Object Notation) which is also stored in our model folder. 


Our website utilizes basic HTML and JS. It must be noted that all of this JS code was graciously made open source by yining1023 in her doodleNet file. Big thanks to her. 

More specifically, this project uses a JS library called p5.js, a platform that has a variety of artistic capabilities and functions. Here are a few of the functions used in this project:

createCanvas() creates a canvas for the user to draw on.

<img src="readMePictures/pic28.png">

background() will set the background of the canvas to a specific rgb value. In the code below, our clear button is effectively erasing the doodles on the canvas by setting the color of the whole canvas.

<img src="readMePictures/pic29.png">

To load our local json model into the javascript, we use the following function:

<img src="readMePictures/pic30.png">

In order for the user’s doodle to be properly passed in and identified by our keras model, we need to format it in a very specific way. yining1023 resized the doodle into a 28 x 28 format. This is so that the images are compatible with our model, which was also trained on datasets containing 28 x 28 pictures.

<img src="readMePictures/pic31.png">

loadPixels() is a p5.js function which stores the image pixel data into a pixels array. From here, the data is converted into yet another format, which is stored in an array labeled inputs. Variables onePix contains a value between 0 and 1 (rather than the traditional 0-255). The pixel value is appended to oneRow. When a full row is completed, meaning the length of oneRow is 28, it is appended to inputs. 

<img src="readMePictures/pic32.png">

Here is an example of the inputs array. It will continuously update as the user draws:

<img src="readMePictures/pic33.png">

After the doodle has been formatted properly, our json model can now use it to predict different classes:


<img src="readMePictures/pic34.png">

guess array contains an array with the different probabilities of each class (essentially displaying our keras model softmax layer)

<img src="readMePictures/pic35.png">


In order to display these probabilities and their corresponding classes on the front end, a CLASSES array is initialized:

<img src="readMePictures/pic36.png">

Then for each element in the CLASSES array, its probability is stored:

<img src="readMePictures/pic37.png">


Something to keep note of is that the order of elements in the CLASSES array may cause computational bias when allocating probabilities.
