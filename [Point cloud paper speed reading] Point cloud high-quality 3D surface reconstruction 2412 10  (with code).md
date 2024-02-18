Point cloud PCL free knowledge planet, point cloud paper speed reading. 

 标题：Local Implicit Grid Representations for 3D Scenes 

 本人:Chiyu "Max"1.2 Avneesh South 

 Planet ID: particle 

 Welcome to join the free knowledge planet, get PDF papers, and welcome to forward Moments to share your happiness. 

 Abstracts of papers 

 Shape prior knowledge learned from point cloud data is often applied in 3D reconstruction from local or noisy point cloud data. However, since typical 3D autoencoders cannot handle their scale, complexity, or diversity, there is no such shape predictor in indoor scenes. In this paper, we introduce a Local Implicit Grid representation, a new 3D shape representation aimed at scalability and generality. Most 3D surfaces share geometric details at some scale. In this paper, an autoencoder is trained to learn how to embed 3D point cloud shapes of this size. Then, we use the decoder as a component in a shape optimization that resolves a set of latent codes on a regular grid of overlapping crops, such that the interpolation of the decoded local shapes matches partial or noise observations. And the value of this method in 3D surface reconstruction from sparse point observations is proved, and experiments show that this method is significantly better than other methods. 

 ![avatar]( 20200524221321834.JPG) 

 Main contributions 

 A Local Implicit Grid (LIG) representation is proposed, which is a regular grid composed of overlapping local regions, each of which is encoded by implicit eigenvectors. 

 The main contributions of this work are: 

 • Proposed local implicit mesh representation of geometric shapes, learning and leveraging geometric features on part point clouds, and related methods such as overlapping implicit mesh mechanisms and implicit mesh optimization methods to represent and reconstruct scenes with high reducibility. 

 • Compared with related methods for learning prior knowledge of the entire object, the local-based method significantly improves the versatility. 

 The method is applied to the challenging task of scene reconstruction from sparse point samples and shows significant improvement over state-of-the-art methods. 

 ![avatar]( 20200524221427849.JPG) 

 Paper Atlas   

 ![avatar]( 20200524221441270.JPG) 

 This widget representation can be generalized across object categories and is easily scalable to large scenes. By positioning the implicit function in the mesh, the entire scene can be reconstructed from point cloud data by optimizing the hidden mesh. 

 ● English abstract 

 ![avatar]( 20200524221511376.JPG) 

 Shape priors learned from data are commonly used to reconstruct 3D objects from partial or noisy data. Yet no such shape priors are available for indoor scenes, since typical 3D autoencoders cannot handle their scale, complexity, or diversity. In this paper, we introduce Local Implicit Grid Representations, a new 3D shape representation designed for scalability and generality. The motivating idea is that most 3D surfaces share geometric details at some scale – i.e., at a scale smaller than an entire object and larger than a small patch. We train an autoencoder to learn an embedding of local crops of 3D shapes at that size. Then, we use the decoder as a component in a shape optimization that solves for a set of latent codes on a regular grid of overlapping crops such that an interpolation of the decoded local shapes matches a partial or noisy observation. We demonstrate the value of this proposed approach for 3D surface reconstruction from sparse point observations, showing significantly better results than alternative approaches.  

