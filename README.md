# Design and Evaluation of Motion Planners for Quadrotors
*What two-stage quadrotor motion planner should I use for my environment?* 

![Experiment of Quadrotor flying through a small maze](https://github.com/KumarRobotics/kr_mp_design/blob/main/pics/real_exp_maze.png)

This repo gives a guideline on what motion planners to use for different environments. This repo provided three tools:
1. A set of two-stage motion planners.
2. A set of maps generators (obstacle, maze, real datasets).
3. A evaluation metric for environment called Environment Complexity Signature (ECS) you can use to evaluate your environment and choose the right motion planner.

### Planners
#### Frontend planners
1. Jump Point Search (JPS)
2. RRT*
3. Motion Planning Primitive (MPL)
4. Stable Sparse RRT (SST)
5. Dispersion Planner 
#### Backend planners
1. GCOPTER (Differential Flatness)
2. ALTRO (Indirect Trajectory Optimization)
### Maps
All maps are of size 10m x 5m x 5m. We provide three types of maps:
1. Obstacle Map: Random 3D maps with obstacles, where the density of each type can be specified.
2. Maze Map (Image Map Loader): Random 3D maze maps from a 2D png file. Load your own images by specifying a png file or folder.
3. Real Datasets (pcd Map Loader): We cropped data from STPLS3D and M3ED to the same size. Load your own point cloud map by inputting a pcd file.


### Environment Complexity Signature (ECS)
ECS measures the complexity of an environment. It consists of density index, clutter index and structure index. Please see the paper for which planner performs best in each ECS range. *(Coming Soon)* You can use ECS to evaluate your environment and choose the right motion planner.

## Installation
1. Planners: ljarin:kr_autonomous_flight. Branch: [dev_not_fixed_dt](https://github.com/ljarin/kr_autonomous_flight/tree/dev_not_fixed_dt)
2. Maps: We have consolidated all three types of maps into one repo [kr_param_map](https://github.com/KumarRobotics/kr_param_map). Maze file generator can be found [here](https://github.com/shaoyifei96/multi_solution_mazegenerator)
3. ECS: Also can be found here [kr_param_map](https://github.com/KumarRobotics/kr_param_map)
4. Datasets: [STPLS3D](https://www.stpls3d.com/) and [M3ED](https://m3ed.io/)


# Citation
```
@article{shao2023design,
  
}
```



