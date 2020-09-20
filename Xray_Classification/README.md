# Deep Learning & Pneumonia Detection


<img src="/Users/ericagabriel/Flatiron/Projects/Xray_Classification/intropic.png">

## Purpose
The scope of this project is to build a model that can classify whether a given patient has pneumonia, given a chest x-ray image. 

## Other Resources
#### Non Technical Presentation
https://www.youtube.com/watch?v=tO3uWGehqHg

#### Blog
**Technical:** https://medium.com/analytics-vidhya/computer-vision-and-pneumonia-detection-part-1-technical-4e3592de208b?source=friends_link&sk=665a349b71fc55dce132f6a28cfa5ef9

**Analysis:** https://medium.com/@gabriel.erica3/computer-vision-and-pneumonia-detection-part-2-analysis-6eec56d2cc69

## Case Background and Description of Data
The x-rays were provided by the Guangzhou Women and Children’s Medical Center in Guangzhou, China, on patients ranging from ages 1–5 years old. The image set contains images of “Normal”, “Viral” & “Bacterial” Pneumonia, classified into 2 categories: “Normal”and “Pneumonia”. There were 1341 Normal scans and 3875 Pneumonia scans. All unreadable and poor quality scans were removed prior to providing the dataset. In order to simulate  a real world scenario, I added 2534 additional images, and augmented them to reflect real world scenarios- blurry, distorted images, shifted/rotated images, and images that are zoomed in and out of focus.
Files: 
* Train- The set of images to be used for training
* Val- The set of "holdout" images used to tune and optimize the model(s)
* Test- The set of images used to validate the best performing model

<img src="/Users/ericagabriel/Flatiron/Projects/Xray_Classification/ZoomedXray.png">

## Explanation of Models
To execute this project, I built a binary Convolutional Neural Network from scratch, and relied on the metrics Accuracy, Loss, Recall, Precision, and F1 Score. In addition to the scratch model, the chest x-rays were also trained on a pre-trained model, **VGG16**, freezing all except for the last 4 layers.

### Best Model Using Validation Image Set: Model 6
* Number of Layers was reduced to 3
* Optimizer = Adam()
    * Learning Rate = 0.001
* Kernel Regularizer = L2
    * Learning Rate = 0.005
* Batch Size: 1000
* Epochs: 15
 

#### Model 6:  Loss vs. Epoch
<img src="/Users/ericagabriel/Flatiron/Projects/Xray_Classification/LossEpoch_valset.png">

#### Model 6:  Accuracy vs. Epoch
<img src="/Users/ericagabriel/Flatiron/Projects/Xray_Classification/ValAccEpoch_valset.png">

#### Model 6: Confusion Matrix
<img src="/Users/ericagabriel/Flatiron/Projects/Xray_Classification/ConfusionMatrix_valset.png">

#### Observations
The loss fluctuates at 2 epochs, then continues to decrease, and remains constant after 4 epochs. Here the loss converges which is what we want, however the training and validation accuracy does not converge. The model has a high bias and low variance. The final training loss and accuracy was 8.0386 and 0.495. The final validation loss and accuracy was 7.971 and 0.5.

### Final Model Using Test Image Set: Model 7
* Optimizer = Adam()
    * Learning Rate = 0.01
* Kernel Regularizer = L2
    * Learning Rate = 0.01
* Batch Size: 750
* Epochs: 11
 

#### Model 7:  Loss vs. Epoch
<img src="/Users/ericagabriel/Flatiron/Projects/Xray_Classification/LossEpoch_testset.png">

#### Model 7:  Accuracy vs. Epoch
<img src="/Users/ericagabriel/Flatiron/Projects/v/LossEpoch_testset.png">

#### Model 7: Confusion Matrix
<img src="/Users/ericagabriel/Flatiron/Projects/Xray_Classification/Confmatrix_testset.png">

#### Observations
The loss has increased between the traing and test set. The bias and variance in the model has increased, with the training accuracy being 0.50, and the testing accuracy is 0.375. The final loss for the training data was 8.0386 and the testing loss was 9.936. In upcoming projects, given the proper tech tools, I want to double the amount of images, increase the amount of hidden layers to reveal more features, and increase the size of the images to 150 x 150 so that the model is able to capture more features, and experiment with the neuron count. 

### Pre-trained Model Using Testing Image Set: Model 9
* Optimizer = Adam()
    * Learning Rate = 0.01
* Kernel Regularizer = L2
    * Learning Rate = 0.01
* Batch Size: 750
* Epochs: 11
 

#### Model 9:  Loss vs. Epoch
<img src="/Users/ericagabriel/Flatiron/Projects/Xray_Classification/Pretrain_LossEpochTest.png">

#### Model 9:  Accuracy vs. Epoch
<img src="/Users/ericagabriel/Flatiron/Projects/Xray_Classification/Pretrain_AccEpochTest.png">

#### Model 9: Confusion Matrix
<img src="/Users/ericagabriel/Flatiron/Projects/Xray_Classification/Pretrain_Confmatrix.png">

#### Observations
The results of the pretrained model, faired the same as the results from my final model. In addition to the improvements above, to improve upon this model, I will alter the neurons in the desne layers, and use feature extraction as a means of fine tuning. 

## Exploratory Data Analysis

### Question 1: What are the Pros and Cons of Using X-rays for Detection?

#### Findings
 **Pros:**
 * Fast way to view internal organs & and air-filled parts
* Inexpensive (For Medical professionals)
* Fast turnaround time on results

**Cons:**
* Images can be difficult decipher
* Can’t detect the type of bacteria or source
* Can be costly for patients:
    * With Health Insurance: $0 - $50 
    * Without Health Insurance: $200 - $400

X-rays in Guangzhou are done as apart of patient’s routine healthcare. Meanwhile the cost of x-rays in the US fluctauates by state. How can they afford to do so? What resources are needed to make this protocol available in the US? X-Ray exams for the Top-10 deadliest diseases should have set income based prices, and be offered free in the case of a Global Pandemic.


### Question 2: Can COVID be Detected via Chest X-Ray?
<img src="/Users/ericagabriel/Flatiron/Projects/Xray_Classification/CDC.png">

**Findings:**
Currently the primary method for testing COVID-19 is by administering a viral test/nose swab. Results can take days to return because often they must be sent to a lab for analysis. These labs can be located out of town and out of state. A negative result only means that you did not have Coronavirus *AT THE TIME* the priginal test was taken. A long term side effect of COVID-19 is pneumonia-induced lung injuries in both lungs. The CDC chart above shows the amount of COVID-19, Influenza, and Pneumonia related deaths from 2/1/2020 to 8/1/2020. It reveals that 44% of people who died from COVID-19 also had Pneumonia. Given the correlation between these 2 diseases, medical professionals should consider making chest x-rays a method to detect COVID-19.
 
 #### Question 3: Why aren't X-Rays Taken in Color?

 <img src="/Users/ericagabriel/Flatiron/Projects/Xray_Classification/3D_Color_Image.gif">

 The above gif is a 3D, color scan of an ankle. Its the first x-ray scan of color and was taken in 2018 by New Zealand Company, MARS Bioimaging. Their scanner is able to distinguish between bone, muscle, and fat. When will the rest of the world catch on to this technology? What's stopping us?
