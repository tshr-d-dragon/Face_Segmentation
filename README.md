# Face_Segmentation

In this project, the goal is to train a model for segmenting various parts of face.

**Data:** [link](https://www.kaggle.com/datasets/ashish2001/multiclass-face-segmentation)

**Number of Images:** Train(19535) and Validation (2653)

Original Dataset have 18 classes can be referred from [here](https://www.kaggle.com/datasets/ashish2001/512x512-face-parsing-segmentation-tfrecords), However, I compounded classes like left_ear and right_ear to ear, etc. and also neglected the unnecessary classes like hair, hat, etc. 

**Classes:** 8   
- 0: Background
- 1: Face Skin
- 2: Eyebrows
- 4: Eyes
- 6: Nose
- 7: Mouth
- 13: Ears
- 16: Glasses
  
**Evaluation Metric:** Precision, Recall, Dice Score (F1-Score), Jacard Score (mIoU Score)

**Loss:** Dice Loss + Categorical_Cross_Entropy Loss + Jacard Loss

Images are in very big in size with varying orientation (Portrait as well as Landscape). So, for this project, I have decided to used images and masks of resized
value of 256 x 256.

**Pixel wise distribution of classes per image:**
![Distribution of Dataset](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Distribution%20of%20Dataset.png)

**Model Training:**
- I used PSPNet with ResNet50 as a backbone and Deeplabv3+ model with EfficientNetB0 as a backbone
- I used 4000 training images and 800 validation images only for training because of shortage of infrastructure
- I trained the model for 39 epochs with initial learning rate of 0.1 with SGD (Stochastic Gradient Descent) optimizer and Reduce Learning Rate on Plateau with patience of 4 and factor of 0.5)
- I also used Early Stopping callback with patience of 10 epochs to prevent overfitting


**Graphs (Loss, DiceScore (F1-Score), IOU_Score):**

- PSPNet

| Learning Rate | loss | F1 | IOU |
|:---:|:---:|:---:|:---:|
| ![LR](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/LR_PSPNet.png) | ![loss](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/loss_PSPNet.png) | ![F1](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/F1Score_PSPNet.png) | ![IOU](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/IOU_PSPNet.png) |

- Deeplab

| Learning Rate | loss | F1 | IOU |
|:---:|:---:|:---:|:---:|
| ![LR](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/LR_Deeplab.png) | ![loss](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/loss_Deeplab.png) | ![F1](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/F1Score_Deeplab.png) | ![IOU](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/IOU_Deeplab.png) |
