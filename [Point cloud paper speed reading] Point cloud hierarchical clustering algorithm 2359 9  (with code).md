Point cloud PCL free knowledge planet, point cloud paper speed reading. 

 标题：PAIRWISE LINKAGE FOR POINT CLOUD SEGMENTATION 

 作者：Lu, Xiaohu and Yao, Jian and Tu 

 Planet ID: Lionheart | Point Cloud Registration 

 Welcome to join the free knowledge planet, get PDF papers, and welcome to forward Moments to share your happiness. 

 Abstracts of papers 

 In this article, we first propose a novel hierarchical clustering algorithm --pairwise linkage (p-linkage), which can be used to cluster data of any dimension, and then efficiently applied to the classification of 3D unstructured point clouds. The P-linkage clustering algorithm first calculates the characteristic value of each point, such as calculating the density of 2D points and the smoothness of 3D points, and then uses more characteristic values to describe the link relationship between each point and its nearest neighbor. The initial clustering can be carried out more easily through the linking of point pairs. Then, the clustering fusion process obtains the final optimized clustering result, and the clustering result can be used in other applications. Based on P-Linkage clustering, we invented in 3D unstructured point clouds An efficient segmentation algorithm, in which the smoothness of points is used as the eigenvalue, slices are created for each initial cluster, and then novel and robust slice fusion methods are used to obtain the final segmentation results. The proposed P-linkage clustering and 3D point cloud segmentation methods require only one input parameter. Experimental results synthesized data in different dimensions of 2d-4d fully demonstrate the efficiency and robustness of the P-Linkage clustering. A large number of experimental results in vehicle, airborne and station laser point clouds demonstrate the robustness of our proposed method. 

 https://github.com/xiaohulugo/PointCloudSegmentation 

 ![avatar]( 20200524215001663.JPG) 

 ● Paper Atlas ● English Abstract 

 In this paper, we first present a novel hierarchical clustering algorithm named Pairwise Linkage (P-Linkage), which can be used forclustering any dimensional data, and then effectively apply it on 3D unstructured point cloud segmentation. The P-Linkage clusteringalgorithm first calculates a feature value for each data point, for example, the density for 2D data points and the flatness for 3D pointclouds. Then for each data point a pairwise linkage is created between itself and its closest neighboring point with a greater featurevalue than its own. The initial clusters can further be discovered by searching along the linkages in a simple way. After that, a clustermerging procedure is applied to obtain the finally refined clustering result, which can be designed for specialized applications. Based onthe P-Linkage clustering, we develop an efficient segmentation algorithm for 3D unstructured point clouds, in which the flatness of theestimated surface of a 3D point is used as its feature value. For each initial cluster a slice is created, then a novel and robust slice mergingmethod is proposed to get the final segmentation result. The proposed P-Linkage clustering and 3D point cloud segmentation algorithmsrequire only one input parameter in advance. Experimental results on different dimensional synthetic data from 2D to 4D sufficientlydemonstrate the efficiency and robustness of the proposed P-Linkage clustering algorithm and a large amount of experimental resultson the Vehicle-Mounted, Aerial and Stationary Laser Scanner point clouds illustrate the robustness and efficiency of our proposed 3Dpoint cloud segmentation algorithm. 

 ![avatar]( 20200524215049534.JPG) 

