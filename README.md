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

Since neural networks require huge amount of data, we augment the current dataset. This is done by multiplying each label (bias field) with the corrected images to obtained 40 input images with this label. By doing this for each label we obtain a total of 1600 input images.

# Training Procedure

We wish to build and train a neural network that takes in the T1 weighted MRI as the input and outputs the bias field. This bias field can be used to reconstruct a corrected version of the input MRI. We train an autoencoder with 4 hidden layers in encoder and 4 hidden layers in decoder. We use "Mean Squared Error" as the loss function and "Adam optimizer" is used for weight updates. Since the dataset is huge, the training process is not straightforward. This is mainly because the dataset cannot be loaded in the disk at once. So, a custom dataloader is written in Keras that fetches the data required for each iteration. To further speed up the process, the slicing and preprocessing of MRIs is done beforehand and the results are stored as .npz files. These files are used in the process.

# Results

![Image of ](https://octodex.github.com/images/yaktocat.png)
