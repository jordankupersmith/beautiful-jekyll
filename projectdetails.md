---
layout: page
title: Project Details
subtitle: Information about the breast cancer detection algorithm
---



### Context and Motivation

About 12% of women will develop breast cancer over the course of her lifetime. According to a 2011 medscape article, 52% of malignancies are missed on the mammography and more than 25% of those missed are due to human error. We aim to supplement the naked eye of medical doctors with image predicting techniques
Our target audience for our image processing technique is medical doctors to aid them in breast cancer detection. We hope that medical doctors can supplement their detection methods of the naked eye with our algorithm



### Scope

Ultimately, the goal is to save lives. In 2018, an estimated 266,120 new cases of breast cancer will be diagnosed and about 40,920 women will die from it. This tool will aid in the early diagnosis of breast cancer which is very important. More than 90% of women diagnosed with breast cancer at the earliest stage survive their disease for at least 5 years compared to around 15% for women diagnosed with the most advanced stage of disease (http://www.cancerresearchuk.org).

### Data

Images from the Curated Breast Imaging Subset of Digital Database for Screening Mammography (CBIS-DDSM). They include 3,103 mammogram image examples with two different views: 
*Cranial-Cuadal (CC): Exposure taken from above
*Mediolateral-oblique (MLO): Exposure from the side at an angle

<br> The data contain 3,672 tissue abnormality examples which are split between calcifications and masses:
*1,872 identified calcifications
*1,696 identified masses

<br>Each abnormality includes a cropped image of the abnormality and a mask indicating the location in the full mammogram image

#### Abnormality categories and labels 

Each of the abnormalities is rated in several categories:
&nbsp;Calcifications
&nbsp;&nbsp;*Type: Amorphous, Pleomorphic, Punctate, Dystrophic, Vascular, etc.
&nbsp;&nbsp;*Distribution: Clustered, Linear, Regional, Diffusely Scattered, etc.
&nbsp;&nbsp;*Assessment: 0 - 5 (Integer)
&nbsp;&nbsp;*Pathology: Benign, Benign With Callback, Malignant
&nbsp;&nbsp;*Subtlety: 1 - 5 (Integer)

Masses
&nbsp;*Shape: Oval, Irregular, Round, Lymph Node, Focal Asymmetric Density, etc.
&nbsp;&nbsp;*Margin: Spiculated, Ill Defined, Circumscribed, Obscured, Microlobulated, etc. 
&nbsp;&nbsp;*Assessment: 0 - 5 (Integer)
&nbsp;&nbsp;*Pathology: Benign, Benign With Callback, Malignant
&nbsp;&nbsp;*Subtlety: 1 - 5 (Integer)








