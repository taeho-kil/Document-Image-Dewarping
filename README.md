# Robust Document Image Dewarping Method using Text-lines and Line Segments (ICDAR 2017)


<p align="center">
<img src="/image/abs.png" width="800"> 
</p>


## Abstract
Conventional text-line based document dewarping
methods have problems when handling complex layout and/or
very few text-lines. When there are few aligned text-lines in the
image, this usually means that photos, graphics and/or tables take
large portion of the input instead. Hence, for the robust document
dewarping, we propose to use line segments in the image in
addition to the aligned text-lines. Based on the assumption and
observation that many of the line segments in the image are
horizontally or vertically aligned in the well-rectified images,
we encode this property into the cost function in addition to
the text-line alignment cost. By minimizing the function, we can
obtain transformation parameters for camera pose, page curve,
etc., which are used for document rectification. Considering that
there are many outliers in line segment directions and missed
text-lines in some cases, the overall algorithm is designed in an
iterative manner. At each step, we remove text components and
line segments that are not well aligned, and then minimize the
cost function with the updated information. Experimental results
show that the proposed method is robust to the variety of page
layouts.


## Algorithm
### Proposed cost function
For the parametric modeling of the dewarping process, we adopt the model in [1].
By this model, the geometric relation between the captured image domain and the rectified document domain can be
parameterized with the polynomial parameters ![equation](https://latex.codecogs.com/gif.latex?%5C%7Ba_%7Bm%7D%5C%7D_%7Bm%3D0%7D%5E%7BM%7D) and camera pose matrix ![equation](https://latex.codecogs.com/gif.latex?%5Cmathbf%7BR%7D).

For the estimation of these dewarping parameters ![equation](https://latex.codecogs.com/gif.latex?%5CTheta%20%3D%5C%28%5C%7Ba_%7Bm%7D%5C%7D_%7Bm%3D0%7D%5E%7BM%7D%2C%5Cmathbf%7BR%7D%5C%29), we develop a cost function:

![equation](https://latex.codecogs.com/gif.latex?f_%7Bcost%7D%5C%28%5CTheta%20%5C%29%3Df_%7Btext%7D%5C%28%5CTheta%20%5C%29&plus;%5Clambda%20f_%7Bline%7D%5C%28%5CTheta%20%5C%29)

where ![equation](https://latex.codecogs.com/gif.latex?f_%7Btext%7D%5C%28%5CTheta%20%5C%29) is a term reflecting the properties of text-lines in rectified images [1]. To be precise, this term becomes small when transformed text-lines are well-aligned: horizontally straight, line-spacings between two neighboring text-lines are regular, and text-blocks are either left-aligned, right-aligned, or justified.

However, the optimization of ![equation](https://latex.codecogs.com/gif.latex?f_%7Btext%7D%5C%28%5CTheta%20%5C%29) sometimes yields severe distortions on non-text regions, and we also exploit line segments in document images by introducing ![equation](https://latex.codecogs.com/gif.latex?f_%7Bline%7D%5C%28%5CTheta%20%5C%29)


### Alignments of line semgents and its term
Based on the observation that the majority of line segments are horizontally or vertically aligned in the rectified images, we define the term as

![equation](https://latex.codecogs.com/gif.latex?f_%7Bline%7D%28%20%5CTheta%20%29%3D%20%5Csum_%7Bi%7D%20%5Cmin%20%28%5Ccos%5E%7B2%7D%20%5Ctheta_%7Bi%7D%20%2C%5Csin%5E%7B2%7D%20%5Ctheta_%7Bi%7D%29%2C)

where ![equation](https://latex.codecogs.com/gif.latex?%5Ctheta_%7Bi%7D) is the angle of the transformed ![equation](https://latex.codecogs.com/gif.latex?i)-th line segment (when rectified with the current parameters ![equation](https://latex.codecogs.com/gif.latex?%5CTheta)). This term makes that all line segments are aligned in either vertical or horizontal direction.

<p align="center">
<img src="/images/angle.png" width="500"> 
</p>

### Outlier removal and optimization

The direct optimization of ![equation](https://latex.codecogs.com/gif.latex?f_%7Bcost%7D) may yield poorly rectified results, due to outliers. We treat two outlier types that are missed text-lines and line segments having arbitrary direction (non horizontal/vertical). For the outlier removal, we design an iterative mathod. For the outlier removal, we design an iterative method. At each step, we refine the features (text components and line segments) by removing outlier and minimize the cost function with updated inliers.

<p align="center">
<img src="/images/iteration.png" width="500"> 
</p>

## Experimental results
### Experimental results on CBDAR 2007 dewarping contest dataset
### Experimental results on our dataset (non conventional images)


## Reference
1. Beom Su Kim, Hyung Il Koo, and Nam Ik Cho, "Document Dewarping via Text-line based Optimization," Pattern Recognition, Vol. 48, No. 11, pp. 3600 - 3614, Nov. 2015.
