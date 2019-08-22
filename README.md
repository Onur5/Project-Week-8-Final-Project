<img src="https://bit.ly/2VnXWr2" alt="Ironhack Logo" width="100"/>

# Title of My Project
*[Onur Taskin]*

*[Data Analytics June 2019]*

## Content
- [Project Description](#project-description)
- [Dataset](#dataset)
- [Cleaning](#cleaning)
- [Model Training and Evaluation](#model-training-and-evaluation)
- [Conclusion](#conclusion)
- [Reason for the problems](#Reason-for-the-problems)
- [Future Work](#future-work)
- [Organization](#organization)
- [Links](#links)

<a name="project-description"></a>

## Project Description
Today millions of people, all around the world, communicate using sign language. While applications capturing the complex gestures and translate them to verbal speech would be very usefull for the community, the projects had limited success so far.

Especially, mobile application could be usefull in the everyday.  

Given the circumstances of the Ironhack bootcamp this project has to deliver results in less then a week.


### Thus, the short aim is to create first a model that identifies different alphabetic letters shown in sign language. Building a Convolutional Neural Network (CNN) in Keras, the model is meant to translate letters in real time.

### The created models are tested on live data


The longterm aim of this project is to create an mobile application that can fully read all hand gestures.

<a name="dataset"></a>

## Dataset

While Kaggle.com offers lots of different datasets (pictures of sign language letters and digits. ([link](https://www.kaggle.com/datasets?search=sign+lang)), the majority of this datasets is of low quality (according to the community).

    --> After an initial analysis an additional dataset was choosen to increase the accuracy of the model
        In the end both datasets were merged to train better models.

### The first Dataset

As first dataset, the one with the best documentation and highest score in terms of quality was chosen:
The choosen dataset for this project ([link](https://www.kaggle.com/datamunge/sign-language-mnist)) is an adjusted version of the original MNIST (Modified National Institute of Standards and Technology database) image dataset of handwritten digits, which is a popular benchmark for image-based machine learning methods.

- American Sign Language letter of hand gestures

- With 24 classes of letters (excluding J and Z due to motion requirement)

- Training dataset (27,455 cases) and test dataset (7172 cases)

- Format: 28x28 pixel image, with grayscale values (0-255)


Example of the original pictures before the grayscaling and resizing:

  ![Dataset 1 - Example for pictures](https://github.com/Onur5/Project-Week-8-Final-Project/blob/master/Bin/Dataset%201%2C%20example%20of%20pictures.png)

The second dataset is provided by the Kaggle community ([link](https://www.kaggle.com/datamunge/sign-language-mnist) includes drop-in replacements, which are more challenging for computer vision and original for real-world applications.

The dataset is in available as a CSV file with labels and pixel values in single rows.

### The second Dataset

The second dataset is provide by the kaggle community ([link](https://www.kaggle.com/datamunge/sign-language-mnist)). 

- 800 pictures for each letter

- the hand gesture frame is cutted and placed on a black background

- each picture of an hand gestures is rotated 10 times, to create 10 pictures 

- data quality low, as the rotation is done for each picture with very small rotation gaps and because the hand gestures are cutted

      --> After the preperation of the second dataset and the merge of the datasets there was total of more than 44k picture data to
        analyse
        
        
 Example of the original pictures before the grayscaling and resizing:
 
  ![Dataset 2 - Example for pictures](https://github.com/Onur5/Project-Week-8-Final-Project/blob/master/Bin/Dataset%202%2C%20example%20of%20pictures.png)
 
<a name="cleaning"></a>

## Cleaning

The cleaning process of the dataset has been made in two Jupyter Notebooks.

The first dataset was cleaned in the notebook "Code for first Dataset and Model.ypng"
and the second one in "Code for additional Dataset and Models.ypng".

In the following the cleaning for both databases is described:

### The first Dataset (preperation for the first CNN model)

As the first dataset was provided as a DataFrame there werent to many adjustments to be made on the data. In general no missing values or NaNs were available in the dataset.
To fit the data into a CNN  model the datasets shape had to be adjusted however.

The major adjustment steps on the dataset are:
  1. Transforming the DataFrame into an Array
  
  2. Resizing the Array into the picture format (27000, (28,28), 1)
    
    --> Here the 27k indicates the amount of picutres (the rows), the (28,28) the pixels 28x28 and the 1 represents the grayscaled color
  
  3. Standardize the color by dividing each value by 255
  
  
 Distribution of Dataset 1:
 
   ![Dataset 1 - Distribution](https://github.com/Onur5/Project-Week-8-Final-Project/blob/master/Bin/Distribution%20of%20first%20dataset.png)
  

 ----
### The second Dataset (preperation for the additional models)

As the second dataset was provided in the form of actual pictures the preperation was more complicated. 

The aim of the cleaning was to bring the data into the same form of the first dataset, so that they can be merged and finally fitted into a model.

The major adjustment steps on the dataset are:
  1. Importing the datasets as Arrays
  
  2. Smoothing the "pictures"
  
  3. Greyscaling the "pictures"
  
  4. Resizing the Array into the picture format (17000, (28,28), 1).

  5. Standardize the color by dividing each value by 255
  
  6. Merging the two datasets
  
    --> After the merge there was a total of 44k different "pictures" available that were used to fit into the model.


<a name="model-training-and-evaluation"></a>

## Model Training and Evaluation
In total three different models were created.

In the following a small explanaition of the training of the models and their accuracy is presented:


### The first Model
This model was trained with the first dataset.


The functions in the model are:
  - Three convolutional layer
  
  - Three max-pooling layer
  
  - Two density layer
  
The choosen hyperparameter are:
  - 20 Epochs
  
  - 128 Batch-Sizes
  
  - A test-size of 30% of the total dataset.
  
 
 
 Detailed Function and Parameter of Model 1:
 
   ![Model 1 - Functions and Parameter](https://github.com/Onur5/Project-Week-8-Final-Project/blob/master/Bin/Model%20with%20function%20and%20parameter.png)
 
    
     However the accruacy of the model on the 7k test data lies at about 88%.
 
 
 ### The second Model
 This model was trained with the merged dataset (44k different pictures).
 
 As the dataset is way more complicated the functions of the dataset are adjusted:
    - Increased amount of convolutional layers, with higher kernels
    
    - Increased amount of max-pooling layers
    
    - Increased amount of density layers
  
 The chosen hyperparameter are as follows:
   - 15 Epochs
  
  - 256 Batch-Sizes
  
  - A test-size of 30% of the total dataset.
 
 
  Detailed Function and Parameter of Model 2:
 
    ![Model 2 - Functions and Parameter](https://github.com/Onur5/Project-Week-8-Final-Project/blob/master/Bin/Model%202%2C%20with%20function%20and%20parameter.png)
    
    
  Perforemance of Model 2 over all Epochs:
  
  ![Model 2 - Perforemance over all Epochs](https://github.com/Onur5/Project-Week-8-Final-Project/blob/master/Bin/Model%202%2C%20perforemance.png)
  
    However the accruacy of the model on the 7k test data lies at about 56%.
 
 ### The third Model
 This model was trained with the merged dataset (44k different pictures).
 
 After the bad performance of model two the amount of layers and kernel sizes were again raised.
 But the pooling size were lowered to have better pictures:
 
    - More convolutional layers, with higher kernels
    
    - Smaller size of max-pooling layers
    
    - More density layers
 
 --> One of the most important changes in model 3 was to include a balanced split into test and train data, so that the learning is more accurate
 
 The chosen hyperparameter are as follows:
   - 20 Epochs
  
  - 128 Batch-Sizes
  
  - A test-size of 30% of the total dataset.
 

  Detailed Function and Parameter of Model 3:
 
    ![Model 3 - Functions and Parameter](https://github.com/Onur5/Project-Week-8-Final-Project/blob/master/Bin/Model%20with%20function%20and%20parameter.png)
    
    
  Perforemance of Model 3 over all Epochs:
  
  ![Model 3 - Perforemance over all Epochs](https://github.com/Onur5/Project-Week-8-Final-Project/blob/master/Bin/Model%203%2C%20perforemance.png)
  
  
       However the accruacy of the model on the 7k test data lies at about 89%.
       
  
<a name="conclusion"></a>

## Conclusion
Especially the final model, which was trained with a more complex datasets, shows a satisfying accuracy on the test data.

Using open cv2 the models were tested on live data.

THe code for this can be found in the jupyter nootboke "DEMO.ypng".

The pictures captured from the front camera of the laptop were smoothed, greyscaled, resized and analyzed by the model.
Many letters are recognized by the model.

However, the model is still far from perfect and needs alot of improvements.

At this stage it can be used to learn the sign language letters.

A test can be runned in the jupyter nootboke "DEMO.ypng", which asks for a specific letter and analyzes the live data until it recognizes the prefered picture

<a name="Reason-for-the-problems"></a>

## Reason for the problems

One reason for the bottlenecks of the model is the underlying dataset used for the training of the model:

### The datasets 
  - Especially the second dataset is of a very low quality
  
  - The first dataset provides only very small pictures which makes the learning harder
  
  - In general have the underyling pictures only a very low variety

### The model itself:
  - Not enough time to optimize the Hyperparameters
  
  - Lack of knowledge and ressource to use the perfect Layers
    --> f.e. Pool-Size still too high

<a name="future-work"></a>

## Future Work

### For the current models there are some ideas to overcome the problems:
  - Collection of more and better diversified datasets through the Community
  
  - Optimization of the Variables (Better Ressource/Computers needed)
  
  - Model still is a "cluster-model". Have to be changed to work with probabilities

### For the long-term aim of the model
   - Analyze total gestures of hands
   
      --> Starting point for this is the frequently used “Hand Keypoint Detection“ technic.


<a name="organization"></a>

## Organization
The organization was mainly done on a [handwritten calendar](https://github.com/Onur5/Project-Week-8-Final-Project/blob/master/Bin/d7e6a758-0dfd-451b-827f-e30f8b3a0152.png)) and later adopted to ([Trello](https://trello.com/b/COrcTYwq/final-project))


<a name="links"></a>

## Links
[Repository](https://github.com/Onur5/Project-Week-8-Final-Project)  
[Slides](https://docs.google.com/presentation/d/1DMK8wsLhHhNOS47d6kyafDe96Er8a5RlWn0ecVaFwjY/edit?usp=sharing)  
[Trello](https://trello.com/b/COrcTYwq/final-project)  
