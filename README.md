# Design and Evaluation of Motion Planners for Quadrotors
*What two-stage quadrotor motion planner should I use for my environment?* [arXiv](https://arxiv.org/abs/2309.13720)

![Experiment of Quadrotor flying through a small maze](https://github.com/KumarRobotics/kr_mp_design/blob/main/pics/real_exp_maze.png)

This repo gives a guideline on what motion planners to use for different environments. This repo provided three tools:
1. A set of two-stage motion planners.
2. A set of map generators (obstacle, maze, real datasets).
3. An evaluation metric for any environment called Environment Complexity Signature (ECS). You can use it to evaluate your environment and choose the right motion planner.

This repo is tested with Ubuntu 20.04 and ROS Noetic. Everything in this repo flies on hardware!
### Planners
#### Frontend planners
1. Jump Point Search (JPS)
2. RRT* (OMPL)
3. Motion Planning Primitive (MPL) 
4. Stable Sparse RRT (SST) (OMPL)
5. Dispersion Planner 
#### Backend planners
1. GCOPTER (Differential Flatness)
2. ALTRO (Indirect Trajectory Optimization)
### Maps
All maps are of size 20m x 10m x 5m. We provide three types of maps:
1. Obstacle Map: Random 3D maps with obstacles, where the density of each type can be specified.
2. Maze Map (Image Map Loader): Random 3D maze maps from a 2D png file. Load your own images by specifying a png file or folder.
3. Real Datasets (pcd Map Loader): We cropped data from STPLS3D and M3ED to the same size. Load your own point cloud map by inputting a pcd file.


### Environment Complexity Signature (ECS)
ECS measures the complexity of an environment. It consists of density index, clutter index, and structure index. Please see the paper for which planner performs best in each ECS range. You can use ECS to evaluate your environment and choose the right motion planner.

## Installation
The easies way to is to use vcs to clone all the repos.
Make a ros workspace and cd to src
```
git clone -b dev_not_fixed_dt git@github.com:ljarin/kr_autonomous_flight.git
sudo apt install python3-vcstool
vcs import < kr_autonomous_flight/external_all.yaml #import dependencies, GCOPTER and Motion Primitive will have access issues, please email maintainer to get an copy
vcs import < motion_primitives/deps_ssh.repos # import dispersion planner dependencies
rosdep install --from-paths src --ignore-src -r -y
sudo apt install -y libspdlog-dev  ros-noetic-ompl libpcl-dev libeigen3-dev libtbb-dev libgtest-dev python3-pcl libtool libnlopt-dev
pip3 install pandas tqdm
catkin config --cmake-args -DCMAKE_BUILD_TYPE=Release #if you want other cmake flags later make sure you reset the config
catkin build
```
If building packages require a specific cmake version, follow [this](https://apt.kitware.com/) for cmake installation instructions.

Download the files from [here](https://drive.google.com/drive/folders/1LImwhYTajVImL3pydA4d91aILSOMddD3?usp=sharing) for point-cloud of real maps, pre-generated maze maps, and dispersion planner precomputed offline file. If you want to run obstacle maps with other planners, you do not need these files. 

Next give path to the json file in tracker_params_mp.yaml : dispersion/graph_file: FILL IN PATH 

Coming soon: Splitting the repos to fly the quad to a different repo than the ones that do mapping.
### Components
1. Planners: 
   1. Two-Stage framework to switch between planners. This repo also contains JPS, RRT*, MPL, SST: [kr_autonomous_flight](https://github.com/ljarin/kr_autonomous_flight/tree/dev_not_fixed_dt), [JPS](https://github.com/KumarRobotics/jps3d)
   2. Dispersion Planner: [motion_primitive](https://github.com/ljarin/motion_primitives)
   3. GCOPTER: [GCOPTER](https://github.com/yuwei-wu/GCOPTER.git)
   4. ALTRO:[kr_ilqr_optimizer](https://github.com/KumarRobotics/kr_ilqr_optimizer/tree/icra_final), [altro](https://github.com/shaoyifei96/altro/tree/ros)
2. Maps: We have consolidated all three types of maps into one repo [kr_param_map](https://github.com/KumarRobotics/kr_param_map). To generate your own maze file, use this generator [here](https://github.com/shaoyifei96/multi_solution_mazegenerator)
3. ECS: To evaluate for a new environment, use [kr_param_map](https://github.com/KumarRobotics/kr_param_map)
4. Datasets: [STPLS3D](https://www.stpls3d.com/) and [M3ED](https://m3ed.io/)


# Citation
```
@misc{shao2023design,
      title={Design and Evaluation of Motion Planners for Quadrotors}, 
      author={Yifei Simon Shao and Yuwei Wu and Laura Jarin-Lipschitz and Pratik Chaudhari and Vijay Kumar},
      year={2023},
      eprint={2309.13720},
      archivePrefix={arXiv},
      primaryClass={cs.RO}
}
```



