# Face_Segmentation

## Analysis of the problem statement and Dataset:
In this project, the goal is to train a model for segmenting various parts of face.

**Dataset:** [link](https://www.kaggle.com/datasets/ashish2001/multiclass-face-segmentation)

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

## Model Training:
- I used PSPNet with ResNet50 as a backbone and Deeplabv3+ model with EfficientNetB0 as a backbone
- I used 4000 training images and 800 validation images only for training because of shortage of infrastructure
- I trained the model for 39 epochs with initial learning rate of 0.1 with SGD (Stochastic Gradient Descent) optimizer and Reduce Learning Rate on Plateau with patience of 4 and factor of 0.5)
- I also used Early Stopping callback with patience of 10 epochs to prevent overfitting


## Graphs (Loss, DiceScore (F1-Score), IOU_Score):

- PSPNet

| Learning Rate | loss | F1 | IOU |
|:---:|:---:|:---:|:---:|
| ![LR](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/LR_PSPNet.png) | ![loss](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/loss_PSPNet.png) | ![F1](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/F1Score_PSPNet.png) | ![IOU](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/IOU_PSPNet.png) |

- Deeplab

| Learning Rate | loss | F1 | IOU |
|:---:|:---:|:---:|:---:|
| ![LR](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/LR_Deeplab.png) | ![loss](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/loss_Deeplab.png) | ![F1](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/F1Score_Deeplab.png) | ![IOU](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/IOU_Deeplab.png) |

## Predictions on 3 images from Test Dataset:

- PSPNet

| Image | Ground Truth | Prediction |
|---|---|---|
| ![1](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/test_10.png) | ![2](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/test_10_mask.png) | ![3](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/test_10_pred.png) |
| ![1](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/test_50.png) | ![2](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/test_50_mask.png) | ![3](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/test_50_pred.png) |
| ![1](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/test_100.png) | ![2](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/test_100_mask.png) | ![3](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/PSPNet_images/test_100_pred.png) |

- Deeplab

| Image | Ground Truth | Prediction |
|---|---|---|
| ![1](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/test_10.png) | ![2](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/test_10_mask.png) | ![3](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/test_10_pred.png) |
| ![1](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/test_50.png) | ![2](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/test_50_mask.png) | ![3](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/test_50_pred.png) |
| ![1](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/test_100.png) | ![2](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/test_100_mask.png) | ![3](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Deeplab_images/test_100_pred.png) |

## Performance Comparison:

- On Complete (Train: 4000 and Val: 800 images) Dataset:

![TrainVal](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Performance_TrainVal.png)


- On Test Dataset (7766 images):

![Test](https://github.com/tshr-d-dragon/Face_Segmentation/blob/main/Performance_Test.png)

## Future Steps:
-   Try training model with complete dataset
-   Try training model with different loss functions
-   Try training Deeplabv3+ and PSPNet models with different backbones
-   Try with different model such as Unet, LinkNet, ICNet with different backbones
-   Try training model further for more epochs
-   Try gathering more data for training by new annotations and augmentations
-   Try training the model further with smaller learning rate with Adam or SGD (with momentum)
