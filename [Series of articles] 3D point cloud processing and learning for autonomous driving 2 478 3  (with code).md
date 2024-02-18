标题：3D Point Cloud Processing and Learning for Autonomous Driving 

 作者：Siheng Chen, Baoan Liu, Chen Feng, Carlos Vallespi-Gonzalez, Carl Wellington 

 Compiler: Point Cloud PCL 

 Source: arXiv 2020 

 This article is for academic sharing only. Due to malicious reports, we cannot apply for originality for the time being. If my translated article is infringing, please contact to delete it. Welcome to join the free knowledge planet, get PDF papers, and welcome to forward Moments. If there is any error in the content, please comment and leave a message. Please do not reprint without permission! 

 The official account is dedicated to sharing articles and technologies related to point cloud processing, SLAM, 3D vision, and high-precision maps. Welcome to join us, communicate and progress together. If you are interested, please contact WeChat 920177957. 

 Write on the front 

 This article can be said to be a very complete introduction to the role of point clouds in autonomous driving of each module, from the macro sub-module of the point cloud in the role and application of autonomous driving, read the entire article, will not only have a more comprehensive understanding of autonomous driving technology, and understand the importance of point clouds in autonomous driving, the creation of high-precision maps introduced here and positioning perception module introduction is the core technology in the field of autonomous driving, such as in the introduction of the two positioning methods of the positioning module, when introducing the use of semantic geometric information and point cloud intensity information for positioning in different scenarios, it is completely suitable for the apollo autonomous driving solution, allowing readers to gain a lot. Here the blogger decided to translate it completely and share it with more interested friends. 

 There may be clerical errors or poor understanding in the process of translation and understanding. Everyone is welcome to leave a message. Due to the length of the article, the article will be divided into multiple articles and updated. The full English pdf is available on the free Knowledge Planet. 

 directory 

 1. Introduction 

 The significance, history and current situation of autonomous driving 

 1-B A complete autonomous driving system module 

 1-C 3D point cloud processing and learning 

 1-D Outline 

 2. Key elements of 3D point cloud processing and learning 

 2-A point cloud characteristics 

 2-B matrix representation 

 2-C representative tools 

 3. Creation of high-precision maps and processing of 3D point clouds 

 Overview of 3-A high-definition map creation module 

 Splicing of 3-B 3D Point Clouds 

 Extraction of semantic features from 3-C point clouds 

 3-D map creation challenges 

 4. Processing based on point cloud positioning 

 Overview of 4-A Positioning Module 

 4-B Map-based Localization 

 4-C point cloud positioning challenges 

 5. Point cloud perception 

 5-A Perception Module Overview 

 Detection of 5-B 3D Point Cloud Objects 

 5-C point cloud perception challenges 

 6. Summarize and expand the problem 

 6-A The relationship between academia and industry 

 6-B qualitative results 

 2. Key elements of 3D point cloud processing and learning 

 In this section, basic tools for 3D point cloud processing and learning will be introduced. Start with the key characteristics of 3D point clouds. Evaluate some of the methods for representing 3D point clouds. Finally, a range of popular tools for processing 3D point clouds are reviewed. These tools have received a great deal of attention in the academic community. Even though some of them may not be directly applied to autonomous driving systems, they are still worth mentioning as they can inspire new technologies that may be useful for autonomous driving. 

 2-A 

 point cloud characteristics 

 As discussed in Section 1-C, two typical three-dimensional point clouds in autonomous driving are considered: real-time lidar point clouds and point cloud high-resolution maps. 

 Real-time LiDAR point cloud. For each three-dimensional point in a real-time LiDAR point cloud, its associated laser beam and captured timestamp can be tracked. A real-time LiDAR point cloud can be naturally organized on a two-dimensional image whose x-axis is timestamp and y-axis is laser ID. Therefore, we treat each individual real-time LiDAR point cloud as an organized three-dimensional point cloud. For example, the Velodyne HDL-64E has 64 independent lasers, each one firing thousands of times per second to capture a 360-degree field of view. Therefore, we obtain a set of three-dimensional points associated with 64 elevation angles and thousands of azimuth angles. Each acquired three-dimensional point is associated with a distance measurement, an intensity value, and a high-precision GPS timestamp. Note that for the global shutter image, the pixel values are collected simultaneously by a charge-coupled device (CCD); however, for real-time LiDAR scans, the 3D points are collected in various timestamps. For the same laser beam, three-dimensional point cloud information is collected after successive emission; for different lasers, the emitted laser beams are also not synchronized; therefore, the collected three-dimensional points are not perfectly aligned on a two-dimensional regular grid. Since the arrangement of the 64 lasers follows a regular angular spacing, the point density of real-time LiDAR varies across the entire range; that is, much more three-dimensional points are collected from nearby objects than from distant objects. In addition, real-time LiDAR point clouds are subject to occlusion; that is, 3D point clouds can only be acquired from the surface of an object facing the LiDAR. In summary, some of the key characteristics of real-time LiDAR point clouds include: 

 ● Pseudo-3D points. Real-time lidar scans only reflect a specific viewpoint, so we consider its dimensionality to be pseudo-3D. 

 ● Occlusion. Each individual real-time lidar can only record the 3D environment from one viewpoint. Objects in front will block other objects behind; 

 ● Sparse point cloud. Compared with two-dimensional images, real-time lidar is usually a sparse representation of the surface of an object, especially for distant objects. It cannot provide detailed three-dimensional shape information of the object object. 

 Point cloud high-precision map. To create a point cloud map, it is necessary to stitch together point clouds obtained from cross-time scans taken by real-time LiDAR from multiple autonomous vehicles. Since there is no direct way to organize a point cloud map, we treat it as an unorganized three-dimensional point cloud. For example, for a 200 × 200 square meter high-precision map, it is necessary to acquire LiDAR point cloud data around the area and conduct 5-10 trials, resulting in more than 10 million 3D points. Since LiDAR can collect point clouds from different views, the stitched high-precision map becomes denser and shows detailed three-dimensional shape information. To summarize, some of the key properties of a point cloud map include: 

 ● Full 3D points. Point cloud maps stitch together multiple LiDAR point clouds from different views, similar to 3D data collected by scanning objects on a turntable. Point cloud maps capture more information about the surface of objects, providing a denser and more detailed 3D representation; 

 ● Irregular. The 3D points in the point cloud map are irregularly scattered in 3D space. They come from multiple LiDAR scans, and there is no laser ID association, resulting in disorganized 3D point clouds; 

 ● No occlusion. A point cloud map is a collection of three-dimensional points collected from multiple viewpoints. It depicts a static three-dimensional scene with less occlusion. 

 Dense point clouds. Point cloud maps provide dense point clouds that contain detailed 3D shape information, such as high-resolution shapes and surface normals. 

 ● Semantic point cloud. As another layer of the HD map, the semantic feature map related to traffic rules contains semantic labels for 3D scenes, including pavements, buildings, and trees. Since the semantic feature map and point cloud map related to traffic rules are aligned in 3D space, the semantic information of each 3D point cloud can be tracked. For example, a 3D point cloud labeled as a tree in a point cloud map will help improve perception, as lidar points on leaves are often noisy and difficult to identify 

 2-B 

 matrix notation 

 Representations have been at the heart of most signal processing and machine learning techniques. A good representation lays the foundation for revealing hidden patterns and structures within the data and benefits subsequent tasks. A general representation of a three-dimensional point cloud is achieved through a set that ignores any order of three-dimensional points. Let S = (pi; ai) be a set of n three-dimensional points whose pi = [Xi; Yi; Zi] ¾ R3 represents the three-dimensional coordinates of the i-th point and ai represents other properties of the i-th point. Real-time lidar scan points typically include intensity 😉 R, and point cloud maps typically include surface normals ni 😉 R3; therefore, ai = [ri; ni] ¾ R4. For efficient storage and scientific computation, matrix (or tensor) representations are very interesting. Let f be a mapping from a set of 3D points S to a matrix (or tensor) X with a shape to be determined. Therefore, the matrix of a three-dimensional point cloud is represented as X = f (S) Next we will discuss several typical methods for implementing the mapping f (▽). 

 Primitive point cloud. The most straightforward matrix representation of a 3D point cloud is to list each 3D point in the collection as a row in the matrix. 

 ![avatar]( 20210306150236610.gif) 

 The advantages of a representation based on the original point cloud are: 

 1) Simple and versatile. 

 2) It retains all the information in the original 3D point set; but the disadvantage is that it is not conducive to exploring any geometric characteristics of 3D points. This representation method is usually used in the map and positioning module of autonomous driving systems and requires high accuracy. 

 Three-dimensional point cloud voxelization. For the success of two-dimensional image processing and computer vision, three-dimensional space can be discretized into voxels, and a series of voxels can be used to represent three-dimensional point clouds. A simple discretization method is to divide three-dimensional space into equidistant non-overlapping voxels from each of the three dimensions; 

 ![avatar]( 20210306150236611.gif) 

 3D voxelization point cloud representation 

 Draw a three-dimensional space in the range H, W, D along the X, Y, and Z axes, respectively. The size of each voxel is h, w, d, respectively. The (i, j, k) voxel represents the three-dimensional voxel space. The voxel expression is as follows: 

 ![avatar]( 20210306150236608.gif) 

 The advantages of voxelization-based representation are: 

 (I) The generated voxels are associated with a natural hierarchy, with all voxels having a uniform spatial size. 

 (Ii) Data can be analyzed using off-the-shelf tools such as 3D convolution. 

 However, the disadvantages are: 

 (I) It does not consider the specific properties of ordered three-dimensional point clouds. 

 (Ii) usually results in a very sparse representation in which most voxels are empty. 

 (Iii) It involves the trade-off between resolution and memory. This representation method can be used for autonomous driving perception modules and storage of 3D point clouds. 

 Depth map. As described in Section 2-A, a real-time LiDAR scanning point cloud is essentially a series of distance measurements taken from a single location with an angular field of view; as depicted in the figure. 

 ![avatar]( 20210306150236609.gif) 

 Representation Method of Converting Lidar into Depth Two-Dimensional Map 

 We can approximately organize three-dimensional points in real-time lidar into two-dimensional distance image images. Each pixel in the depth image corresponds to a point in three-dimensional space. The pixel value is the range from the lidar to the nearest three-dimensional point in the truncated cone. Specifically, we divide the three-dimensional space along the azimuth angle [0; 2π) and the pitch angle [theta] (− π/2; π/2] with the resolution of the azimuth angle α and the pitch angle theta. The (i, j) first pixel corresponds to the truncated cone space Vi and uses a two-dimensional matrix to represent the three-dimensional point cloud. Its (i, j) element is 

 ![avatar]( 20210306150236611.gif) 

 Take into account the minimum distance value in each truncated cone space. When none of the points fall into the section space, we set the default to − 1. Note that depending on the lidar settings, depth image-based representations can also use non-uniform pitch angles. The advantages of distance image-based representations are: 

 (I) Capable of naturally simulating the way lidar captures three-dimensional points, reflecting two-dimensional surfaces in three-dimensional space; 

 (Ii) Most relevant cross-sectional spaces have one or more three-dimensional points, resulting in a compact distance-view image; however, the disadvantage is that it is difficult to model unorganized point clouds, such as those in HD maps, which can be used for perception modules. 

 Aerial view. A bird's-eye view (BEV) -based representation is a special case of three-dimensional voxelization by ignoring height. It projects 3D voxels onto a BEV image; see image. 

 ![avatar]( 20210306150236615.gif) 

 Representation method of aerial view 

 Draw a three-dimensional space in the range H and W along the X and Y axes, respectively. The size of each pixel is h, w, respectively. The (i, j) th pixel in the BEV image represents the space Vi; the three-dimensional point cloud is represented by a two-dimensional matrix. Let X (BEV) 😉 R, whose (i, j) elements are 

 ![avatar]( 20210306150236620.gif) 

 The matrix X (BEV) records occupancy in two-dimensional space. Note that the BEV-based representation has some variables. For example, instead of using binary values, MV3D [8] uses some statistical values in each cylinder space to construct X (BEV). 

 The advantages of BEV-based notation are: 

 (I) It is easy to apply technologies based on 2D vision. 

 (Ii) It is easy to integrate with information from HD maps. For example, driveable areas and intersection locations encoded in high-resolution maps can be projected onto the same two-dimensional space and fused with lidar information; 

 (Iii) Easy to use in subsequent modules such as prediction and motion planning. 

 (Iv) Object objects are always the same size regardless of distance (in contrast to depth map-based representations), which is a strong prior knowledge that makes learning problems easier; however, the drawback of this voxel two-dimensional BEV representation is that: 

 (I) It involves a serious trade-off between resolution and memory, leading to over-quantification problems in obtaining details of small objects. 

 (Ii) It does not consider the specific properties of ordered three-dimensional point clouds and cannot explain occlusion phenomena. 

 (Iii) It causes sparsity problems because most pixels are empty. This representation can be used for perception modules in autonomous driving. 

 2-C 

 Representative tool 

 3D point clouds have been extensively studied in areas such as robotics, computer graphics, computer vision, and signal processing. Here are some representative tools for processing and learning 3D point clouds. Due to the practical application of deep neural networks methods in autonomous driving, we mainly emphasize methods based on deep neural networks. 

 Non-deep learning methods. Before the advent of deep learning, there were already many traditional methods to handle 3D point clouds for various tasks. However, unlike deep neural networks, these traditional methods are difficult to describe with a single methodological framework. This is because traditional tools are specifically designed to meet the needs of each task and are developed for actual point cloud characteristics. For example, in 3D point cloud segmentation and 3D shape detection, traditional techniques are area growth based on simple geometric heuristics, or graph-based optimization, or robust estimation methods such as RANSAC [9]. 3D keypoint matching, as another important task, is closely related to 3D point cloud registration and 3D point cloud recognition. In order to solve this problem, many statistical-based methods have been developed in the traditional way to describe the geometry around three-dimensional keypoints or objects; see [10] for a more comprehensive discussion. 

 Convolutional neural networks. The motivation for using convolutional neural networks is to take advantage of off-the-shelf deep learning tools to process 3-D point clouds. Convolutional neural networks (CNNs), as a regularized form of multi-layer perceptrons, employ a series of convolutional layers that are commonly used for the analysis of images and videos. The convolutional layer operates on the input data with a set of learnable filters to produce an output representing an activation map of the filter. The advantage of convolutional layers is weight sharing, i.e. applying the same filter coefficients (weights) to any position in the 2-D image, which not only saves a lot of learnable weights, but also guarantees translation invariance, helping to avoid overfitting to limited training data. CNNs, as a general and mature learning framework, is widely used in various computer vision tasks, including classification, detection, segmentation, etc., and has achieved the most advanced performance in most tasks. 

  Based on the success of CNN methods in image and video, CNNs have also been applied to 3D point cloud data. A variety of representations have been used, including 3D voxelization-based representations, depth map-based representations, and BEV-based representations. One advantage of using CNNs to handle 3D point clouds is that convolutional algorithms can better organize local spatial relationships. In PointNet, each 3D point cloud is processed individually; in CNNs, adjacent voxels or pixels are considered jointly, providing richer contextual information. The basic operators of CNNs are generally applicable to 3D convolution for 3D voxelization-based representations and 2D convolution for depth map-based representations and BEV-based representations. 

  Even with the discretization properties of point clouds, many of the techniques and architectures developed for 2D images can be easily extended to handle 3D point clouds. Although discretization leads to inevitable loss of information, CNNs generally have reliable performance and are widely used in many tasks. As mentioned earlier, a key problem with discretized 3D point clouds is that the resulting 3D volume or 2D images are sparse. Processing empty voxels wastes a lot of computation. In summary, CNNs deal with discretized 3D point clouds. This approach inevitably modifies precise 3D position information, but still provides good empirical performance due to the prior nature of spatial relationships and the maturity of CNNs. Therefore, it is widely used in industry. 

 A PointNet-based approach. The purpose of using a PointNet-based approach is to process raw 3-D point clouds directly through deep neural networks without any discretization of the point clouds. PointNet [7] is the pioneering work to achieve this goal. Raw 3-D point clouds are essentially disordered collections, and PointNet is designed to respect this property and produce the same output regardless of the order of the input data. The key technical contribution of PointNet is to use a shared set of point-by-point multilayer perceptrons (MLPs) and then use a global pool to extract geometric features while ensuring this arrangement invariance of the raw 3D data. Although the architecture is simple, it has become a standard module for many 3D point cloud learning algorithms, and has achieved amazing performance in 3D point cloud recognition and segmentation. PointNet is a representation X (raw) based on the original point cloud. Let H ¾ R N × D be a local feature matrix, where the i-th line Hi represents the feature of the i-th point, and H ¾ R D is the global feature vector. A basic computational representation of PointNet 

 ![avatar]( c1d098dde64d751174f9a53afc58fe0c.png) 

 Where X (raw) is the feature of the i-th 3D point, MLP (L) represents L-layer MLP, which maps each 3D point to a feature space, and maxpool (😂) performs downsampling by computing the maximum (point cloud dimension) along the column; see Figure 3 (a). Note that each 3D point here passes the same MLP separately. 

 ![avatar]( 1d04fc1ea51881838080f3d5a56d27bc.png) 

   PointNet icon 

 Intuitively, MLP proposes D representative geometric shapes and tests whether these figures appear around each 3D point. The maximum pool records the best response values on all 3D points for each pattern. Essentially, the global eigenvector h summarizes the matching values of the D representative geometric patterns in the 3D point cloud, which can be used to identify the 3D point cloud. At the same time, since each 3D point passes through the same mlp separately, and max-pooling removes the dimension of the points, the entire computational block is permutation-invariant, that is, the ordering of the 3D points does not affect the output of the block. 

 The PointNet of 3D point cloud deep learning is somewhat similar to the Principal Component Analysis (PCA) of data analytics in that it is simple, versatile, and effective. Just like the Principal Component Analysis, PointNet extracts global features in the 3D point cloud. To sum up, the PointNet-based method handles the 3D point cloud in a raw point-based representation and guarantees its arrangement invariance. The effectiveness of the method has been validated in different extended domains and learning tasks of deep learning. 

 Methods based on graph theory. The motivation for using methods based on graph theory is to take advantage of the spatial relationships between three-dimensional points to accelerate end-to-end learning for deep neural networks. One advantage of CNNs is that the convolutional operators take into account local spatial relationships; however, these relationships are between adjacent voxels (or adjacent pixels) rather than between the original 3D points. To capture the local relationships between three-dimensional points, a graph structure can be introduced where each node is a three-dimensional point and each edge reflects the relationship between each pair of three-dimensional points. This graph structure is a representation of the degree of dispersion of the original object surface. The matrix representation of the N-node graph is the proximity matrix A ¾ R, and its (i, j) elements reflect the pairwise relationship between the i-th 3D point and the j-th 3D point, as shown in the figure. 

 ![avatar]( 20210306150236623.gif) 

    Diagram of a graph-based method 

 Methods based on graph theory usually consider primitive representations based on point clouds. Each column vector in point cloud X is then the data supported on Figure A above; called a graph signal. Methods for constructing graphs are K-nearest neighbor graphs, an-graphs, and learnable graphs. K-nearest neighbor graphs are graphs in which two nodes are connected by edges when their Euclidean distance is in the Kth smallest Euclidean distance from one 3D point to all other 3D points. Nearest neighbor graphs are graphs in which two nodes are connected by an edge when their Euclidean distance is less than a given threshold. K-nearest neighbor graphs and -graphs can be efficiently implemented by using efficient data structures, such as octree [11]. A learnable graph is a graph structure trainable by adjacency matrices in an end-to-end learning architecture. 

 In summary, graph theory-based methods are used to construct graph structures to capture the distribution of three-dimensional point clouds and to exploit local spatial relationships. This approach deals with three-dimensional point clouds in raw point-based representations, ensuring permutation invariance. This approach is not yet mature: although utilizing a graph can improve overall performance, graph construction is more art than science and requires additional computational costs; moreover, the deep structure of graph-based neural networks still needs more exploration [16]. 

 References 

 Swipe up to view 

 [1] A. Taeihagh and H. Si Min Lim, “Governing autonomous vehicles: emerging responses for safety, liability, privacy, cybersecurity, and industry risks,” Transport Reviews, vol. 39, no. 1, pp. 103–128, Jan. 2019.  

 [2] National Research Council, “Technology development for army unmanned ground vehicles,” 2002.  

 [3] C. Badue, R. Guidolini, R. Vivacqua Carneiro, P. Azevedo, V. Brito Cardoso, A. Forechi, L. Ferreira Reis Jesus, R. Ferreira Berriel, T. Meireles Paixo, F. Mutz, T. Oliveira-Santos, and A. Ferreira De Souza, “Self-driving cars: A survey,” arXiv:1901.04407 [cs.RO], Jan. 2019. [4] M. Bansal, A. Krizhevsky, and A. S. Ogale, “ChauffeurNet: Learning to drive by imitating the best and synthesizing the worst,” CoRR, vol. abs/1812.03079, 2018.  

 [5] C. Urmson, J. Anhalt, D. Bagnell, C. R. Baker, R. Bittner, M. N. Clark, J. M. Dolan, D. Duggins, T. Galatali, C. Geyer, M. Gittleman, S. Harbaugh, M. Hebert, T. M. Howard, S. Kolski, A. Kelly, M. Likhachev, M. McNaughton, N. Miller, K. M. Peterson, B. Pilnick, R. Rajkumar, P. E. Rybski, B. Salesky, Y-W. Seo, S. Singh, J. M. Snider, A. Stentz, W. Whittaker, Z. Wolkowicki, J. Ziglar, H. Bae, T. Brown, D. Demitrish, B. Litkouhi, J. Nickolaou, V. Sadekar, W. Zhang, J. Struble, M. Taylor, M. Darms, and D. Ferguson, “Autonomous driving in urban environments: Boss and the urban challenge,” in The DARPA Urban Challenge: Autonomous Vehicles in City Traffic, George Air Force Base, Victorville, California, USA, 2009, pp. 1–59.  

 [6] G. P. Meyer, A. Laddha, E. Kee, C. Vallespi-Gonzalez, and C. K. Wellington, “Lasernet: An efficient probabilistic 3d object detector for autonomous driving,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2019. 

  [7] C. Ruizhongtai Qi, H. Su, K. Mo, and L. J. Guibas, “Pointnet: Deep learning on point sets for 3d classification and segmentation,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2017, pp. 77–85. 

  [8] X. Chen, H. Ma, J. Wan, B. Li, and T. Xia, “Multi-view 3d object detection network for autonomous driving,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2017, pp. 6526–6534. 

 [9] M. A. Fischler and R. C. Bolles, “Random sample consensus: a paradigm for model fitting with applications to image analysis and automated cartography,” Communications of the ACM, vol. 24, no. 6, pp. 381–395, 1981. 

  [10] X-F. Hana, J. S. Jin, J. Xie, M-J. Wang, and W. Jiang, “A comprehensive review of 3d point cloud descriptors,” arXiv preprint arXiv:1802.02297, 2018.  

 [11] J. Peng and C.-C. Jay Kuo, “Geometry-guided progressive lossless 3D mesh coding with octree (OT) decomposition,” ACM Trans. Graph. Proceedings of ACM SIGGRAPH, vol. 24, no. 3, pp. 609–616, Jul. 2005.  

 [12] A. Ortega, P. Frossard, J. Kovacevic, J. M. F. Moura, and P. Vandergheynst, “Graph signal processing: Overview, challenges, and applications,” Proceedings of the IEEE, vol. 106, no. 5, pp. 808–828, 2018. 

  [13] S. Chen, D. Tian, C. Feng, A. Vetro, and J. Kovacevi ˇ c, “Fast resampling ´ of three-dimensional point clouds via graphs,” IEEE Trans. Signal Processing, vol. 66, no. 3, pp. 666–681, 2018.  

 [14] Y. Wang, Y. Sun, Z. Liu, S. E. Sarma, M. M. Bronstein, and J. M. Solomon, “Dynamic graph CNN for learning on point clouds,” ACM Transactions on Graphics (TOG), vol. 38, no. 5, November 2019.  

 [15] S. Chen, S. Niu, T. Lan, and B. Liu, “Large-scale 3d point cloud representations via graph inception networks with applications to autonomous driving,” in Proc. IEEE Int. Conf. Image Process., Taipei, Taiwan, Sept. 2019.  

 [16] G. Li, M. Muller, A. K. Thabet, and B. Ghanem, “DeepGCNs: Can ¨ GCNs go as deep as CNNs?,” in ICCV, Seoul, South Korea, Oct. 2019. 

  [17] G. Grisetti, R. Kummerle, C. Stachniss, and W. Burgard, “A tutorial ¨ on graph-based SLAM,” IEEE Intell. Transport. Syst. Mag., vol. 2, no. 4, pp. 31–43, 2010. 

  [18] D. Droeschel and S. Behnke, “Efficient continuous-time SLAM for 3d lidar-based online mapping,” in 2018 IEEE International Conference on Robotics and Automation, ICRA, 2018, Brisbane, Australia, May 21-25, 2018, 2018, pp. 1–9. 

 [19] P. J. Besl and N. D. McKay, “A method for registration of 3D shapes,” IEEE Trans. Pattern Anal. Mach. Intell., vol. 14, no. 2, pp. 239–256, 1992.  

 [20] A. Y. Hata and D. F. Wolf, “Road marking detection using LIDAR reflective intensity data and its application to vehicle localization,” in 17th International IEEE Conference on Intelligent Transportation Systems, ITSC 2014, Qingdao, China, October 8-11, 2014, 2014, pp. 584–589. 

  [21] S. Shi, X. Wang, and H. Li, “PointRCNN: 3d object proposal generation and detection from point cloud,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., Long Beach, CA, June 2019.  

 [22] B. Li, “3d fully convolutional network for vehicle detection in point cloud,” in 2017 IEEE/RSJ International Conference on Intelligent Robots and Systems, IROS 2017, Vancouver, BC, Canada, September 24-28, 2017, 2017, pp. 1513–1518. 

  [23] B. Yang, W. Luo, and R. Urtasun, “PIXOR: real-time 3d object detection from point clouds,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2018, pp. 7652–7660.  

 [24] J. Zhou, X. Lu, X. Tan, Z. Shao, S. Ding, and L. Ma, “Fvnet: 3d front-view proposal generation for real-time object detection from point clouds,” CoRR, vol. abs/1903.10750, 2019.  

 [25] B. Li, T. Zhang, and T. Xia, “Vehicle detection from 3d lidar using fully convolutional network,” in Robotics: Science and Systems XII, University of Michigan, Ann Arbor, Michigan, USA, June 18 - June 22, 2016, 2016. 

  [26] Y. Zhou and O. Tuzel, “Voxelnet: End-to-end learning for point cloud based 3d object detection,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., Salt Lake City, UT, USA, June 2018, pp. 4490–4499.  

 [27] S. Shi, Z. Wang, X. Wang, and H. Li, “Part-a2 net: 3d part-aware and aggregation neural network for object detection from point cloud,” CoRR, vol. abs/1907.03670, 2019.  

 [28] Y. Yan, Y. Mao, and B. Li, “Second: Sparsely embedded convolutional detection,” Sensors, vol. 18, no. 10, 2019. 

  [29] A. H. Lang, S. Vora, H. Caesar, L. Zhou, J. Yang, and O. Beijbom, “Pointpillars: Fast encoders for object detection from point clouds,” CoRR, vol. abs/1812.05784, 2018.  

 [30] T-Y. Lin, P. Dollar, R. B. Girshick, K. He, B. Hariharan, and S. J. ´ Belongie, “Feature pyramid networks for object detection,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2017, pp. 936–944.  

 [31] F. Yu, D. Wang, E. Shelhamer, and T. Darrell, “Deep layer aggregation,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2018, pp. 2403–2412. 

  [32] W. Liu, D. Anguelov, D. Erhan, C. Szegedy, S. E. Reed, C-Y. Fu, and A. C. Berg, “SSD: single shot multibox detector,” in Computer Vision - ECCV 2016 - 14th European Conference, Amsterdam, The Netherlands, October 11-14, 2016, Proceedings, Part I, 2016, pp. 21–37. 

  [33] T-Y. Lin, P. Goyal, R. B. Girshick, K. He, and P. Dollar, “Focal ´ loss for dense object detection,” in IEEE International Conference on Computer Vision, ICCV 2017, Venice, Italy, October 22-29, 2017, 2017, pp. 2999–3007.  

 [34] J. Ku, M. Mozifian, J. Lee, A. Harakeh, and S. L. Waslander, “Joint 3d proposal generation and object detection from view aggregation,” in 2018 IEEE/RSJ International Conference on Intelligent Robots and Systems, IROS 2018, Madrid, Spain, October 1-5, 2018, 2018, pp. 1–8.  

 [35] C. Ruizhongtai Qi, W. Liu, C. Wu, H. Su, and L. J. Guibas, “Frustum pointnets for 3d object detection from RGB-D data,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2018, pp. 918–927.  

 [36] D. Xu, D. Anguelov, and A. Jain, “PointFusion: Deep sensor fusion for 3d bounding box estimation,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn. 2018, pp. 244–253, IEEE Computer Society.  

 [37] M. Liang, B. Yang, S. Wang, and R. Urtasun, “Deep continuous fusion for multi-sensor 3d object detection,” in Computer Vision - ECCV 2018 - 15th European Conference, Munich, Germany, September 8-14, 2018, Proceedings, Part XVI, 2018, pp. 663–678. 

  [38] M. Liang, B. Yang, Y. Chen, R. Hu, and R. Urtasun, “Multi-task multi-sensor fusion for 3d object detection,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2019, pp. 7345–7353. 

  [39] G. P. Meyer, J. Charland, D. Hegde, A. Laddha, and C. VallespiGonzalez, “Sensor fusion for joint 3d object detection and semantic segmentation,” CoRR, vol. abs/1904.11466, 2019.  

 [40] A. Geiger, P. Lenz, and R. Urtasun, “Are we ready for autonomous driving? the KITTI vision benchmark suite,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., Providence, RI, June 2012, pp. 3354– 3361.  

 [41] K-L. Low, “Linear least-squares optimization for point-toplane icp surface registration,” Tech. Rep., University of North Carolina at Chapel Hill, 2004.  

 [42] J. Yang, H. Li, D. Campbell, and Y. Jia, “Go-icp: A globally optimal solution to 3d ICP point-set registration,” IEEE Trans. Pattern Anal. Mach. Intell., vol. 38, no. 11, pp. 2241–2254, 2016.  

 [43] A. Geiger, P. Lenz, C. Stiller, and R. Urtasun, “Vision meets robotics: The kitti dataset,” International Journal of Robotics Research (IJRR), 2013.  

 [44] Z. Wu, S. Song, A. Khosla, F. Yu, L. Zhang, X. Tang, and J. Xiao, “3d shapenets: A deep representation for volumetric shapes,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2015, pp. 1912–1920. 

  [45] F. Pomerleau, F. Colas, and R. Siegwart, “A review of point cloud registration algorithms for mobile robotics,” Foundations and Trends in Robotics, vol. 4, no. 1, pp. 1–104, 2015.  

 [46] H. Fathi, F. Dai, and M. I. A. Lourakis, “Automated as-built 3d reconstruction of civil infrastructure using computer vision: Achievements, opportunities, and challenges,” Advanced Engineering Informatics, vol. 29, no. 2, pp. 149–161, 2015.  

 [47] B. Reitinger, C. Zach, and D. Schmalstieg, “Augmented reality scouting for interactive 3d reconstruction,” in IEEE Virtual Reality Conference, VR 2007, 10-14 March 2007, Charlotte, NC, USA, Proceedings, 2007, pp. 219–222. 

 To be continued... 

 resource 

 3D point cloud paper and related application sharing 

 [Point cloud paper speed reading] Odometer based on lidar and positioning method in 3D point cloud map 

 3D object detection: MV3D-Net 

 Overview of 3D Point Cloud Segmentation (Part 1) 

 3D-MiniNet: Learning 2D Representations from Point Clouds for Fast and Efficient 3D LIDAR Semantic Segmentation (2020) 

 Use QT to add VTK plug-in under win to realize point cloud visualization GUI 

 JSNet: Joint Instances and Semantic Segmentation for 3D Point Clouds 

 A Survey of Semantic Segmentation of 3D Point Cloud in Large Scene 

 The outofcore module in PCL---Display of large-scale point clouds based on out-of-core octree 

 Target Segmentation Based on Local Convex 

 Point cloud labeling based on 3D convolutional neural networks 

 SuperVoxel of Point Cloud 

 Large-scale point cloud segmentation based on hyperdot graph 

 More articles can be viewed: A summary of historical articles on point cloud learning 

 SLAM and AR related sharing 

 [Open source solution sharing] ORB-SLAM3 is open source! 

 AVP-SLAM: Semantic SLAM in Automatic Parking Systems 

 [Point Cloud Paper Speed Reading] StructSLAM: Structured Line Feature SLAM 

 SLAM and AR Overview 

 Commonly used 3D depth cameras 

 Overview and Evaluation of Monocular Vision Inertial Navigation SLAM Algorithm for AR Devices 

 SLAM Review (4) Laser and Vision Fusion SLAM 

 Kimera's Semantic SLAM System for Real-Time Reconstruction 

 Overview of SLAM (3) - Vision and inertial navigation, vision and deep learning SLAM 

 Extensible SLAM Framework - OpenVSLAM 

 Gao Xiang: Challenges in unstructured road laser SLAM 

 SLAM Overview of Lidar SLAM 

 SLAM Method Based on Fisheye Camera 

 Online sharing and recording summary in the past 

 3D Model Retrieval Technology of the First Bilibili Recording 

 Application of deep learning in 3D scenes recorded and broadcast by Bilibili 

 The third Bilibili recording of CMake advanced learning 

 Point Cloud Object and Six-Degree-of-Freedom Attitude Estimation Recorded by Bilibili 

 The fifth Bilibili recording of point cloud deep learning semantic segmentation expansion 

 Pointnetlk Interpretation of the 6th Bilibili Recording 

 [线上分享录播]点云配准概述及其在激光SLAM中的应用 

 [线上分享录播]cloudcompare插件开发 

 [线上分享录播]基于点云数据的 Mesh重建与处理 

 [线上分享录播]机器人力反馈遥操作技术及机器人视觉分享 

 [线上分享录播]地面点云配准与机载点云航带平差 

 If you are interested in this article, please send "Knowledge Planet" in the background to get the QR code. Be sure to join the free Knowledge Planet according to the remarks of "Name + School/Company + Research Direction", download the pdf document for free, and communicate with more friends who love to share! 

 If the above content is wrong, please leave a comment, and welcome to correct and communicate. If there is any infringement, please contact to delete it. 

 ![avatar]( 35373ef3189a78155d2e95ccecc7a390.png) 

 Scan QR code 

                    Follow us 

 Let's share and learn together! Looking forward to friends who have ideas and are willing to share joining the free planet to inject fresh vitality of love and sharing. The topics shared include but are not limited to 3D vision, point clouds, high-precision maps, autonomous driving, and robotics and other related fields. 

 Sharing and cooperation method: WeChat "920177957" (note required) Contact email: dianyunpcl@163.com, enterprises are welcome to contact the official account for cooperation. 

