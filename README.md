# Document image dewarping using text-lines and line Segments


<p align="center">
<img src="/algorithm_image/abs.png" width="600"> 
</p>


## Abstract
Conventional text-line based document dewarping methods have problems when handling complex layout and/or
very few text-lines. When there are few aligned text-lines in the image, this usually means that photos, graphics and/or tables take
large portion of the input instead. Hence, for the robust document dewarping, we propose to use line segments in the image in
addition to the aligned text-lines. 
Based on the assumption and observation that all the transformed line segments are still straight (line to line mapping), and many of them are horizontally or vertically aligned in the well-rectified images, we encode this properties into the cost function in addition to the text-line based cost. 
By minimizing the function, we can obtain transformation parameters for camera pose, page curve (extrinsic parameters) and camera focal length (intrinsic parameter), which are used for document rectification. Considering that there are many outliers in line segment directions and missed text-lines in some cases, the overall algorithm is designed in an iterative manner. At each step, we remove text components and line segments that are not well horizontal/vertical aligned, and then minimize the cost function with the updated information. Experimental results show that the proposed method is robust to the variety of page layouts.
Moreover, the proposed method can extend to general curves surfaces as well as document.

## Algorithm

### Two line semgent properties
<p align="center">
<img src="/algorithm_image/straight_property.png" width="400">
<img src="/algorithm_image/align_property.png" width="400"> 
</p>

#### Straightness property
The straightness property describes the line segments extracted in curved document image, lines on the curved document surface become still straight in the well-rectified domain (Although the lines extracted in the well-rectified image can be curved in the curved document surface). It means that line-to-line mapping.
Since the straightness property is always satisfied with all plane to plane mapping, it is not a significant constraint in rectification considering only camera view (such as homography). However we consider page curve as well as camera view in rectification process, then this property becomes an efficient constraint that prevents lines from being curved.

#### Alignment property
Based on the observation that the majority of line segments are horizontally or vertically aligned in the rectified images.

### Outlier removal
<p align="center">
<img src="/algorithm_image/iteration.png" width="800"> 
</p>

The direct optimization of ![equation](https://latex.codecogs.com/gif.latex?f_%7Bcost%7D) may yield poorly rectified results, due to outliers. We treat two outlier types that are missed text-lines and line segments having arbitrary direction (non horizontal/vertical). For the outlier removal, we design an iterative method. At each step, we refine the features (text components and line segments) by removing outlier (that are not well aligned) and minimize the cost function with updated inliers.

## Experimental results
### CBDAR 2007 dataset
We evaluate our method on the CBDAR 2007 dewarpint contest dataset [http://staffhome.ecm.uwa.edu.au/~00082689/downloads.html], that is consisted of binarized text images.

| Input image   |    Kim [2]    |   Proposed    |
| ------------- | ------------- | ------------- |
| <img src="/results/cbdar/1_in.png" width="200">  | <img src="/results/cbdar/1_kim.png" width="200">  | <img src="/results/cbdar/1_proposed.png" width="200">  |
| <img src="/results/cbdar/2_in.png" width="200">  | <img src="/results/cbdar/2_kim.png" width="200">  | <img src="/results/cbdar/2_proposed.png" width="200">  |
| <img src="/results/cbdar/3_in.png" width="200">  | <img src="/results/cbdar/3_kim.png" width="200">  | <img src="/results/cbdar/3_proposed.png" width="200">  |
| <img src="/results/cbdar/4_in.png" width="200">  | <img src="/results/cbdar/4_kim.png" width="200">  | <img src="/results/cbdar/4_proposed.png" width="200">  |
| <img src="/results/cbdar/5_in.png" width="200">  | <img src="/results/cbdar/5_kim.png" width="200">  | <img src="/results/cbdar/5_proposed.png" width="200">  |
| <img src="/results/cbdar/6_in.png" width="200">  | <img src="/results/cbdar/6_kim.png" width="200">  | <img src="/results/cbdar/6_proposed.png" width="200">  |

### Our document image dataset
In order to consist of non conventional document images (i.e., not text-abundant cases), we collected 100 images having various layouts (e.g., three column documents, documents containing large tables and/or figures, presentation slides, and so on).

| Input image   |    Kim [2]    |   Proposed    |
| ------------- | ------------- | ------------- |
| <img src="/results/dataset1/1_in.png" width="200">  | <img src="/results/dataset1/1_kim.png" width="200">  | <img src="/results/dataset1/1_proposed.png" width="200">  |
| <img src="/results/dataset1/2_in.png" width="200">  | <img src="/results/dataset1/2_kim.png" width="200">  | <img src="/results/dataset1/2_proposed.png" width="200">  |
| <img src="/results/dataset1/3_in.png" width="200">  | <img src="/results/dataset1/3_kim.png" width="200">  | <img src="/results/dataset1/3_proposed.png" width="200">  |
| <img src="/results/dataset1/4_in.png" width="200">  | <img src="/results/dataset1/4_kim.png" width="200">  | <img src="/results/dataset1/4_proposed.png" width="200">  |
| <img src="/results/dataset1/5_in.png" width="200">  | <img src="/results/dataset1/5_kim.png" width="200">  | <img src="/results/dataset1/5_proposed.png" width="200">  |
| <img src="/results/dataset1/6_in.png" width="200">  | <img src="/results/dataset1/6_kim.png" width="200">  | <img src="/results/dataset1/6_proposed.png" width="200">  |

### Our curved image dataset
In order to consist of general curved surface images (such as bottles), we collected 74 images.

| Input image   |    Kim [2]    |   Proposed    |
| ------------- | ------------- | ------------- |
| <img src="/results/dataset2/1_in.png" width="200">  | <img src="/results/dataset2/1_kim.png" width="200">  | <img src="/results/dataset2/1_proposed.png" width="200">  |
| <img src="/results/dataset2/2_in.png" width="200">  | <img src="/results/dataset2/2_kim.png" width="200">  | <img src="/results/dataset2/2_proposed.png" width="200">  |
| <img src="/results/dataset2/3_in.png" width="200">  | <img src="/results/dataset2/3_kim.png" width="200">  | <img src="/results/dataset2/3_proposed.png" width="200">  |
| <img src="/results/dataset2/4_in.png" width="200">  | <img src="/results/dataset2/4_kim.png" width="200">  | <img src="/results/dataset2/4_proposed.png" width="200">  |
| <img src="/results/dataset2/5_in.png" width="200">  | <img src="/results/dataset2/5_kim.png" width="200">  | <img src="/results/dataset2/5_proposed.png" width="200">  |
| <img src="/results/dataset2/6_in.png" width="200">  | <img src="/results/dataset2/6_kim.png" width="200">  | <img src="/results/dataset2/6_proposed.png" width="200">  |

## Executable program
Executable program can be downloaded by below links:

http://ispl.synology.me:8480/sharing/uA2DTRA8U


## Reference
[1] Taeho Kil, Wonkyo Seo, Hyung Il Koo and Nam Ik Cho, "Robust Document Image Dewarping Using Text-Line and Line Segments", ICDAR 2017.

[2] Beom Su Kim, Hyung Il Koo, and Nam Ik Cho, "Document Dewarping via Text-line based Optimization", Pattern Recognition 2015.
