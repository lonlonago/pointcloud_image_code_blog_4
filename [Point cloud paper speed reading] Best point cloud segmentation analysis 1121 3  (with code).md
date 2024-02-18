Point cloud PCL free knowledge planet, point cloud paper speed reading. 

 标题：Learning to Optimally Segment Point Clouds 

 作者：Peiyun Hu, David Held 

 Planet ID: particle 

 Welcome to join the free knowledge planet, get PDF papers, and welcome to forward Moments to share your happiness. 

 Abstracts of papers 

 We propose an approach that combines graph-theoretic search with data-driven learning: searching a set of candidate segmentation for candidate segmentation with a high composite objectivity score. We demonstrate that if the segmentation is scored according to the lowest objectivity in the segmentation, then there is an efficient algorithm that can find the optimal worst-case segmentation in an exponential number of candidate segmentation. In addition, we also propose an efficient algorithm for the average case. For evaluation, we reuse the KITTI 3D detection as a segmentation benchmark, and empirically demonstrate that our algorithm performs significantly better on segmentation point clouds than past bottom-up segmentation methods and top-down object-based algorithms. 

 Main contributions 

 • Use geometric constraints to reduce the number of candidate partitions and build a tree structure 

 • Utilize tree structure for optimal segmentation search, and propose an efficient search algorithm that can be applied to dynamic programming 

 This paper uses KITTI as an experimental dataset, and the results of point cloud segmentation and point cloud instance segmentation are shown in the following figures TABLE I and TABLE II: The proposed method performs worse in common classifications such as car than SECOND ++, but performs better in rare classifications such as misc. 

 Paper Atlas 

 ![avatar]( 2020052422170361.JPG) 

 ● English abstract 

 ![avatar]( 20200524221728204.JPG) 

 We focus on the problem of class-agnostic instancesegmentation of LiDAR point clouds. We propose an approachthat combines graph-theoretic search with data-driven learning:it searches over a set of candidate segmentations and returnsone where individual segments score well according to a datadriven point-based model of “objectness”. We prove that ifwe score a segmentation by the worst objectness among itsindividual segments, there is an efficient algorithm that findsthe optimal worst-case segmentation among an exponentiallylarge number of candidate segmentations. We also present anefficient algorithm for the average-case. For evaluation, werepurpose KITTI 3D detection as a segmentation benchmarkand empirically demonstrate that our algorithms significantlyoutperform past bottom-up segmentation approaches and topdown object-based algorithms on segmenting point clouds.  

