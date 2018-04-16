---
layout: page
title: Project Details
subtitle: Information about the breast cancer detection algorithm
---



### Context and Motivation

About 12% of women will develop breast cancer over the course of her lifetime. According to a 2011 medscape article, 52% of malignancies are missed on the mammography and more than 25% of those missed are due to human error. We aim to augment the trained eye of medical doctors with image predicting techniques.

Our target audience for our image processing technique is medical doctors to aid them in breast cancer detection. We hope that medical doctors can supplement their detection methods of the naked eye with our algorithm.



### Scope

Ultimately, the goal is to save lives. In 2018, an estimated 266,120 new cases of breast cancer will be diagnosed and about 40,920 women will die from it. This tool will aid in the early diagnosis of breast cancer which is very important. More than 90% of women diagnosed with breast cancer at the earliest stage survive their disease for at least 5 years compared to around 15% for women diagnosed with the most advanced stage of disease (http://www.cancerresearchuk.org).

### Dataset

Images from the Curated Breast Imaging Subset of Digital Database for Screening Mammography (CBIS-DDSM). They include 3,103 mammogram image examples with two different views:
* Cranial-Cuadal (CC): Exposure taken from above
* Mediolateral-oblique (MLO): Exposure from the side at an angle

<br> The data contain 3,672 tissue abnormality examples which are split between calcifications and masses:
* 1,872 identified calcifications
* 1,696 identified masses

<br>Each abnormality includes a cropped image of the abnormality and a mask indicating the location in the full mammogram image

#### Abnormality categories and labels

Each of the abnormalities is rated in several categories:<br>
**Calcifications:**
* Type: Amorphous, Pleomorphic, Punctate, Dystrophic, Vascular, etc.
* Distribution: Clustered, Linear, Regional, Diffusely Scattered, etc.
* Assessment: 0 - 5 (Integer)
* Pathology: Benign, Benign With Callback, Malignant
* Subtlety: 1 - 5 (Integer)

**Masses:**
* Shape: Oval, Irregular, Round, Lymph Node, Focal Asymmetric Density, etc.
* Margin: Spiculated, Ill Defined, Circumscribed, Obscured, Microlobulated, etc.
* Assessment: 0 - 5 (Integer)
* Pathology: Benign, Benign With Callback, Malignant
* Subtlety: 1 - 5 (Integer)


### Data Processing


Our dataset came from cancerimagearchive.net, which was about 165 GB of data. This was ~2700 mammogram images, with mask images, for a total of 6000 images. The mask images to help researchers identify where cancer did occur in the image. The images needed to be converted from DICOM format to a more friendly format, and we selected png. These png images were cropped into 224x224 pixel images resulting in millions of images. Anything with a near black background was then filtered out so we would only train our model on actual tissue. There is large proportion of the images not containing cancer, and we decided to only keep a 1:5 ratio of positive to negative images.

The total dataset is 147,442 224x224 images. Then we applied Contrast Limited Adaptive Histogram Equalization from OpenCV to increase the contrast within images. Finally we sorted them into training, validation, and test datasets with an 8:1:1 ratio. Due to the size of the dataset, the data was loaded memory incrementally during training, using the built-in “flow from directory” functionality of Keras and Tensorflow.


### Cloud Computing

With our dataset ready, we pushed it to SoftLayer’s S3 object storage. We all ended up using different cloud compute environments based on the credits that we had from remaining classes. We didn’t find that any were more helpful than others other than Google “Colaboratory” let you share a jupyter-like notebook, but with the shared document functionality of google docs as well as a GPU computer. Unfortunately, Softlayer doesn’t support GPUs on Ubuntu, requiring you to take additional steps to get it running. We trained a multitude of configurations including our own architectures, but ultimately settled on a pre-trained architecture called mobilenet. We chose this one because it was a lot lighter than the others, but hadn’t sacrificed much for accuracy. In the future, with more time and compute resources, we might switch to a more robust pre-trained model.  After 1 epoch through the data, we opened all layers up to training, which helped us out of our accuracy plateau around 67% accuracy.

### Results

The accuracy in the test set is 0.79. <br>

#### Confusion Matrix

|                      | True Positive | True Negative |
|----------------------|---------------|---------------|
| Predicted   Positive | 681           | 293           |
| Predicted   Negative | 904           | 3842          |
|                      |               |               | 
<br>

| Confusion Matrix Analysis          |       |   
|------------------------------------|-------|
| Sensitivity                        | 0.43  |
| Specificity                        | 0.929 |
| Precision                          | 0.699 |
| Negative   Predictive Value        | 0.81  |
| False   Positive Rate              | 0.071 |
| False   Discovery Rate             | 0.301 |
| False   Negative Rate              | 0.57  |
| Accuracy                           | 0.791 |
| F1   Score                         | 0.532 |
| Matthews   Correlation Coefficient | 0.427 |

<br>

### Evaluation

The model is significantly better than a coin flip but we cannot say it is highly accurate. The lack of accuracy is mostly false positives, which is okay for our purposes because this is a failsafe for doctors. We are light years away from replacing the naked eye. There is often a trade off in modeling between precision and recall. In this model, our recall is good but our precision is poor. Recall is more important in this case. In other words, we can either reduce false negatives or reduce false positives. It is better to reduce false negatives because we don't want a doctor getting a negative and then not looking carefully at the xray when there actually is a tumor. On the other hand, when the model flags it as positive, it would be a call to the doctor to look at it really carefully and then make the final call.

<br>We attempted many tweaks to the model, these included adjustments such as using pretrained models, different layers, different numbers of nodes, adjustments to dropout and batch size only resulted in marginal improvements.

### Challenges

* The amount of data was significant and required GPUs to train in a reasonable amount of time.
* Segmenting the image files was time consuming and limited experiments with different segment sizes.
* Grayscale images decreased the efficacy of pretrained ImageNet models
* Diffuse edges of features in the images further eroded efficacy of pretrained models











