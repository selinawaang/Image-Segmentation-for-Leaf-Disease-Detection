# Image Segmentation for Leaf Disease Detection
Author: Selina Wang\
Date: December, 2020\
Course: MATH123 Tufts University


I perform image segmentation using spectral clustering to segment leaf images and identify tar spots on maple leaves. I explore the theoretical aspect of constructing a normalized Laplacian, as well as the impacts of different parameter choices on the segmentation. I find that spectral clustering can indeed successfully segment leaf images from the background, and segment tar spots form the leaf. 

![leaf34_2_10](https://user-images.githubusercontent.com/80374850/200037955-07ad8d0f-f4a4-4492-9ae0-21c2dfac972f.png)


### Methodology
- I downsize the image to $50 * 50$ pixels to reduce computational complexity, and also convert it to a grey scale image.
- I then construct the weight matrix for this image to form a graph with the data points as nodes. The first component of the weight matrix forms a Gaussian Kernel using the difference in grey scale value between data points, $\|F_i-F_j\|$, while the second component considers the $L_2$ distance between data points on the image, $\|X_i-X_j\|$. Combining these two factors gives a weight matrix that takes into account both the "color" difference and the distance.
- Form normalized Laplacian L: For this problem, I consider a graph partition using a normalized cut. The normalized cut considers the cut value between different groups, relative to the association between nodes within one group to the rest of the group. We consider the optimal partition to be the one that not only minimizes the normalized cut, but also maximizes the association between points within the same group. The advantage of using this method is that the spectral clustering will do a better job at capturing the big structure of the data, as opposed to clustering out small groups of outliers.
- Perform spectral clustering: The spectral clustering step involves forming a spectral embedding using the eigenvectors of L and then performing K-means clustering on the embedding.
- Tune parameters: I measure the quality of segmentation using the cut value of the graph partition. Intuitively, a smaller cut value would indicate a better segmentation as this means that the connectivity between nodes in different groups is smaller. Using this as the metric, I then used a grid method to search for the best parameter combination.


### Result:
I chose three leaves that vary in shape, color and positioning of the tar spot to test the success of spectral clustering in segmenting the tar spot. I experimented with two different backgrounds: a grey textured background, and a plain white background. The outcome is shown in the figure below.

<img width="900" alt="Screen Shot 2022-11-04 at 2 01 49 PM" src="https://user-images.githubusercontent.com/80374850/200044651-e60e0967-94e1-433f-869e-6ce5f399e1f2.png">

For more details please see the full [report](https://github.com/selinawaang/Image-Segmentation-for-Leaf-Disease-Detection/blob/7c452ccd77d14460d4966bfc075c64e77ba82f06/Image%20Segmentation%20Final.ipynb).
