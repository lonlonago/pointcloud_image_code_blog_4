Point cloud PCL free knowledge planet, point cloud paper speed reading. 

 标题：Fast 3D Line Segment Detection From Unorganized Point Cloud 

 Author: Xiaohu Lu, Yahui Liu, Kai Li 

 Compiled by: particle 

 Welcome to join the free knowledge planet, get PDF papers, and welcome to forward Moments to share your happiness. 

 This paper proposes a 3D line segment detection algorithm based on large-scale disordered point cloud. Compared with the traditional method of extracting 3D edge points first and then fitting 3D line segments, this paper proposes a 3D line segment detection algorithm based on point cloud segmentation and 2D line segment detection. In the case of input disordered point cloud, three-step detection of 3D line segments is performed. First, the point cloud is divided into 3D planes by region growth and region merging. Secondly, for each 3D plane, all the points to which it belongs are projected onto the plane to form a 2D image, and then 2D contour extraction and least squares fitting are performed to obtain 2D line segments. Then these 2D line segments are re-projected on the 3D plane to obtain the corresponding 3D line segments. Finally, a post-processing method for removing outliers and merging adjacent three-dimensional line segments is proposed. Experiments on multiple public datasets demonstrate the effectiveness and robustness of the method. 

 More results and C++ open source code in https://github.com/xiaohulugo/3DLineDetection 

 Main contribution 

 The method proposed in this paper still belongs to the category of images, but for the shortcomings of image-based methods, a faster line segment detection method for 3D point cloud data is proposed. The method mainly includes three parts: 

 (1) Point cloud segmentation: By means of region generation and region merging, the input point cloud is divided into three-dimensional planes. 

 (2) Detection of three-dimensional straight lines based on the plane: For each point cloud plane, all point clouds belonging to the plane are projected onto the plane to form a two-dimensional image, and then contour extraction and least squares fitting are performed based on the two-dimensional image to obtain two-dimensional line segments of each plane. Finally, these two-dimensional line segments are mapped to the three-dimensional plane to obtain three-dimensional line segment point cloud data. 

 (3) Post-processing: Through the three-dimensional structure information of the scene, the abnormal point cloud of the three-dimensional plane and the three-dimensional line segment is removed, and finally all the three-dimensional line segment point cloud data is merged. 

 Paper step atlas 

 ![avatar]( 20200705153750888.PNG) 

 Module A little cloud segmentation, this module mainly has three steps 

 Point cloud normal vector computing 

 region generation 

 Regional merger 

 ![avatar]( 20200705153810772.PNG) 

  Module 2 is based on the extraction of the three-dimensional line segment of the segmented plane. The steps are as follows 

 3D-2D projection 

 Line detection of 2D images (detection method is LSD reference [1]) 

 2D-3D mapping 

 ![avatar]( 20200705153822426.PNG) 

  Module 3 Post-processing, noise removal 

 Noise removal plane point cloud 

 Noise removal line segment point cloud 

 All line segment point clouds merge 

 ![avatar]( 20200705153834654.PNG) 

 Experimental results and summary   

 This paper proposes and proves a simple and effective 3D line detection algorithm for large-scale unorganized point clouds. This method is based on point cloud segmentation and 2D line detection, and uses post-processing methods to remove outliers. Unlike traditional edge point-based methods, this method is simple to implement and fast (100,000 point clouds for 40 seconds). Since our method is based on point cloud segmentation, a failure case of our method is on curved surfaces, and the segmentation effect of planes in curved point clouds is unsatisfactory. Despite this, the method is very effective for structural scenes. 

 References 

 【1】R. G. von Gioi, J. Jakubowicz, J.-M. Morel, and G. Randall, “LSD: A fast line segment detector with a false detection control,” IEEE Transactions on Pattern Analysis and Machine Intelligence. 

 If you are interested in this article, please click "Original Reading" to get the QR code of Knowledge Planet. Be sure to join the free Knowledge Planet according to the remarks of "Name + School/Company + Research Direction", download the pdf document for free, and communicate with more friends who love to share! 

 ![avatar]( 20200705153852662.PNG) 

