---
layout: project
type: project
image: images/project-3/nuclei.png
title: Advancing Medical Discovery through Nuclei Segmentation
permalink: projects/data_science_bowl_2018
# All dates must be YYYY-MM-DD format!
date: 2018-04-16
labels:
  - Image Segmentation
  - U-Net
  - Cell biology
summary: Competition to find and segment cell nuclei in divergent images, thereby advancing medical discovery.
---
Described here is an approach to the 2018 Data Science Bowl competition, this soluction  scored within the top 20% of submissions, out of over 3000 teams. The objective of the competition was to segment nuclei in cell microscopy images.

Identifying cell nuclei is the starting point for many biological analyses. Most of the human body’s 30 trillion cells contain a nucleus full of DNA, the genetic code that programs each cell. Segmenting nuclei allows researchers to identify individual cells in a sample, measure their morphometry, and analyse how cells react to drug treatments.

The objective of this competition was to create a single generalised model for segmentation that works across different kinds of microscopy and image modalities, robust to variation in the size of the nuclei and the image color scheme. Such a model could be built into software that biologists use with all kinds of microscopes and eliminate the need for them to train on their individual data or provide metadata about their cell type, microscope, or resolution.

## Images
Below is a montage of images from the stage 1 test data to show the difference in image modalities that the model should perform on:

<div align="center">
    <img src="/images/project-3/montage_test.png" alt="Front End" style="width:60%">
</div>


## Approach:
For this competition I attempted three approaches. First, a simple adaptive <a href="https://en.wikipedia.org/wiki/Otsu%27s_method" target="_blank">Otsu threshold</a> on greyscale converted images to set a baseline result. Following on from this I tried a U-net convolutional neural network, and mask R-CNN models. The mask R-CNN performed the best, I also tried various data augmentation steps, and post morphological processing with the watershed transform.

## Model evaluation
<a href="https://www.kaggle.com/c/data-science-bowl-2018#evaluation" target=" _blank">Evalutation of this model</a> uses the mean average precision at different intersection over union (IoU) thresholds. The IoU of a proposed set of object pixels and a set of true object pixels is calculated.

The metric sweeps over a range of IoU thresholds, at each point calculating an average precision value. The threshold values range from 0.5 to 0.95 with a step size of 0.05: `(0.5, 0.55, 0.6, 0.65, 0.7, 0.75, 0.8, 0.85, 0.9, 0.95)`. In other words, at a threshold of 0.5, a predicted object is considered a "hit" if its intersection over union with a ground truth object is greater than 0.5.

At each threshold value `t`, a precision value is calculated based on the number of true positives (TP), false negatives (FN), and false positives (FP) resulting from comparing the predicted object to all ground truth objects.

A true positive is counted when a single predicted object matches a ground truth object with an IoU above the threshold. A false positive indicates a predicted object had no associated ground truth object. A false negative indicates a ground truth object had no associated predicted object. The average precision of a single image is then calculated as the mean of the above precision values at each IoU threshold.

Lastly, the score returned by the competition metric is the mean taken over the individual average precisions of each image in the test dataset.

This was implemented locally in the `./utils/evaluate.py` file.

## Submission: run-length encoding
<a href="https://www.kaggle.com/c/data-science-bowl-2018#evaluation" target=" _blank">Run length encoding</a> is used for competition submissions to reduce the submission file size. Instead of submitting an exhaustive list of indices for your segmentation, pairs of values that contain a start position and a run length. E.g. '1 3' implies starting at pixel 1 and running a total of 3 pixels (1,2,3).

The competition format requires a space delimited list of pairs. For example, '1 3 10 5' implies pixels 1,2,3,10,11,12,13,14 are to be included in the mask. The pixels are one-indexed and numbered from top to bottom, then left to right: 1 is pixel (1,1), 2 is pixel (2,1), etc.

The metric checks that the pairs are sorted, positive, and the decoded pixel values are not duplicated. It also checks that no two predicted masks for the same image are overlapping.

This was implemented locally in the  `./utils/evaluate.py` file.

## Resources:
* <a href="https://github.com/williamgrimes/nuclei_segmentation/" target="_blank">Github</a>
* <a href="https://www.kaggle.com/c/data-science-bowl-2018" target="_blank">Website</a>
* <a href="https://arxiv.org/abs/1505.04597" target="_blank">Paper: U-net</a>
* <a href="https://arxiv.org/abs/1703.06870" target="_blank">Paper: Mask R-CNN</a>
