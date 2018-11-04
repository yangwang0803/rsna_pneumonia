# Kaggle - RSNA Pneumonia Detection Challenge 

Rank 49 solution of the Kaggle featured competetition [RSNA Pneumonia Detection Challenge](https://www.kaggle.com/c/rsna-pneumonia-detection-challenge)


## Model overview
The architecture of the model is Matterport's implementation of [MaskRCNN](https://github.com/matterport/Mask_RCNN) with minimal changes. The training is divided into two phases:

1. Phase 1  
Phase 1 training predicts with the original labels, then tests on the entire training set to generate pseudo-labels for the false positives.

2. Phase 2  
Phase 2 training predicts with the pseudo-labels, then merges with the Phase 1 prediction on the testing data to remove false positives.



## Basic procedures to reproduce the results

1
`/code/training_maskrcnn.ipynb`

This is the phase 1 model that trains with the original labels `/data/stage_1_train_labels.csv`. The output of this notebook is under `/model/Mask_RCNN/pneumonia20181018T1640/mask_rcnn_pneumonia_0020.h5`

2
`/code/testing_maskrcnn.ipynb` up to block "Phase 2 prediction"

This is the phase 1 prediction. The phase 1 model predicts on the entire training set to generate the pseudo-labels for phase 2 model. The output of this notebook is under `/data/stage_1_train_labels_2.csv`

3
`/code/training_maskrcnn_2.ipynb`

This is the phase 2 model that trains with the pseudo-labels generated in phase 1. The purpose of phase 2 is to detect false positives in phase 1 and remove them. The output of this notebook is under `/model/Mask_RCNN/pneumonia20181021T0214/mask_rcnn_pneumonia_0020.h5`

4
`/code/testing_maskrcnn.ipynb`

This is the phase 2 prediction. The phase 2 model predicts the false positives and then remove them from the phase 1 predictions. The final output is under `/code/submission.csv`