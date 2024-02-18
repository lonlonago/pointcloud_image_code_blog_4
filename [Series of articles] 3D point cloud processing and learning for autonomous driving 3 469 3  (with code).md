标题：3D Point Cloud Processing and Learning for Autonomous Driving 

 作者：Siheng Chen, Baoan Liu, Chen Feng, Carlos Vallespi-Gonzalez, Carl Wellington 

 Compiler: Point Cloud PCL 

 Source: arXiv 2020 

 This article is for academic sharing only. If there is any infringement, please contact to delete it. Welcome to join the free knowledge planet, get PDF papers, and welcome to forward Moments. If there is any error in the content, please comment and leave a message. Please do not reprint without permission! 

 The official account is dedicated to sharing articles and technologies related to point cloud processing, SLAM, 3D vision, and high-precision maps. Welcome to join us and make progress together with each exchange. If you are interested, please contact WeChat 920177957. 

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

 3. Creation of high-precision maps and processing of 3D point clouds 

 3-A 

 Overview of high-definition map creation module 

 A high-definition (HD) map for autonomous driving is an accurate heterogeneous map representation of a static 3D environment and traffic rules. It typically consists of two map layers: 

 The main reason for creating offline high-precision maps is that real-time detection is too challenging to understand the traffic rules in the road. For example, based on existing technology, it is difficult for autonomous vehicles to determine the correct lane in real time at the intersection of complex lane mergers and forks. In contrast, all traffic rules and environmental information can be easily encoded into high-precision maps, which go through the offline process under human supervision and quality assurance. High-precision maps provide powerful and indispensable prior knowledge, fundamentally simplifying the design of multiple modules in autonomous driving systems, including positioning, perception, prediction, and motion planning. Therefore, high-precision maps are widely regarded as an indispensable component of autonomous driving. The role of high-precision maps is as follows: 

 Positioning a priori. The role of positioning is to locate the pose of autonomous vehicles. In high-precision maps, point cloud maps and semantic features related to traffic rules (such as lane markings and markers) are usually used as a priori for map-based positioning. These priors are used to register the point cloud map with the real-time lidar scanning point cloud, so as to obtain the real-time high-precision motion pose of the autonomous vehicle. 

 A priori knowledge of perception. The role of perception is to detect all objects in the scene, as well as their internal states. The perception module can use high-precision maps as a priori for detection. For example, the position of traffic lights in HD maps is often used as a perception priori for traffic light state estimation. Taking the point cloud map as a priori, the real-time LiDAR scanning point cloud can be divided into foreground points and background points. The background points, that is, those points located on static scenes, such as road surfaces and tree trunks, can then be removed, and only the front attractions are provided to the perception module. This form can greatly reduce the amount of calculation and improve the accuracy of object detection. 

 Predictive prior knowledge. The role of prediction is to predict the future trajectory of each object in the scene. In high-precision maps, the geometric structure and connectivity of roads and lanes in 3D are important prerequisites for the prediction module. This prior knowledge can be used to guide the predicted target trajectory to follow the lane. 

 A priori knowledge of motion planning. The role of motion planning is to determine the motion trajectories of autonomous vehicles. In high-precision maps, semantic features related to traffic rules (such as lane geometry and connectivity, traffic lights, traffic signs, and lane speed limits) are essential prerequisites for the motion planning module. This a priori knowledge is used to guide predetermined trajectories to follow the correct lanes and obey stop signs and other traffic signs. Since high-precision maps are important for autonomous driving, high-precision maps must be created and timely updated. To achieve this, complex engineering procedures are often required, utilizing machine learning techniques and human supervision to analyze the acquired data from multiple modes. The standard map creation module includes two core components: 3D point cloud splicing and semantic feature extraction; 3D point cloud splicing merges real-time lidar scanning point cloud data collected from multiple vehicles across time into the point cloud map; semantic feature extraction extracts semantic features such as lane geometry and traffic lights from the point cloud map. 

 ![avatar]( 20210306150344689.gif) 

 As shown in the figure, a standard high-precision map generation system consists of two core components: 3D point cloud stitching and semantic feature extraction. 3D point cloud stitching usually adopts the method of SLAM based on graph theory, and the semantic feature extraction involves machine learning and human supervision of the iterative process. A key component of graph-based SLAM is the attitude graph, which models the relationship between LiDAR poses. Nodes are the edges between the LiDAR pose and the non-aligned level representing two frames of LiDAR poses. The final output includes a point cloud map, which is a dense 3D point cloud, and a semantic feature map related to traffic rules, which contains the locations of road signs, traffic signs, and traffic lights 

 3-B 

 Splicing of 3D Point Clouds 

 The goal of 3D point cloud splicing is to generate high-precision point cloud maps using sensor data collected by the fleet at different time periods. Since point cloud maps are related to the prior accuracy of all maps, any local part of the point cloud map requires centimeter-level accuracy. In order to quickly create and update city-level high-precision maps, the 3D point cloud splicing process must be highly robust and efficient. 

 A fundamental problem in 3D point cloud stitching is to estimate the 6-degree-of-freedom attitude, also known as the LiDAR attitude, for each LiDAR scan. Think of the map frame as a standardized global frame, and the LiDAR frame as a self-moving point cloud frame of the autonomous vehicle when the timestamp of the corresponding real-time LiDAR point cloud is acquired. Then, the LiDAR attitude is the transformation between the map frame and the LiDAR frame. It includes three-dimensional translation and three-dimensional rotation. Note that the 6-degree-of-freedom attitude can be represented as a 4 × 4 homogeneous transformation matrix. With the LiDAR attitude, all LiDAR scanning point clouds can be synchronized into a standardized global frame and integrated into a dense 3D point cloud. To estimate the attitude of the LiDAR, a commonly used technique is the Synchronous Localization and Mapping (SLAM) technique. Let Si and Sj be the i-th and j-th real-time lidar scans, respectively. Its SLAM expression is: 

 ![avatar]( 4aac2b6e656cf60478147736b353736b.png) 

 Where pi is the 6-degree-of-freedom attitude associated with the i-th real-time lidar scan point cloud, h_Si; Sj (pi, pj) represents the negative logarithmic maximum likelihood between Si and Sj, and g (〃) represents the negative logarithmic likelihood of the difference between the predicted lidar position in the map frame and the GPS measurement. h_SiSj represents the objective function of the iterative closest point (ICP) algorithm and minimizes the objective function of the ICP algorithm. 

 SLAM is an important research field in the field of robotics. At present, a large number of studies have been devoted to solving optimization problems. For example, filter-based SLAM solves optimization problems in an approximate real-time manner. Based on real-time sensor measurements, Bayesian filtering is used to iteratively predict and optimize maps and lidar poses. On the other hand, graph-based SLAM optimizes all lidar poses by using all sensor measurements across time. It constructs an attitude graph to simulate the relationship between lidar poses. Intuitively, the weight of each edge is either the point-to-point distance between two lidar scan points or the point-to-surface distance. Therefore, solving the SLAM equation is equivalent to minimizing the sum of the weights of the edges of the pose graph. 

 For the creation of city-level high-resolution maps, SLAM solutions must meet the following requirements: 

 Accuracy of higher local and global maps. Local accuracy indicates that the lidar attitude of one local area is accurate relative to another area; global accuracy indicates that all lidar attitudes in the entire high definition map are accurate relative to the global frame. For SLAM solutions, since the autonomous driving software module requires high-precision local environment of high-precision maps, the constructed map must achieve local accuracy of centimeters per microradian; centimeter-level global accuracy helps to speed up the update process of high definition maps, especially for city-scale applications; 

 High robustness. The SLAM solution needs to process noise sensor measurements collected by multiple vehicles in complex scenarios and complex driving conditions, and has 

 High efficiency. SLAM solutions need to handle the optimization of more than hundreds of millions of LiDAR poses. To achieve higher accuracy and robustness, graph-based SLAMs have a better choice than filter-based SLAMs because the form of global optimization makes graph-based SLAMs inherently more precise; however, solving city-scale graph-based SLAM problems with high efficiency and robustness remains a challenge for two main reasons. First, the scale of the scenario is enormous. Since the core step of the optimization algorithm is to solve a series of equations associated with n × n matrices, where n is the total number of LiDAR poses, solving the optimization problem in a brute-force manner is expensive. For city-scale maps, n may be hundreds of millions, which has a great impact on the computational efficiency and numerical stability of the optimization algorithm. Secondly, since the sensor data is collected under complex driving conditions, the calculation accuracy of the edge weights of the attitude map is low. For example, the mismatch calculation between point clouds scanned by continuous lidar may be affected by moving objects. 

 To solve this problem efficiently, graph-based SLAM and hierarchical refinement forms can be employed [18]. The function of hierarchical refinement methods is to provide good initialization for global optimization, making optimization both fast and accurate. The hierarchical refinement form distinguishes between two types of edges in the attitude graph: adjacent edges and closed edges. Adjacent edges are to model the relationship between two lidar poses, whose corresponding lidar scan points are successive frames from the same dataset; cyclic closed edges are to model the relationship between two lidar poses, whose corresponding lidar point clouds are point cloud frames collected at the same location from different datasets (different vehicles or across time). To handle both types of edges, the hierarchical refinement form consists of two steps: 

 (1) Optimize adjacent edges, including LiDAR pose maps from a single dataset. 

 (2) Optimize loop closed edges, including LiDAR pose across time datasets. 

 In the first step, sensor measurements from multiple modes (including IMU, GPS, odometer, camera, and LiDAR) can be fused together, rather than simply relying on aligning LiDAR scans to calculate adjacent edges. Because successive LiDAR scans have similar LiDAR attitudes, this step is usually easy and provides extremely high accuracy. In the second step, the loop closed edges are calculated by aligning the LiDAR scans with the ICP algorithm. After these two steps, global optimization is performed. Since most edges in the attitude graph are adjacent edges, high-precision optimization can be performed with the first step, so the hierarchical refinement form provides good initialization for global optimization. Therefore, the hierarchical refinement method can greatly reduce the computational effort of the entire pose map optimization and improve the robustness of the global optimization. 

 3-C 

 Point Cloud Semantic Feature Extraction 

 The purpose of semantic feature extraction is to extract semantic features related to traffic rules from point cloud maps, such as geometric properties of lanes, lane connectivity, traffic signs and traffic lights, etc. This module requires high accuracy and recall rate. For example, losing a traffic light in a city high-precision map may cause serious problems for perception and motion planning modules, thus seriously compromising the safety of autonomous driving. The semantic feature extraction component usually consists of two iterative steps: 

 For automatic feature extraction, standard machine learning techniques are based on convolutional neural networks. The input is typically a collection of LiDAR ground images and camera images associated with the corresponding real-time LiDAR scan point cloud. A BEV-based representation of a point cloud map obtained in the 3D point cloud stitching of LiDAR ground images rendering, where the value of each pixel is the ground height and laser reflectivity of each LiDAR point. The output is typically a semantic segmentation of a LiDAR ground image or camera image. These networks follow a standard image segmentation architecture. After the output is obtained, pixel-by-pixel semantic labels are projected back to the point cloud map. By simulating the projected 3D points into 3D splines or 3D polygons, a semantic feature map related to traffic rules is obtained. Please note that the results of human editing jobs can also be used as an important training data source for automatic feature extraction algorithms, so these two steps form a positive feedback loop to improve the accuracy and efficiency of high-precision map production. 

 3-D 

 Map creation challenges 

 There are still some challenges in the production of high-precision maps. 

 Global centimeter-level point cloud map. Urban large-scale scene updates with global precision point cloud maps are of great help, and changes in urban features usually occur in local areas. Ideally, map updates should focus on the target part of the attitude map; however, point cloud maps with high local accuracy but no global accuracy will not be able to freely access the target scene from a global perspective and guarantee its overall accuracy. In contrast, for point cloud maps with high global accuracy, one can concentrate on updating the target part of the attitude map, thus significantly reducing the computational scale; however, for graph-based SLAM, it is a challenge to mandate that the map has global accuracy. This is because the global optimization method of graph-based SLAM tends to distribute the error of each edge evenly in the graph. Therefore, even if GPS observations are accurate, the corresponding LiDAR attitude will be skewed after global optimization. Enforcing centimeter-level global accuracy for point cloud maps can be particularly challenging where GPS signals are not available, such as in building canyons, tunnels, and underground garages. 

 Automatic Semantic Feature Extraction. Although semantic segmentation methods based on 3D point clouds and camera images have been widely studied, the automatic extraction of lane connectivity representing lane interrelationships in intersections and traffic lights remains a challenge. This is due to limited training labels and complex traffic conditions. Currently, solutions for extracting complex semantic features such as traffic lights to lane information still mainly rely on manual control, which is both time-consuming and costly. 

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

 If you are interested in this article, please send "Knowledge Planet" in the background to get the QR code. Be sure to join the free Knowledge Planet according to the remarks of "Name + School/Company + Research Direction", download the pdf document for free, and communicate with more friends who love to share! 

 If the above content is wrong, please leave a comment, and welcome to correct and communicate. If there is any infringement, please contact to delete it. 

 ![avatar]( 71e262f84eca33e3d28098bb26ccc3b7.png) 

 Scan QR code 

                    Follow us 

 Let's share and learn together! Looking forward to friends who have ideas and are willing to share joining the free planet to inject fresh vitality of love and sharing. The topics shared include but are not limited to 3D vision, point clouds, high-precision maps, autonomous driving, and robotics and other related fields. 

 Sharing and cooperation method: WeChat "920177957" (note required) Contact email: dianyunpcl@163.com, enterprises are welcome to contact the official account for cooperation. 

