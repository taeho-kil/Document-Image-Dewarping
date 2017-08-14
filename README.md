# Robust Document Image Dewarping Method using Text-lines and Line Segments (ICDAR 2017)


<p align="center">
<img src="/image/abs.png" width="700"> 
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
### Alignments of line semgents and its term
### Outlier removal and optimization


## Experimental results
### Experimental results on CBDAR 2007 dewarping contest dataset
### Experimental results on our dataset (non conventional images)


## Reference
