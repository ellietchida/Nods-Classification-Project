# Nodding Classification Project

## Introduction

This project uses a simple unsupervised clustering algorithm---K-means---to figure out whether each frame in an observation belongs to nod position A or B for the NIRSPEC instrument on Keck II.

Normally, observations follow a pattern like ABAB, but older datasets don’t follow clean patterns, especially when bad frames are removed. This code tries to recover that information using features from the data itself without labels as a reference.


## How It Works

1. Each frame is turned into a spatial profile by collapsing the image.
2. From that profile, we calculate a few features:
   - flux-weighted centroid
   - peak location
   - width
   - asymmetry (left-right imbalance)
   - total flux
3. These features are scaled using StandardScaler() so they are on similar ranges, with a weight applied to the centroid feature.
4. K-means clustering (with 2 clusters, dividing frames to be assessed in groups of 8) groups frames into A and B.


## Important Takeaways

The centroid tells us where the trace is relative to a "median" amongst other frames, which is the main difference between A and B since these shift. Features based on the data shape itself, like width and total flux, are too specific and vulnerable to hot pixels, making them bad for classification.

Main ideas: 
- Using centroid + peak or centroid + peak + asymmetry gave the best results
- Some features (like width) made things worse
- Feature choice matters more than the model itself
- Data preprocessing is important!


## Outputs

The code produces:
- A and B labels for each frame
- Plots of spatial profiles
- Confusion matrices and supervised metrics (when labels are known)
- Silhouette scores (for unlabeled data)


## Running the code!

Requires:
- numpy
- matplotlib
- scikit-learn

AND YOUR OWN DATA :)

### Author: Eleanor Tchida