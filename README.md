# Non-Uniformity-Correction-in-MRIs


# Description:

Generally, T1-weighted MRIs exhibits an intensity non-uniformity due to imperfections in the field coils or due to changes in the magnetic susceptibility. This non-uniformity can confuse the tissue classifiers in the pre-processing stage, as they assume uniform intensities for a tissue. Therefore, it is necessary to remove this non-uniformity before the tissue classification is performed. This non-uniformity is also called as the Bias Field.

Traditionally, non-uniformity correction is done through mathematical curve fitting techniques. This method is found to be inefficient when a high amount of non unoformity exists in MRIs. So, we try to solve this problem using Deep Learning Techniques. In recent years, Deep Learning techniques have found to efficient in solving problems related to Image reconstruction and segmentation.  

# Goal

Train a Convolutional Neural Network(CNN) based autoencoder by performing Data Augmentation techniques and analyze the predicted bias fields and corrected MRIs using Brain Suite Software. 


# Dataset

This data has 40 T1 weighted MRIs and their corresponding Bias fields. Corrected MRIs can be obtained by dividing the input images with their bias field image. Both the input images and labels are 3d images and dimensions are given below.

Input MRI: 260 x 311 x 260 
Output Bias: 260 x 311 x 260 

Since neural networks require huge amount of data, we augment the current dataset. This is done by multiplying each label (bias field) with the corrected images to obtained 40 input images with this label. By doing this for each label we obtain a total of 1600 input images. All the dataset are available here:

**Link : (https://drive.google.com/open?id=19rREknauQ4stxaLp_Fa7M7cb7uU1s8NJ)**


# Overview

The analysis and implementation has been done using Python 3.6 version. The versions of the external libraries used are as mentioned below:

NumPy == 1.16.4
Matplotlib == 3.0.3
Scikit-Learn == 0.21.1
Nibabel >= 2.0.2
Nilearn (!pip install nilearn)

*Augmentation.ipynb*: Used for Augmenting the dataset and storing the datasets as .npz
*Augment_training.ipynb*: Used for training the neural network with custom dataloader.
*Augmentation_Reconstruction.ipynb*: Used for reconstructing the corrected images from the predicted bias.


# Training Procedure

We wish to build and train a neural network that takes in the T1 weighted MRI as the input and outputs the bias field. This bias field can be used to reconstruct a corrected version of the input MRI. We train an autoencoder with 4 hidden layers in encoder and 4 hidden layers in decoder. We use "Mean Squared Error" as the loss function and "Adam optimizer" is used for weight updates. Since the dataset is huge, the training process is not straightforward. This is mainly because the dataset cannot be loaded in the disk at once. So, a custom dataloader is written in Keras that fetches the data required for each iteration. To further speed up the process, the slicing and preprocessing of MRIs is done beforehand and the results are stored as .npz files. These files are used in the process.


# Results

**Input MRI images:**

![BiasField](/images/Input.png)

**Reconstructed Bias Field:**

![BiasField](/images/BiasField.png)

**Corrected MRI images:**

![BiasField](/images/Corrected.png)

Brainsuite software has been used for visualization of the above images. It can be downloaded from the website below:  http://brainsuite.org
