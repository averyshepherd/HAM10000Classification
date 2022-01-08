# Skin Lesion Classification

# Introduction
## Why do this project?
* 20% of Americans diagnosed with skin cancer before age 70
* 1% of skin cancer cases are invasive melanoma
* 62% of skin cancer deaths that are invasive melanoma

## Goals
* Develop a model that predicts the correct image class with high accuracy (multi-class classification).
* Develop a model that predicts whether a lesion is a melanoma or non-melanoma with high accuracy (binary classification).
* Ultimately, ensure the developed models have low false negative rates pertaining to melanoma.

# Dataset
* Originally from Harvard Dataverse
* Collection of 10,015 dermatoscopic images used for training neural networks for automated diagnosis of skin lesions.
* Includes 7 diagnostic categories (classes) : 
  * Actinic keratoses and intraepithelial carcinoma (akiec)
  * Basal cell carcinoma (bcc)
  * Benign keratosis-like lesions (bkl)
  * Dermatofibroma (df) 
  * Melanoma (mel)
  * Melanocytic nevi (nv) 
  * Vascular lesions (vasc)
* Other predictors include age, sex, localization & how the lesion was confirmed.

# Multiclass Classsification

## CNN Architecture-1
![image](https://user-images.githubusercontent.com/12545194/148628883-52a1747b-ee4d-4810-a08f-b44fbd0a9808.png)
The NN was predicting almost all the images to belong to 1 class. After further investigation, it was found that this was being caused due to dying ReLU and absence of normalization.

## CNN Architecture-2
![image](https://user-images.githubusercontent.com/12545194/148628980-c9d2d845-17f2-421a-aab5-ff72d98e1809.png)


# Binary Classsification

## Architecture - 1
![image](https://user-images.githubusercontent.com/12545194/148629026-f02ddafd-7dd9-4fc9-a7d1-dcc9ae1543c8.png)

## Architecture - 2
The CNN architecture 3 was able to achieve a decent false negative rate but had a really high positive rate. To address, high positive rate issue we used a cascaded model.
![image](https://user-images.githubusercontent.com/12545194/148629043-af120ee9-f7bf-4021-8906-e1a8f3c67474.png)

### Improvement due to Cascading
<img width="754" alt="image" src="https://user-images.githubusercontent.com/12545194/148629122-802af12c-9b2a-4c2c-a1c6-937bf36f3afe.png">



# Understanding Neural Network better
<img width="1037" alt="image" src="https://user-images.githubusercontent.com/12545194/148629094-f828cd8f-15d6-47ab-84d9-17421c1685ac.png">

Couple of key observations:
* Looks like CNN Layer 1 is working like a edge detector and extracting all the edges or gradients in the image
* CNN layer 1 is good enough to “circle out” the lesion from the image
* As we proceed within the layers, the deformities on the skin don’t hold much weight. This is a very important observation because we would like to create a model that is NOT biased towards any skin color. (It is highly likely that BatchNormalisation layers are enabling this removal of bias)
