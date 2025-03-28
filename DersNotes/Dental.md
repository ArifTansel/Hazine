### 2.3 Segmentation Methods

#### 2.3.1 General Point Cloud Segmentation Methods

This section explores general point cloud segmentation methods, which are independent of the type of point cloud data (e.g., scene point cloud, LiDAR point cloud, or shape point cloud).

- **PointNet**: PointNet is a highly effective deep learning architecture for point cloud processing tasks, including object classification, part segmentation, and semantic parsing of scenes. It captures the global features of the point cloud, offering a strong understanding of the overall structure.
    
- **PointNet++**: Building on PointNet, PointNet++ introduces hierarchical feature learning. This enhancement enables the network to better understand local neighborhoods within the point cloud, providing a more detailed segmentation.
    
- **DGCNN**: DGCNN (Dynamic Graph CNN) addresses the challenge that point clouds, being unordered sets of points, inherently lack topological information. DGCNN introduces EdgeConv, a module that builds dynamic graphs at different network layers, enabling the capture of local neighborhood and topological features.
    
- **PointMLP**: PointMLP presents a residual network architecture for point clouds, achieving competitive performance without relying on complex local geometric extractors. This makes the network faster while maintaining strong results.
    
- **PCT**: Inspired by the success of Transformer networks in natural language and image processing, PCT introduces a transformer-based architecture for point cloud processing. It carefully designs the input network with farthest point sampling and nearest neighbor search, allowing the network to benefit from both local and global structures.
    
- **BAAFNet**: BAAFNet integrates geometric and semantic features in a bilateral fashion to extract local context details from point clouds. It processes multiple resolutions of the point cloud, reducing ambiguity and providing a comprehensive understanding of each point's uniqueness.
    

#### 2.3.2 Tooth Point Cloud Segmentation Methods

This section focuses on methods specifically designed for tooth point cloud segmentation, which are influenced by the general segmentation methods mentioned earlier.

- **MeshSegNet**: MeshSegNet, proposed by Lian et al., introduces a novel architecture where graph-constrained learning modules extract multi-scale contextual features in a hierarchical manner. The network then integrates local-to-global geometric features for an in-depth characterization of tooth mesh cells. It draws heavily from the PointNet architecture but distinguishes itself by using an adjacency matrix to better understand local geometric features.
    
- **GAC**: GAC, proposed by Zhao et al., uses a dual-branch network. The global feature branch is similar to PointNet, while the local feature branch introduces LSAM (Local Semantic Attention Module). LSAM, inspired by EdgeConv from DGCNN, dynamically computes graph edge weights and learns local context using both positional and semantic features. A graph attention mechanism is used to aggregate the information from these dynamic graphs.
    
- **TSGCNet**: TSGCNet, developed by Zhang et al., employs a two-stream network to process coordinates and point normals separately. Like GAC, it uses graph attention layers to summarize graph weights. However, TSGCNet distinguishes itself by initially handling coordinates and normals separately to fully leverage their distinct roles in characterizing mesh cells.
    
- **MBESegNet**: MBESegNet, proposed by Li et al., is designed to handle hierarchical and multi-scale information. Similar to BAAFNet, this method enhances local features bidirectionally using both geometric and semantic information to improve segmentation accuracy.