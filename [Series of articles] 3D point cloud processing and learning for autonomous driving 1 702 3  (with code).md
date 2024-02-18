标题：3D Point Cloud Processing and Learning for Autonomous Driving 

 作者：Siheng Chen, Baoan Liu, Chen Feng, Carlos Vallespi-Gonzalez, Carl Wellington 

 Compiler: Point Cloud PCL 

 Source: arXiv 2020 

 This article is for academic sharing only. If there is any infringement, please contact to delete it. Welcome to join the free knowledge planet, get PDF papers, and welcome to forward Moments. If there is any error in the content, please comment and leave a message. Please do not reprint without permission! 

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

 1. Introduction 

 1-A 

 The significance, history and current situation of autonomous driving 

 As one of the most exciting engineering projects in the world today, autonomous driving is an aspiration of many researchers and engineers. It is a goal that may fundamentally redefine the future of human society and the daily life of everyone. Once autonomous driving becomes mature, we will witness a huge transformation in public transportation, infrastructure and the face of cities. The world looks forward to using autonomous driving to reduce traffic accidents caused by driver error, save drivers' time and free up labor, save parking spaces, and especially relieve traffic pressure in urban areas [1]. 

 In order to continuously approach the goal of autonomous driving, it has taken decades of efforts. From the 1980s to the DARPA Challenge in 2004 and the DARPA Urban Challenge in 2007, autonomous driving research was mainly conducted in the United States and Europe, and progress was made in autonomous driving capabilities in various scenarios [2]. 

 In 2009, Google began a research project on autonomous cars, and later created Waymo to commercialize this achievement, building on its early technological success. In 2013-2014, the rise of deep neural networks revolutionized practical computer vision and machine learning. The emergence of these technologies led to the belief that many of the technical bottlenecks of autonomous driving could be fundamentally addressed. In 2015, Uber created the Uber Advanced Technology Group, with the goal of enabling autonomous driving to achieve scalable shared services. This goal has become a widely adopted deployment strategy in the industry. At present, there are many high-tech companies, automakers and startups working on autonomous driving technology, including Apple, Aptiv, ArgoAI, Aurora, Baidu, GM Cruise, Didi, Lyft, Pony.ai, Tesla, Zoox, major automotive companies, and many others [3]. These companies all have this ambitious goal to reach SAE level 4 autonomous driving in the near future. Although many groups in industry and academia have made significant progress, there is still a lot of work to be done. Achieving autonomous driving requires a joint effort of industry and academia. Recently, there has been a lot of discussion and assumptions about the progress and future of autonomous driving; however, few ideas have been made public by those pushing industrial-grade autonomous driving technology from the front lines. In this paper, we provide a unified perspective from both practitioners and researchers. 

 1-B 

 A complete autonomous driving system module 

 The autonomous driving system mainly includes sensors, map creation, positioning, perception, prediction, path planning, motion planning, and control modules [5]; see Figure 1. 

 ![avatar]( ffa7e0be5ca7342851fe317ce38ea03a.png) 

 Figure 1 Block diagram of a classic autonomous driving system. 

 The high-precision map is generated offline. At runtime, the online system is assigned a destination. The system then senses the environment, locates itself onto the map, perceives the world around it, and makes corresponding predictions about the movements of these objects. The motion planner uses this predictive information to plan the safe-form trajectory of the autonomous vehicle (AV) for a safe and effective route to be executed along with the vehicle controller. Note that two types of three-dimensional point clouds are used in this autonomous driving system: a point cloud map created by the map creation module and used by the positioning module, and a real-time lidar point cloud collected by the sensing module and used by the positioning and sensing module. 

 Sensing Module. In order to ensure the reliability of the system, autonomous driving often requires multiple types of sensors. Cameras, radio detection and ranging (radar), light detection and ranging (lidar), and ultrasonic sensors are the most commonly used of these sensors. Lidar is a representation of an accurate three-dimensional point cloud that can directly provide a scene. Although 3D reconstruction and depth estimation techniques based on 2D images have been significantly improved with the development of deep learning-based computer vision algorithms, the resulting estimates are still not always accurate or reliable. In addition to algorithmic limitations, fundamental bottlenecks include the exponential distance error growth inherent in depth estimation, poor performance in low light, and high computational cost of processing high-resolution images. On the other hand, LiDAR measures 3D information of a scene through direct physical sensors. Real-time LiDAR scans consist of a large number of 3D points, called 3D point clouds. Each 3D point records the distance from the LiDAR to the outer surface of the object and can be converted into precise 3D coordinates. These 3D point clouds are very valuable for autonomous vehicles to self-locate and detect surrounding objects in the 3D world. The vast majority of companies and researchers rely heavily on LiDAR to achieve more reliable autonomous vehicles [6]. This is why we believe that advanced 3D point cloud processing and learning technologies are essential in the field of autonomous driving. 

 Map creation module. The task of map creation is to create a high-precision (HD) point cloud map, which is an accurate heterogeneous map representation of the static three-dimensional environment and traffic rules. A high-precision map typically contains two map layers: a point cloud map, which represents the three-dimensional geometric information of the surrounding environment; and a semantic feature map related to traffic rules, containing road boundaries, lanes, traffic signs, traffic lights, etc. The two map layers are aligned in three-dimensional space and are able to provide detailed navigation information. As a map layer, a point cloud map is a dense three-dimensional point cloud, which is mainly used to provide positioning prior knowledge. Unlike ordinary maps designed for human travel, high-precision maps are designed for autonomous vehicles. The map creation module is crucial because high-resolution maps provide valuable prior environmental information; see Section 3 for details. 

 Positioning module. The task of positioning is to find the self-position of the autonomous vehicle relative to the reference position in the high-precision map. This module is crucial because the autonomous vehicle must position itself in order to use the correct lane and other important priority choices in the high-precision map. One of the core technologies is 3D point cloud registration; that is, to estimate the precise position of the autonomous vehicle by matching real-time LiDAR scans with offline high-precision maps; see Section 4 for details. 

 Perception. Perception is the task of perceiving the surrounding environment and extracting information related to navigation. Since the perception module is the vision system of an autonomous vehicle, it needs to detect, track and classify objects in a three-dimensional scene, so this module is crucial. It was once considered to be the technical bottleneck of autonomous driving. In recent years, with the development of large-scale training data and advanced machine learning algorithms, the overall performance of the perception module has been greatly improved. Some core technologies include two-dimensional object detection and three-dimensional object detection. Two-dimensional object detection has been relatively mature, while three-dimensional object detection is based on real-time lidar scanning and has become an increasingly popular research topic. See Section 5 for details. 

 Prediction. The task of prediction is to predict the potential future trajectory of each object in a 3D scene. This module is very important because autonomous vehicles need to know the likely future behavior of nearby objects in order to plan safe trajectories. 

 Path planning. Path selection is the task of designing a high-level path for an autonomous vehicle from its starting position to its destination. The output of this module provides a high-level guide to the motion planning module. 

 Motion planning. The task of motion planning is to design the trajectory of an autonomous vehicle based on its current state, surroundings, and destination. This module is very important because autonomous vehicles need to know how to react to their surroundings. 

 Control module. Control is the task of executing commands from the motion planning module. It is responsible for controlling the actuators of the steering wheel, throttle, and brakes. 

 1-C 

 3D point cloud processing and learning 

 As mentioned earlier, lidar provides indispensable 3D information for autonomous driving. We will now continue to introduce processing and learning techniques that convert raw measurements into useful information. 

 The role of point cloud autonomous driving. Two types of three-dimensional point clouds are commonly used in autonomous vehicles: real-time lidar scanning point clouds and point cloud maps, which are one layer in a high-precision map. Point cloud maps provide a priori environmental information: The localization module uses the point cloud map as a reference value for three-dimensional point cloud registration to determine the position of autonomous vehicles, and the perception module uses the point cloud map to help segment the foreground and background point clouds. On the other hand, the localization module uses real-time lidar to register the point cloud map, and the perception module uses real-time lidar point clouds to detect surrounding objects in a three-dimensional scene. Therefore, the processing and learning of three-dimensional point clouds is essential for building map generation, localization, and perception modules in an autonomous driving system. 

 Recent advances in academia. Algorithms for sensor acquisition of data and data feeding. In the development of radar, acoustic sensors, and communication systems, one-dimensional signal processing has undergone rapid development over the past century, having a revolutionary impact on digital communication systems. With the popularity of cameras and televisions, two-dimensional image processing has undergone rapid development over the past 30 years, leading to significant changes in the fields of photography, entertainment, and surveillance. With the development of industrial robotics, autonomous driving technology, and augmented reality, three-dimensional sensing technology has been rapidly developed. At the same time, processing and learning algorithms for three-dimensional point clouds have also begun to receive extensive attention in academia. The following discussion is divided into two parts: 3D point cloud processing (processing 3D point clouds from a signal processing perspective) and 3D point cloud learning (processing 3D point clouds from a machine learning perspective). 

 Three-dimensional point cloud processing. Three-dimensional point cloud processing is the process of analyzing and modifying a three-dimensional point cloud through various mathematical and computational algorithms to optimize its transmission, storage, and quality. Although processing algorithms can vary widely, many processing methods extend from one-dimensional signal processing and two-dimensional image processing. For example, 3D point cloud compression corresponds to image compression, the purpose of which is to reduce the storage or transmission cost of the 3D point cloud; 3D point cloud denoising corresponds to image denoising, the purpose of which is to remove noise from the 3D point cloud; 3D point cloud registration is the three-dimensional correspondence of image registration, the purpose of which is to align two or more three-dimensional point clouds of the same scene; 3D point cloud downsampling and upsampling correspond to image scaling, the purpose of which is to change the resolution (number of point clouds) in the three-dimensional point cloud. 

 3-D point cloud deep learning. 3-D point cloud deep learning is the process of interpreting and understanding 3-D point clouds. With the powerful tools of deep neural networks, computer vision researchers aim to extend deep learning from images and videos to 3-D point clouds. The two main learning problems are the recognition and segmentation of 3-D point clouds. Similar to the case of 2-D images, the purpose of 3-D point cloud recognition is to divide a given 3-D point cloud into a predefined category, while the purpose of 3-D point cloud segmentation is to divide a given 3-D point cloud into multiple parts. Due to the irregular format of 3-D point clouds, one of the biggest challenges in designing learning algorithms is to build efficient data structures to represent 3-D point clouds. Some algorithms convert 3D point clouds into regular 3D voxels, so 3D convolution can be used for analysis; however, they must be tradeoff between resolution and memory. To deal directly with raw point clouds, PointNet [7] uses a point-by-point multilayer perceptron (MLP) and a maximum pool to ensure arrangement invariance. Afterwards, a series of 3D deep learning methods are based on PointNet networks. 

 The relationship between academia and industry. The technical transformation from one-dimensional time series to two-dimensional images is very natural, because both types of data support regular spacing structures; however, the technical transformation from two-dimensional images to three-dimensional point clouds is not simple, because these points are irregularly scattered in three-dimensional space. Practitioners have also proposed many popular methods for processing three-dimensional point cloud data, which has brought more inspiration. Therefore, there is a lot of room for collaboration between researchers and practitioners in three-dimensional point cloud processing and learning, which can solve some fundamental tasks, thus speeding up the process of autonomous driving. 

 1-D 

 outline 

 The second section introduces the key elements of 3D point cloud processing and learning. Firstly, the conventional characteristics of 3D point clouds are explained, and then various methods for representing 3D point clouds are introduced. Then common methods for processing and learning 3D point clouds are introduced. 

 The latest methods and challenges related to 3D point cloud processing and learning in the Mapping Creation, Localization and Perception module of the autonomous driving system are presented in Sections 3, 4 and 5 respectively. These three modules are given special consideration as they rely heavily on 3D point clouds for reliable performance. In each module, the specific work content of this module will be discussed; why 3D point cloud processing and learning is very important to this module; and how 3D point cloud processing and learning can play a role in this module. 

 Section VI concludes with a discussion and indicates the way forward. Views from academia and industry are compared, followed by the latest qualitative results. 

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

